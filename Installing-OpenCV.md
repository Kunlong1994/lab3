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
1. Make sure you have enough free space on your system using 

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

2. Install dependencies

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
```


```shell
$ cd ~
$ wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.4.0.zip
$ unzip opencv.zip
$ wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.4.0.zip
$ unzip opencv_contrib.zip
```

```shell
cd ~/opencv-3.4.0/
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
  -D CMAKE_INSTALL_PREFIX=/usr/local \
  -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.0/modules \
  -D ENABLE_NEON=ON \
  -D ENABLE_VFPV3=ON \
  -D BUILD_TESTS=OFF \
  -D INSTALL_PYTHON_EXAMPLES=OFF \
  -D BUILD_EXAMPLES=OFF ..
```

Increase the swap size to make installing easier. We will change this only for completing the install of openCV and then change it back

```shell
sudo nano /etc/dphys-swapfile
```

Change `CONF_SWAPSIZE=100` to `CONF_SWAPSIZE=1024`

Then