You can use the official Arduino IDE to program your Arduino directly from your laptop. We use the desktop Arduino IDE and not the Web Editor.

## Install Arduino IDE

Download the Arduino IDE for your laptop operating system here: [https://www.arduino.cc/en/Main/Software](https://www.arduino.cc/en/Main/Software)

## Install the drivers for the Metro Mini on your laptop

You will need to install the drivers for the Metro Mini to allow it to talk to your laptop. This allows you to burn code and send serial messages back and forth between the Metro Mini and your laptop.

The Metro Mini uses a specific USB Serial chip (the SiLabs CP2104). You will install the drivers for your laptop operating system.

Find the drivers for your laptop operating system here: [https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

Note for Linux Users: No drivers *should* be required for your laptop to communicate with the Metro Mini. You should be able to skip this step, but if it doesn't work, there are drivers for Linux on the SiLabs page.

## Setup the Arduino IDE to talk to the MetroMini

Now, you need to tell the Arduino IDE what type of board you are programming and what port (i.e. USB port) the board is on.

1. Plug in your Arduino using a USB cable to your laptop

2. open the Arduino IDE

3. Choose Tools -> Board -> Arduino/Genuino Uno

3. Choose Tools -> Port -> /dev/cu.SLAB_USBtoUART (on MAC) | /dev/ttyUSB0 (on Linux) | COM3 (on Windows, could be another number)