[OpenCV](https://opencv.org) is a great library with computer vision [tools and algorithms](https://docs.opencv.org/2.4/doc/tutorials/tutorials.html). You can use OpenCV for things like face detection, object detection, and image manipulation.

For class, we are providing two ways of getting OpenCV onto your IxE:

1. Burning an updated OS to your SD card
2. Installing OpenCV on your own

## 1. Burning a new OS with OpenCV pre-installed (~ 45 minutes)
*This is easiest if you are connected to the DeviceFarm network.*

Burning a new version of the IxE version of the Raspbian OS is the fastest way to get OpenCV, but it means you will overwrite your entire SD card and start with a fresh system. It will still have all our examples built in, but none of the code you have written. Thus we will backup your code and then reinstall the OS.

### Back up your code

Make sure your code is backed up on Github. You can go into each project directory that you are working on and `commit` and `push` your code to Github.com. Instructions for using Git with your code can be found [here](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Forking-a-GitHub-project)

Inside of a project directory that is git enabled, run

```shell
git commit -m "Write your commit message here"
git push
```

### Copy any other files off your Pi to your laptop

If you have other files, like images, sounds, or code that is not backed up on a Git repo, you can copy the files to your laptop. To do this, we have enabled the Samba Filesharing service on your IxE. Samba will allow you to browse the Pi's file system using your laptop native file explorer (Finder on Mac, Explorer on Windows). Here is how to connect to the Samba file share.

First, make sure your laptop is on the same network as your IxE (for example both computers are on DeviceFarm or your own WiFi).

#### On Mac
1. Open Finder

2. Click `Go` -> `Connect to Server` in the top toolbar

3. In *Server Address* put `smb://ixe[00].local` replacing `[00]` with your IxE number.

4. Put in your username (default is `pi`) and password to your IxE in the new window and click connect.

5. Select the `homes` volume and click Ok

6. Browse your file system and copy your file using drag and drop or Cmd+C and Cmd+V paste onto your laptop.

#### On PC

1. Go to the Windows File Explorer

2. In the left navigation pane, right-click *My Computer*

3. Choose *Map Network Drive*

4. In the location put in `\\ixe[00]\homes` replacing [00] with your IxE number

5. Uncheck *Reconnect at login*

6. Check *Use different credentials*

7. Click connect

8. Put in your IxE username (default: `pi`) and password into the pop-up. You may need to click *Choose another user*

9. Click connect, a new Explorer window should pop up and show your files

10. Browse your file system and copy your file using drag and drop or Ctrl+C and paste Ctrl+V onto your laptop.

**Make sure to do backup everything you want to keep! Once you start burning a new OS there is no way to get your files back.**

### Download our latest IxE Raspbian OS image onto your laptop

You can download the latest OS here: [https://www.dropbox.com/s/pp2lpznt6kd1vl5/IxE_2018-02-22.img.zip?dl=0](https://www.dropbox.com/s/pp2lpznt6kd1vl5/IxE_2018-02-22.img.zip?dl=0)

### Download and install Etcher

[Etcher](https://etcher.io) is a nice GUI program that can help you burn the IxE OS image to your SD card. Download the version for your laptop OS.

### Shut down your IxE

While logged into your IxE using the Terminal, shut down the IxE using

```shell
sudo halt
```

After the green light stops blinking, pull out the power cable.

### Take your SD card and mount on your laptop

Remove the SD card from the Raspberry Pi. Us an SD card adapter and plug it into your computer. If you have an SD card slot, you can use a micro-SD to SD card adapter (available on our cart in the Maker Lab). If you do not have an SD card slot, you can use a micro-SD to USB 3 adapter (there will be a pink adapter on the cart in the Maker Lab -- please do not lose this!).

### Burn the IxE disk image using Etcher

1. Open Etcher

2. Click *Select Image* and choose `IxE_10FEB2018.img` from the location where you download the disk image file

3. The SD card should be selected automatically, but if not, click *Select Drive* and choose the SD card. It should be about 15 GB.

4. Click *Flash!*

Etcher will then flash the IxE disk image to your SD card. This should take about 25 minutes.

### Optional: Setup your WiFi
If you are not on DeviceFarm and want to use your home WiFi or the House WiFi, follow the instructions [here](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Other-ways-to-connect-IxE-to-your-computer) to edit the `wpa_supplicant.conf` file in the `boot` partition so that you can connect to your own Wifi.

### Reboot your IxE

Once the image is flashed/burned to the SD card, you can remove it from your computer and reinsert the card into your Raspberry Pi. Make sure the Raspberry Pi's power cable is unplugged.

Once the card is back in the Raspberry Pi, plug in the power to turn on the Pi.

Since we have reflashed the Pi, it will only have the DeviceFarm WiFi preprogrammed (unless you did the previous step and set it up for your own WiFi). Make sure that your laptop is connected to the same network as your Pi.


### Log in and rename your IxE

Since this is the base image, your Pi will be named `ixe00`. To connect, you can open a terminal and ssh

```shell
ssh pi@ixe00
```

The password is `raspberry`

Once you are logged in, change the hostname to your original number (written on the SD card we gave you). To do this you will change two files, `/etc/hostname` and `etc/hosts/`

1. Edit `/etc/hostname` using

```shell
sudo nano /etc/hostname
```

Change `ixe00` to `ixe[00]` where [00] is your number

Save and exit using `Ctrl + X, yes`

2. Edit `/etc/hosts` using

```shell
sudo nano /etc/hosts
```

Change the last line of the file from 

```shell
127.0.1.1       ixe00
```

to 

```shell
127.0.1.1       ixe[00]
```

replacing the [00] with your number.

Save and exit using `Ctrl + X, yes`

### Reboot your IxE

For the hostname change to take effect, reboot using

```shell
sudo reboot
```

### Reconnect to your IxE

With the hostname changed, you should be able to reconnect to you IxE using your original number. You can ssh using

```shell
ssh pi@ixe[00].local
```

### Put your files back on
After you log in, you can reconnect to the Samba file share to put back all the files you copied over to your laptop. You can do this using drag and drop

You can also put your Git repositories back on using

```shell
git clone https://github.com/YOUR-REPO-HERE
```

You will need to do this for every repository you would like to have back on your Pi.

### Test OpenCV with NodeJS

You can test that OpenCV works with NodeJS by trying the `face-detection.js` sample in the `node-opencv-test` directory.

```shell
cd node-opencv-test/
node face-detection.js
```

If everything is working correctly, then you should see the following output:

```shell
Image saved to out.jpg!
```

You can see the file by typing `ls` and listing at the files in the directory

```shell
ls
face-detection.js  node_modules  out.jpg  package-lock.json
```

To see the actual image, you can open the file by using the Samba file sharing feature, discussed here or you can copy it to your laptop using `scp` from another Terminal window on your laptop. The following line will copy the file from your IxE to your Desktop. Remember to change the [00] with you IxE number.

```shell
scp pi@ixe[00].local:~/node-opencv-test/out.jpg ~/Desktop
```

### Use `node-opencv` in your own projects

Now that everything is working, you can start using OpenCV in your own NodeJS projects. You can install the library to a project using

```shell
npm install opencv --save
```

To use the library in your javascript code, include the `require` line at the top of your code file

```js
var cv = require('opencv');
```

Check out the [examples](https://github.com/peterbraden/node-opencv/tree/master/examples) to see how things work and to build your code off the great work of [Peter Braden](https://github.com/peterbraden/node-opencv).


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

Now that you have OpenCV installed, let's create a new NodeJS project and install the [node-opencv package](https://www.npmjs.com/package/opencv), created by Peter Braden. This will allows us to use OpenCV with NodeJS.

#### 1. Create a new project

First, create a new project directory where we can test the library

```shell
cd ~
mkdir node-opencv-test
cd node-opencv-test
```

#### 2. Install node-opencv

Run

```shell
npm install opencv
```

This will take about 5 minutes since it will compile a number of packages.

#### 3. Run the test

To check and make sure everything is working, we will run the `face-detection` example. This code will detect a face in an image then put a red circle around it. We will run the example with an image of the Mona Lisa included in the `examples` directory of the `opencv` package.

Create a new file called `face-detection.js`

```shell
nano face-detection.js
```

Then copy the following code into the editor

```javascript
var cv = require('opencv');

cv.readImage("node_modules/opencv/examples/files/mona.png", function(err, im){
  im.detectObject(cv.FACE_CASCADE, {}, function(err, faces){
    for (var i=0;i<faces.length; i++){
      var x = faces[i]
      im.ellipse(x.x + x.width/2, x.y + x.height/2, x.width/2, x.height/2);
    }
    im.save('out.jpg');
    console.log('Image saved to out.jpg!')
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
Image saved to out.jpg!
```

You can see the file by typing `ls` and listing at the files in the directory

```shell
ls
face-detection.js  node_modules  out.jpg  package-lock.json
```

To see the actual image, you can open the file by using the Samba file sharing feature, discussed here or you can copy it to your laptop using `scp` from another Terminal window on your laptop. The following line will copy the file from your IxE to your Desktop. Remember to change the [00] with you IxE number.

```shell
scp pi@ixe[00].local:~/node-opencv-test/out.jpg ~/Desktop
```

### Use `node-opencv` in your own projects

Now that everything is working, you can start using OpenCV in your own NodeJS projects. You can install the library to a project using

```shell
npm install opencv --save
```

To use the library in your javascript code, include the `require` line at the top of your code file

```js
var cv = require('opencv');
```

Check out the [examples](https://github.com/peterbraden/node-opencv/tree/master/examples) to see how things work and to build your code off the great work of [Peter Braden](https://github.com/peterbraden/node-opencv).