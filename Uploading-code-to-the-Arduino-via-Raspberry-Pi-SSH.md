If you want to update your code remotely you can use the Raspberry Pi to compile and upload the code to the Arduino. The InteractionEngine has already all tools installed that are necessary to do this from an RPI.

1. Navigate to the sketchbook folder located in home or `~`.

```shell
cd ~/sketchbook/
```

2. Create a folder for your project into the sketchbook folder and change directory to it.
```shell
mkdir yourFolderName/
cd yourFolderName/
```

3. Copy over the template `makefile` from the blink example with the `cp` command.
```shell
cp ~/sketchbook/blink/makefile makefile
```
4. Create a new `.ino` arduino code file, or upload the file from somewhere else. In this example, we are trying to upload and install the example for the [old Nokia screens available from Adafruit](https://www.adafruit.com/product/338). The [GitHub page](https://github.com/adafruit/Adafruit-PCD8544-Nokia-5110-LCD-library) for this project includes instructions and an example.

To copy the example file directly from Github:
1. Navigate to the example folder [link](https://github.com/adafruit/Adafruit-PCD8544-Nokia-5110-LCD-library/tree/master/examples/pcdtest)
1. Open the example[link](https://github.com/adafruit/Adafruit-PCD8544-Nokia-5110-LCD-library/blob/master/examples/pcdtest/pcdtest.ino)
1. Click on `Raw` to get the direct link to the file [link](https://raw.githubusercontent.com/adafruit/Adafruit-PCD8544-Nokia-5110-LCD-library/master/examples/pcdtest/pcdtest.ino)
1. Use the `wget` command on the RPI to directly download the file in to the folder you created. For this example this looks like:
```shell 
wget https://raw.githubusercontent.com/adafruit/Adafruit-PCD8544-Nokia-5110-LCD-library/master/examples/pcdtest/pcdtest.ino
```

5.Now that the file has been downloaded we need to download and install all required libraries that are used by the Arduino board to communicate with the display. At the top of the Arduino-code file (pcdtest.ino) we can see that we require three additional libraries. This is notated in the Arduino with the `#include` command. The three libraries are:
```arduino
#include <SPI.h>
#include <Adafruit_GFX.h>
#include <Adafruit_PCD8544.h>
```

* `SPI` is a library that is always included with the Arduino development environment(IDE) so we don't need to worry about it for now.

The other two libraries are not standard but are easily found on google/github.
* `Adafruit_GFX` library is available from [GitHub from Adafruit](https://github.com/adafruit/Adafruit-GFX-Library). It is a basic graphics library.
* `Adafruit_PCD8544` Is the actual 'device driver' for the display. Again the[Code for that is on Github](https://github.com/adafruit/Adafruit-PCD8544-Nokia-5110-LCD-library)

Most common libraries for Arduino will be available over GitHub. So these installation instructions should apply ion depend of the library you are trying to install.

1. Lets make a new libraries folder inside the sketchbook folder.
```shell
cd ~/sketchbook/ 
mkdir libraries
cd libraries
```


2. Now that we created and moved the new libraries folder we can download the libraries with `git clone`
```shell
git clone https://github.com/adafruit/Adafruit-GFX-Library
git clone https://github.com/adafruit/Adafruit-PCD8544-Nokia-5110-LCD-library
```
2. After downloading we need to rename the folder. We need to remove the "-Library" part at the end. We do this by `moving` the folder to its new name like so:

```shell
mv Adafruit-GFX-Library Adafruit-GFX
mv Adafruit-PCD8544-Nokia-5110-LCD-library Adafruit-PCD8544
```

Lets repeat this quickly for the other library



```shell
pi@ixe[XX]:~/sketchbook $ tree -L 3
.
├── Arduino.mk -> /usr/share/arduino/Arduino.mk
├── blink
│   ├── blink.ino
│   ├── build-uno
│   │   ├── blink.eep
│   │   ├── blink.elf
│   │   ├── blink.hex
│   │   ├── blink.hex.sizeok
│   │   ├── blink.ino.d
│   │   ├── blink.ino.o
│   │   ├── core
│   │   ├── libcore.a
│   │   ├── libs
│   │   └── userlibs
│   └── makefile
├── helloYouSketch
│   ├── build-uno
│   │   ├── core
│   │   ├── helloYou.elf
│   │   ├── helloYou.hex
│   │   ├── helloYou.hex.sizeok
│   │   ├── helloYouSketch.eep
│   │   ├── helloYouSketch.elf
│   │   ├── helloYouSketch.hex
│   │   ├── helloYouSketch.hex.sizeok
│   │   ├── helloYouSketch.ino.d
│   │   ├── helloYouSketch.ino.o
│   │   └── libcore.a
│   ├── helloYouSketch.ino
│   └── makefile
├── libraries
│   ├── Adafruit-GFX
│   │   ├── Adafruit_GFX.cpp
│   │   ├── Adafruit_GFX.h
│   │   ├── Adafruit_SPITFT.cpp
│   │   ├── Adafruit_SPITFT.h
│   │   ├── Adafruit_SPITFT_Macros.h
│   │   ├── fontconvert
│   │   ├── Fonts
│   │   ├── gfxfont.h
│   │   ├── glcdfont.c
│   │   ├── library.properties
│   │   ├── license.txt
│   │   └── README.md
│   └── Adafruit-PCD8544
│       ├── Adafruit_PCD8544.cpp
│       ├── Adafruit_PCD8544.h
│       ├── examples
│       ├── library.properties
│       ├── license.txt
│       └── README.txt
└── yourFolderName
    ├── makefile
    └── pcdtest.ino

```
Notice how the folder names have been changed to `Adafruit-GFX` and `Adafruit-PCD8544`.

6. Now we need to edit the a make file inside your project to also include the libraries. We do this by specifing the libraries folder name behind the `Arduino_LIBS=` field. After adding the librariesthe makefile should look something like this:

```make
BOARD_TAG = uno
ARDUINO_PORT = /dev/ttyUSB0
ARDUINO_LIBS = SPI Adafruit-GFX Adafruit-PCD8544
ARDUINO_DIR = /usr/share/arduino
include ../Arduino.mk
```

7. One thing that this command line version of Arduino does not do is create `funtion prototypes`. `function protypes` just define at the top of the program what a function is called whith-out defining what it actually does. To compile and run our example code with the display example we need to add the following lines aobve the `void setup(){}` funtion.

```c++
void testdrawline(void);
void testdrawbitmap(const uint8_t *bitmap, uint8_t w, uint8_t h) ;
void testdrawchar(void);
void testdrawcircle(void);
void testfillrect(void);
void testdrawtriangle(void);
void testfilltriangle(void);
void testdrawroundrect(void);
void testfillroundrect(void);
void testdrawrect(void) ;
```

Once You have defined the funtion prototypes you can go ahead and run `make`
```shell
make
```

and then
```shell
make upload
``` 
to compile and then upload your code to the arduino.

 








These are the essential steps in setting up a new project that can compile and upload code to the Arduino. 



