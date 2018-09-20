# Data Logger (and using cool sensors!)

For this lab, we will be experimenting with a variety of sensors, sending the data to the Arduino serial monitor, writing data to the EEPROM of the Arduino, and then playing the data back.

## Overview

What's in this lab?

A. [Writing to the Serial Monitor](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-03#part-a--writing-to-the-serial-monitor)

B. [RGB LED](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-03#part-b-rgb-led)

C. [Voltage Varying Sensors](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-03#part-c-voltage-varying-sensors)

D. [I2C Sensors](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-03#part-d-i2c-sensors)

E. [Optional: Graphic Display](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-03#optional-part-e-graphic-display)

F. [Logging Values to the EEPROM and Reading Them Back](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-03#part-f-logging-values-to-the-eeprom-and-reading-them-back)

G. [Create your own Data logger!](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-03#part-g-create-your-own-data-logger)

## In The Report
Include your responses to the bold questions on your own fork of [this lab report template](https://github.com/FAR-Lab/IDD-Fa18-Lab3). Include snippets of code that explain what you did. Deliverables are due next Tuesday. Post your lab reports as README.md pages on your GitHub, and post a link to that on your main class hub page.

## Part A.  Writing to the Serial Monitor
Hook up the simple potentiometer voltage divider circuit from Lab 01.
 
[[images/Pot_schem.png]]
 
The LCD display from the Lab 02 is a great and helpful tool for debug purposes; the serial monitor is another. Use the code from `File->Examples->Communication->Graph` as a template to print data from your potentiometer to the serial monitor. Don't disconnect the USB cable after uploading the code; instead, use the serial monitor button on the Arduino IDE (in the upper right corner, magnifying glass icon) to see the data coming from the Arduino. 
 
**a. Based on the readings from the serial monitor, what is the range of the analog values being read?**
 
**b. How many bits of resolution does the analog to digital converter (ADC) on the Arduino have** (hint: where might you look to find this sort of thing)? How many are you using with the range of values you're seeing?
 
You can also read inputs from the serial monitor, or wait for the serial monitor to open before spewing data over the USB line! A nice tutorial on the basic serial transmit functions can be found at http://arduino.cc/en/Tutorial/AnalogReadSerial. 

NEW!!! Also you can plot the data with the Arduino Serial Plotter! This can be found under `Tools->Serial Plotter`. Try it out.
 
For this lab, you can use the serial monitor, plotter and/or the LCD whenever you are told to display something, depending on what you think is easier/prettier.

## Part B. RGB LED

In your kit, you have a common anode RGB LED. This means that the three LEDs in the RGB package share a common power source, and turn on when the R, G, or B legs have a low enough voltage to cause current to flow.

![RGB LED schematic](images/rgbled.png)

<!--Modify the Fade code from Lab 1 so that you have the R, G and B leads of the LED on pins 9, 10 and 11, respectively. You will want to change the code so that you can fade each of the colors separately.-->
[Here is sample code](https://learn.adafruit.com/adafruit-arduino-lesson-3-rgb-leds/arduino-sketch) that controls the color of an RGB LED using the Arduino.  

<!--**How might you use this with only the parts in your kit? Show us your solution.**-->

## Part C. Voltage Varying Sensors 
One of the useful aspects of the Arduino is the multitude of analog input pins. We'll explore this more now.
 
### FSR
Now that you have a set up that lets you look at changes in the analog voltage from the potentiometer, let's swap in other analog sensors!

<img src=https://cdn-shop.adafruit.com/1200x900/166-00.jpg alt="FSR" width=400>

The FSR (force sensitive resistor) changes resistance — in this case when pressure is applied to the FSR. [Here's the datasheet](https://cdn-shop.adafruit.com/datasheets/FSR400Series_PD.pdf). We'll use a voltage divider with a 27kOhm resistor, using the analog input with the previous potentiometer code. (Feel free to use a 10kOhm resistor instead, or anything in this range.)

[[images/fsr_voltage_divider.png]]

We need a voltage divider because the Arduino can't measure resistance directly, which is the thing that changes when you physically interact with the sensor. A voltage divider circuit converts a change in resistance to a change in voltage.

**a. What voltage values do you see from your force sensor?**

**b. What kind of relationship does the voltage have as a function of the force applied? (e.g., linear?)**

**c. In `Examples->Basic->Fading` the LED values range from 0-255. What do you have to do so that you get the full range of output voltages from the LED when using your FSR to change the LED color?**

## Flex Sensor, Photo cell, Softpot
Now experiment with the [flex sensor](https://www.adafruit.com/product/1070), [photo cell](https://www.adafruit.com/product/161) and [softpot](https://www.adafruit.com/product/178).

<img src=https://cdn-shop.adafruit.com/1200x900/1070-01.jpg alt="flex sensor" width=250>
<img src=https://cdn-shop.adafruit.com/1200x900/161-00.jpg alt="photocell" width=250>
<img src=https://cdn-shop.adafruit.com/1200x900/178-00.jpg alt="softpot" width=250>

**a. What resistance do you need to have in series to get a reasonable range of voltages from each sensor?**

**b. What kind of relationship does the resistance have as a function of stimulus? (e.g., linear?)**


## Part D. I2C Sensors 

Some more sophisticated sensors have ICs that measure physical phenomena and then output an digital signal indicating what the analog voltage reading is. 
### Accelerometer
<img src=https://cdn-shop.adafruit.com/1200x900/2809-00.jpg alt="Accelerometer" width=400>
 
The accelerometer is a 3-axis, accelerometer based on the LIS3DH. The LIS3DH is a 3.3V part, but the Adafruit board has an onboard voltage regulator so that the part can be powered on 5V power on the Vin pin.
 
Here's the [Datasheet](https://cdn-shop.adafruit.com/datasheets/LIS3DH.pdf) [Product Page](https://www.adafruit.com/product/2809).
 
Unlike the other parts we've used to date, this is a "smart sensor" which can communicate the sensor readings digitally (rather than through an analog voltage) using communication protocols I2C and SPI. 
 
[This example code](https://learn.adafruit.com/adafruit-lis3dh-triple-axis-accelerometer-breakout/arduino) is meant to read values from a 3-axis accelerometer out to a computer over the serial monitor. Test it out! Hint: make sure to read the I2C Wiring section carefully, because the picture uses a different kind of Arduino. Here's a Fritzing diagram of the correct wiring:

[[images/LIS3DH_breadboard.png]]
 
Adapt the code to indicate what your readings are on the X, Y and Z axes of the accelerometer on your 16x2 LCD panel.

Now set up the RGB LED so that each color is mapped to the X, Y and Z axes accelerations.
 
Get a feel for the data the accelerometer provides. Pick up the Arduino+accelerometer board and tilt it in various directions. Start by holding it so that the accelerometer board is parallel to the ground. Find in which direction the X reading increases and decreases; do the same for the Y reading.
 
**a. Include your accelerometer read-out code in your write-up.**

### IR Proximity Sensor

<img src=https://cdn-shop.adafruit.com/1200x900/466-02.jpg alt="Proximity Sensor" width=400>

Solder together your IR proximity sensor.

[Product page](https://www.adafruit.com/product/466) 

[IR Proximity sensor Datasheet](https://cdn-shop.adafruit.com/datasheets/vcnl4000.pdf)

This sensor and the accelerometer both use I2C -- conveniently, I2C is actually a "bus" connection type: that means that you can connect lots of sensors to the same pair of Arduino pins (`A4` and `A5`) and the Arduino can communicate with all of them!

Without disconnecting your accelerometer from pins `A4` and `A5`, use [these instructions and code from Adafruit](https://learn.adafruit.com/using-vcnl4010-proximity-sensor/arduino) to look at the data the sensor returns. (Both your accelerometer and IR sensor should be connected to pins `A4` and `A5` now.) 

What happens when the field of view is clear? Move your hand or a piece of paper over the sensor and see how the readings vary with distance.
 
**a. Describe how the readings change over the sensing range of the sensor. A sketch of readings vs. distance would work also. Does it match up with what you expect from the datasheet?**

Now, the beauty of I2C: you can read data from **both** of these sensors in a single sketch. How do you do this? A simple way is to merge the two sketches together. This can be kind of tricky, but the general gist is this: pick one sketch to be the base sketch that you will modify. Then, from the other sketch: first, copy directly over any global variables or functions -- these don't go inside other functions, they are top level. Second, the other sketch's `setup` and `loop` functions' contents should be pasted into the base sketch's `setup` and `loop` functions, respectively. Make sure you're not duplicating anything that only needs to happen once, for example,  `Serial.begin(9600);`.

**b. Upload your merged code to your lab report repository and link to it here.**

## Optional Part E. Graphic Display

<img src=https://cdn-shop.adafruit.com/1200x900/338-03.jpg alt="LCD display" width=400>

Since you've learned to hook up sensors via I2C, we can also use this serial communication protocol to add displays that use less pins than the 16x2 display we previously used. In your kit is a graphical LCD display with a level shifter, and instructions to hook it up and get it running are [here](https://www.adafruit.com/product/338).

## Part F. Logging values to the EEPROM and reading them back
 
### 1. Reading and writing values to the Arduino EEPROM
The sample code in `File->Examples->EEPROM` shows functions from the [Arduino EEPROM Library](https://www.arduino.cc/en/Reference/EEPROM) to write and read values to Arduino's EEPROM. This [modified version of the SwitchState code](code/SwitchState2.zip) employs these functions in three different states. Try it out.

**a. Does it matter what actions are assigned to which state? Why?**

**b. Why is the code here all in the setup() functions and not in the loop() functions?**

Each character in the string is a byte. That is, it takes 8-bits to encode a character, so the number of characters in the string we are writing is the number of bytes we are occupying in EEPROM. The [Atmega 328P](https://www.microchip.com/wwwproducts/en/atmega328p) at the heart of the Arduino has 1024 bytes of internal [EEPROM](http://en.wikipedia.org/wiki/EEPROM) Memory (which is separate from the 32KB of [Program memory](https://en.wikipedia.org/wiki/Read-only_memory) it has for the code it is running.)

**c. How many byte-sized data samples can you store on the Atmega328?**

**d. How would you get analog data from the Arduino analog pins to be byte-sized? How about analog data from the I2C devices?**

**e. Alternately, how would we store the data if it were bigger than a byte? (hint: take a look at the [EEPROMPut](https://www.arduino.cc/en/Reference/EEPROMPut) example)**

Modify the code to take in analog values from your sensors and print them back out to the Arduino Serial Monitor.

### 2. Design your logger
You've been thinking at a high level about a data logger and what it is used for; now you need to adapt that to the specific implementation. 

In addition to the sensors in your kit, we have sensors from this variety kit: [VKmaker T30 Sensor Module](https://www.amazon.com/VKmaker-Sensors-Modules-Starter-Arduino/dp/B01CS6UMKQ) the separate sensor documentation is [available for download](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/2018Spring/SensorDocumentation.zip).

A lot of the art of data logging is being clever about how to use the sensor. Feel free to engage the teaching team for advice.

Your data logger will have two main modes: one where it logs data and another where it plays the data back. Think a little about what sensors you would like to log data from and how you would like to display your data. Create a state diagram sketch that indicates how you'd like to switch between one mode and the other, and also what you'd like the program to do in each state. This can help you decide what buttons or knobs might be useful for your design.
 
You might make changes to your design before this lab is complete.
 
**a. Turn in a copy of your final state diagram.**

## Part G. Create your own data logger!
Now it's up to you to integrate the software and hardware necessary to interface with your data logger! Your logger should be able to record a stream of analog data (at a sample rate of your desire) and then play it back at some later point in time on your display of choice.
 
**a. Record and upload a short demo video of your logger in action.**