[OpenCV](https://opencv.org) is a great library with computer vision [tools and algorithms](https://docs.opencv.org/2.4/doc/tutorials/tutorials.html). You can use OpenCV for things like face detection, object detection, and image manipulation.

For class, we are providing two ways of getting OpenCV onto your IxE:

1. Burning an updated OS to your SD card
2. Installing OpenCV on your own

## 1. Burning a new OS with OpenCV pre-installed (~ 20 minutes)

## 2. Installing OpenCV 2.4 on your own (~ 1.5 hours)

This guide will show you how to install a version of OpenCV optimized for your Raspberry Pi onto your IxE.

This guide is based on the tutorial by Adrian Rosebrock at PyImageSearch [https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi/](https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi/). He creates easy to follow guides for working with OpenCV. He primarily used Python, which is included on your Pi, but will not be covered in the class. 

We will be setting up our IxE to allow NodeJS to use OpenCV. There are two main things we need to install, the general purpose OpenCV library and the node-opencv package.

We will install OpenCV 2.4.13.5, the latest OpenCV 2.4 version at the time this guide was written. OpenCV 2.4 is used because it has better compatibility with NodeJS. Although OpenCV 3 is the newest version, OpenCV 2.4 is still actively maintained.

### Prepare your system
#### 1. Make sure you have enough free space on your system using 

```shell
df -h
```

You should see that the first line tells you how much space you have in `/dev/root`

```shell
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        15G  4.4G  9.2G  33% /
devtmpfs        434M     0  434M   0% /dev
tmpfs           438M     0  438M   0% /dev/shm
tmpfs           438M   12M  427M   3% /run
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           438M     0  438M   0% /sys/fs/cgroup
/dev/mmcblk0p1   41M   21M   21M  51% /boot
tmpfs            88M     0   88M   0% /run/user/1000
```

In this case, we have 9.2 GB free (`AVAIL`) on the system. If you have less than 1 GB then you should clean up your system (see the footnotes of this guide)

#### 2. Install dependencies

In order to install OpenCV, we need to install other packages that OpenCV will use. Run each line of the following commands to install the dependencies. The whole process should take between 5 - 10 minutes.

```shell
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install build-essential cmake pkg-config
sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install libgtk2.0-dev libgtk-3-dev
sudo apt-get install libcanberra-gtk*
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install python2.7-dev python3-dev
sudo apt-get autoremove
```

### Download OpenCV 2.4

We need to install OpenCV from the source code. The following commands will download the official OpenCV source code to your IxE and unzip the archive.

```shell
$ cd ~
$ wget -O opencv.zip https://github.com/Itseez/opencv/archive/2.4.13.5.zip
$ unzip opencv.zip
```

### Compile and install OpenCV with optimizations

#### 1. Create the build directory and setup for compilation

First, go into the OpenCV 2.4 directory and create a `build` directory where we will compile OpenCV
```shell
cd opencv-2.4.13.5/
mkdir build
cd build
```

Next, compile OpenCV with the following settings. Specifically, `enable_NEON=ON` and `enable_VFPV3=ON`. These tell OpenCV to take advantage of some hardware optimizations of the ARM processor that the Raspberry Pi has. You can read more about this from Adrian Rosebrocks [guide](https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi).

Copy all the commands below into your terminal and then hit enter/return.

```shell
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D ENABLE_NEON=ON \
    -D ENABLE_VFPV3=ON \
    -D BUILD_TESTS=OFF \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D BUILD_EXAMPLES=OFF ..
```

#### 2. Increase the swap space for faster compiling

Increase the swap space to make installing faster and allow you to use all four cores on the Raspberry Pi. We will change this only for completing the install of OpenCV and then change it back since this can shorten the life of your SD card.

Edit the `dphys-swapfile` using `sudo`

```shell
sudo nano /etc/dphys-swapfile
```

Change the line `CONF_SWAPSIZE=100` to `CONF_SWAPSIZE=1024`

Save and exit the file using `Ctrl+X, yes`

Restart the swap service 

```shell
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
```

#### 3. Compile and install OpenCV (takes ~40 minutes)

Now we will compile OpenCV. This will take a long time since the Raspberry Pi processors is not that powerful. Even when using four cores, it will take about 40 minutes to compile everything.

Run `make` with the  four core compile option `-j4`

```shell
make -j4
```

Wait until the OpenCV has full compiled. It will reach 100% and then should go back to the command prompt and allow you to type commands. Do not power off your Pi while you are compiling.

After OpenCV is compiled, install and configure using

```shell
sudo make install
sudo ldconfig
```

#### 4. Decrease your swap space

Now that OpenCV is installed, reduce the swap space back to the original value of 100

```shell
sudo nano /etc/dphys-swapfile
```

Change the line `CONF_SWAPSIZE=1024` to `CONF_SWAPSIZE=100`

Save and exit the file using `Ctrl+X, yes`

Restart the swap service 

```shell
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
```

### Install node-opencv into a project

Now that you have OpenCV installed, let's create a new NodeJS project and install the [node-opencv package](https://www.npmjs.com/package/opencv). This will allows us to use OpenCV with NodeJS.

#### 1. Create a new project

First, create a new project directory where we can test the library

```shell
cd ~
mkdir node-opencv-test
cd node-opencv-test
```

#### 2. Install node-opencv

```shell
npm install opencv
```

#### 3. Run the test

To check and make sure everything is working, we will run the `face-detection` example.

Create a new file called `face-detection.js`

```shell
nano face-detection.js
```

Then copy the following code into the editor

```javascript
cv.readImage("./examples/files/mona.png", function(err, im){
  im.detectObject(cv.FACE_CASCADE, {}, function(err, faces){
    for (var i=0;i<faces.length; i++){
      var x = faces[i]
      im.ellipse(x.x + x.width/2, x.y + x.height/2, x.width/2, x.height/2);
    }
    im.save('./out.jpg');
  });
})
```

Save and exit the file using `Ctrl+X, yes`

Run the code using NodeJS

```shell
node face-detection.js
```

If everything is working correctly, then you should see the following output:

```shell

```

