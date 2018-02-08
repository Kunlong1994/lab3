OpenCV is a great library of computer vision tools an algorithms. This guide will show you how to install a version of OpenCV optimized for your Raspberry Pi onto your IxE.

This guide is based on the tutorial by PyImageSearch [https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi/](https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi/). 

Follow the instructions on [https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi/](https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi/) up to the line where you download OpenCV.

We are installing OpenCV 3.4 which was the newest version at the time this article was created. So, use this line:

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