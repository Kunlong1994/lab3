In this Lab, we will explore the interaction engine and the use of a webcam.

1. [Fork](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Forking-a-GitHub-project) and git clone the [distant-picture](https://github.com/FAR-Lab/distant-pictures) example project. 
1. Install the basic components for the ode server with 'npm install'
1. Make the [basic button circuit](#basic-button-circuit) on your breadboard.
1. Connect the Arduino with a usb cable and [find its port](#check-port-of-arduino-board).
1. [Compile](#compile-arduino-code) and [upload](#upload-arduino-code) the Arduino code.
1. Plugin the webcam
1. start the server with `node server.js /dev/ttyUSB0`
1. [Change the behavior](#change-the-interaction) of the interaction. 

## Basic Button Circuit

In this example, we will have a button connected to an Arduino attached to the IxE via a USB cable change the background color of our webpage. Then we can use a button on the webpage to turn an LED on the Arduino on and off.

For this example, we will need this circuit, with the button connected to `pin 2`. The LED is built in on the board and connected to `pin 13`.

[[images/metroCircuit.png]]

### Find Arduino sketch file
With the circuit built, we will need to program the Arduino. You can do this with your laptop and Arduino IDE if you want. But for now, we would like to show you a tool for compiling and uploading code from the command line called ArduinoMK. This is useful for doing over the air updates to your code and means you don't have to unplug or uninstall your Arduino each time you want to change the firmware. This is really nice when you have it embedded into a project.

For now, we will just upload prebuilt code.

In the `distant-pictures` directory there is a `ArduinoCode` directory that is where the Arduino examples for this assignment are. Let's change directories and list the contents.

```shell
pi@ixe05 ~ $ cd ~/distant-pictures/ArduinoCode
pi@ixe05 ~/distant-pictures/ArduinoCode $ ls
ArduinoCode.ino  build-uno  makefile
```
Befor we can build and upload the Arduino code we need to find the connection port of the arduino. Plugin the Arudino in over USB with the supplied short USB cable. 


### Check port of Arduino board
To see what port the Arduino is on we can us `ls /dev/tty*` (`*` is a wildcard, giving us al listings with anything after the `*`). In this case, the Arduino Uno we use is usually at `/dev/ttyUSB*` where `*` will be a number and most of the time is 0.

```shell
pi@ixe05 ~/sketchbook/blink $ ls /dev/ttyUSB*
/dev/ttyUSB0
```

This tells us that we have a port at `/dev/ttyUSB0`, which is our Arduino. This might differ for your Arduino if other serial devices or pluged in.


To build and upload this program this port needs to be filled into the makefile.

Just call 'cat makefile' to see if the 'ARDUINO_PORT' is set correctly.

```shell
pi@ixe05 ~/sketchbook/blink $ cat makefile
BOARD_TAG = uno
ARDUINO_PORT = /dev/ttyUSB0
ARDUINO_LIBS =
ARDUINO_DIR = /usr/share/arduino
include ../Arduino.mk
```

Here we can see that board type is `uno` and the port is set correctly to `/dev/ttyUSB0`. We are now ready to compile an upload our code.

### Compile Arduino Code
To compile code, use the command `make`.

```shell 
pi@ixe05 ~/distant-pictures/ArduinoCode $ make
-------------------------
Arduino.mk Configuration:
- [AUTODETECTED]       CURRENT_OS = LINUX 
- [USER]               ARDUINO_DIR = /usr/share/arduino 
- [COMPUTED]           ARDMK_DIR = /usr/share/arduino (relative to Common.mk)
- [AUTODETECTED]       ARDUINO_VERSION = 105 
- [DEFAULT]            ARCHITECTURE =  
- [DEFAULT]            ARDMK_VENDOR = arduino 
- [AUTODETECTED]       ARDUINO_PREFERENCES_PATH = /home/pi/.arduino/preferences.txt 
- [DEFAULT]            ARDUINO_SKETCHBOOK = /home/pi/sketchbook 
- [BUNDLED]            AVR_TOOLS_DIR = /usr/share/arduino/hardware/tools/avr (in Arduino distribution)
- [COMPUTED]           ARDUINO_LIB_PATH = /usr/share/arduino/libraries (from ARDUINO_DIR)
- [COMPUTED]           ARDUINO_VAR_PATH = /usr/share/arduino/hardware/arduino//variants (from ARDUINO_DIR)
- [COMPUTED]           BOARDS_TXT = /usr/share/arduino/hardware/arduino//boards.txt (from ARDUINO_DIR)
- [DEFAULT]            USER_LIB_PATH = /home/pi/sketchbook/libraries (in user sketchbook)
- [DEFAULT]            PRE_BUILD_HOOK = pre-build-hook.sh 
- [USER]               BOARD_TAG = uno 
- [COMPUTED]           CORE = arduino (from build.core)
- [COMPUTED]           VARIANT = standard (from build.variant)
- [COMPUTED]           OBJDIR = build-uno (from BOARD_TAG)
- [COMPUTED]           ARDUINO_CORE_PATH = /usr/share/arduino/hardware/arduino//cores/arduino (from ARDUINO_DIR, BOARD_TAG and boards.txt)
- [ASSUMED]            MONITOR_BAUDRATE = 9600 
- [DEFAULT]            OPTIMIZATION_LEVEL = s 
- [DEFAULT]            MCU_FLAG_NAME = mmcu 
- [DEFAULT]            CFLAGS_STD = -std=gnu11 -flto -fno-fat-lto-objects 
- [DEFAULT]            CXXFLAGS_STD = -std=gnu++11 -fno-threadsafe-statics -flto 
- [COMPUTED]           DEVICE_PATH = /dev/ttyUSB0 (from MONITOR_PORT)
- [DEFAULT]            FORCE_MONITOR_PORT =  
- [AUTODETECTED]       Size utility: AVR-aware for enhanced output
- [COMPUTED]           BOOTLOADER_PARENT = /usr/share/arduino/hardware/arduino//bootloaders (from ARDUINO_DIR)
- [COMPUTED]           ARDMK_VERSION = 1.5 
- [COMPUTED]           CC_VERSION = 4.9.2 (avr-gcc)
-------------------------
mkdir -p build-uno
/usr/share/arduino/hardware/tools/avr/bin/avr-objcopy -j .eeprom --set-section-flags=.eeprom='alloc,load' \
	--no-change-warnings --change-section-lma .eeprom=0 -O ihex build-uno/blink.elf build-uno/blink.eep
```

This compiles the code and will give errors if there are some. This is actualy all the same output you would get if you used your Arduino IDE in verbose mode and looked at all the output in the bottom window.

### Upload Arduino Code
Now, lets upload the code using `make upload`.

```shell
pi@ixe05 ~/distant-pictures/ArduinoCode $ make upload
-------------------------
Arduino.mk Configuration:
- [AUTODETECTED]       CURRENT_OS = LINUX 
- [USER]               ARDUINO_DIR = /usr/share/arduino 
- [COMPUTED]           ARDMK_DIR = /usr/share/arduino (relative to Common.mk)
- [AUTODETECTED]       ARDUINO_VERSION = 105 
- [DEFAULT]            ARCHITECTURE =  
- [DEFAULT]            ARDMK_VENDOR = arduino 
- [AUTODETECTED]       ARDUINO_PREFERENCES_PATH = /home/pi/.arduino/preferences.txt 
- [DEFAULT]            ARDUINO_SKETCHBOOK = /home/pi/sketchbook 
- [BUNDLED]            AVR_TOOLS_DIR = /usr/share/arduino/hardware/tools/avr (in Arduino distribution)
- [COMPUTED]           ARDUINO_LIB_PATH = /usr/share/arduino/libraries (from ARDUINO_DIR)
- [COMPUTED]           ARDUINO_VAR_PATH = /usr/share/arduino/hardware/arduino//variants (from ARDUINO_DIR)
- [COMPUTED]           BOARDS_TXT = /usr/share/arduino/hardware/arduino//boards.txt (from ARDUINO_DIR)
- [DEFAULT]            USER_LIB_PATH = /home/pi/sketchbook/libraries (in user sketchbook)
- [DEFAULT]            PRE_BUILD_HOOK = pre-build-hook.sh 
- [USER]               BOARD_TAG = uno 
- [COMPUTED]           CORE = arduino (from build.core)
- [COMPUTED]           VARIANT = standard (from build.variant)
- [COMPUTED]           OBJDIR = build-uno (from BOARD_TAG)
- [COMPUTED]           ARDUINO_CORE_PATH = /usr/share/arduino/hardware/arduino//cores/arduino (from ARDUINO_DIR, BOARD_TAG and boards.txt)
- [ASSUMED]            MONITOR_BAUDRATE = 9600 
- [DEFAULT]            OPTIMIZATION_LEVEL = s 
- [DEFAULT]            MCU_FLAG_NAME = mmcu 
- [DEFAULT]            CFLAGS_STD = -std=gnu11 -flto -fno-fat-lto-objects 
- [DEFAULT]            CXXFLAGS_STD = -std=gnu++11 -fno-threadsafe-statics -flto 
- [COMPUTED]           DEVICE_PATH = /dev/ttyUSB0 (from MONITOR_PORT)
- [DEFAULT]            FORCE_MONITOR_PORT =  
- [AUTODETECTED]       Size utility: AVR-aware for enhanced output
- [COMPUTED]           BOOTLOADER_PARENT = /usr/share/arduino/hardware/arduino//bootloaders (from ARDUINO_DIR)
- [COMPUTED]           ARDMK_VERSION = 1.5 
- [COMPUTED]           CC_VERSION = 4.9.2 (avr-gcc)
-------------------------
mkdir -p build-uno
make reset
make[1]: Entering directory '/home/pi/distant-pictures/ArduinoCode'
/usr/bin/ard-reset-arduino  /dev/ttyUSB0
make[1]: Leaving directory '/home/pi/distant-pictures/ArduinoCode'
make do_upload
make[1]: Entering directory '/home/pi/distant-pictures/ArduinoCode'
/usr/share/arduino/hardware/tools/avr/../avrdude -q -V -p atmega328p -C /usr/share/arduino/hardware/tools/avr/../avrdude.conf -D -c arduino -b 115200 -P /dev/ttyUSB0 \
		-U flash:w:build-uno/ArduinoCode.hex:i

avrdude: AVR device initialized and ready to accept instructions
avrdude: Device signature = 0x1e950f (probably m328p)
avrdude: reading input file "build-uno/ArduinoCode.hex"
avrdude: writing flash (2108 bytes):
avrdude: 2108 bytes of flash written

avrdude: safemode: Fuses OK (E:00, H:00, L:00)

avrdude done.  Thank you.

make[1]: Leaving directory '/home/pi/distant-pictures/ArduinoCode'
```

If everything works, you should see the above output and your Arduino to should flash while programming. Now, let's connect it to the webserver and our webpage.

## Running the webserver with node.js
First navigate out of the 'ArduinoCode' directory with 'cd ..'.
Then run the code similar to last weeks assignment. Howver, we also need to pass reference to the Arduino port to the server.  The command should look something like `node server.js /dev/ttyUSB0`.

```shell
pi@ixe05 ~/distant-pictures $ node server.js /dev/ttyUSB0
listening on *:8000
```

If everything is working, you should see a message in the terminal that the webserver is listening on port 8000.

Just like in the [previous assignment](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-%231#connect-to-your-interaction-engine) you can now go to the browser to controll the arduino and webcam. 

To shut down the server, type `control + C` in the terminal.

```shell
ledOFF
ledON
^C
pi@ixe05 ~/helloYou $
```
## Change the Interaction
For this weeks lab we want to you to change extend the functionality of this basic setup. As a start we want you to change its behavior so that it takes a picture when ever someone presses on the physical button and not from the website. 
