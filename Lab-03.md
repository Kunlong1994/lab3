# Data Logger (and using cool sensors!)

For this lab, we will be experimenting with a variety of sensors, sending the data to the Arduino serial monitor, writing data to the EEPROM of the Arduino, and then playing the data back.

## Part A.  Writing to the Serial Monitor
Hook up the simple potentiometer voltage divider circuit from Lab 01.
 
[[images/Pot_schem.png]]
 
The LCD display from the Lab 02 is a great and helpful tool for debug purposes; the serial monitor is another. Use the code from `File->Examples->Communication->Graph` as a template to print data from your potentiometer to the serial monitor. Don't disconnect the USB cable after uploading the code; instead, use the serial monitor button on the Arduino IDE (in the upper right corner, magnifying glass icon) to see the data coming from the Arduino. 
 
**a. Based on the readings from the serial monitor, what is the range of the analog values being read?**
 
**b. How many bits of resolution does the analog to digital converter (ADC) on the Arduino have** (hint: where might you look to find this sort of thing)? How many are you using with the range of values you're seeing?
 
You can also read inputs from the serial monitor, or wait for the serial monitor to open before spewing data over the USB line! A nice tutorial on the basic serial transmit functions can be found at http://arduino.cc/en/Tutorial/AnalogReadSerial. You can see from the sample code included in the comments of the Graph program that you could use the serial communication functions to communicate data from your sensors to other programs, such as Processing, Flash, MaxMSP.
 
For this lab, you can use the serial monitor and/or the LCD whenever you are told to display something, depending on what you think is easier/prettier.

## Part B. RGB LED

In your kit, you have a common anode RGB LED. This means that the three LEDs in the RGB package share a common power source, and turn on when the R, G, or B legs have a low enough voltage to cause current to flow.

![RGB LED schematic](https://storage.googleapis.com/stateless-www-faranux-com/2017/02/5mm-RGB-LED-Anode.png)

Modify the Fade code from Lab 1 so that you have the R, G and B leads of the LED on pins 9, 10 and 11, respectively. You will want to change the code so that you can fade each of the colors separately. 

## Part C. Voltage Varying Sensors 
One of the useful aspects of the Arduino is the multitude of analog input pins. We'll explore this more now.
 
### 1. FSR, Flex Sensor, Photo cell, Softpot
Now that you have a set up that lets you look at changes in the analog voltage from the potentiometer, let's swap in other analog sensors!

<img src=https://cdn-shop.adafruit.com/1200x900/166-00.jpg alt="FSR" width=250>

The FSR (force sensitive resistor) changes resistance — in this case when pressure is applied to the FSR. [Here's the datasheet](https://cdn-shop.adafruit.com/datasheets/FSR400Series_PD.pdf). We'll use a voltage divider with a 27kOhm resistor, using the analog input with the previous potentiometer code.

[insert circuit drawing]

a. What resistance values do you see from your force sensor?

b. What kind of relationship does the resistance have as a function of the force applied? (e.g., linear?)

c. Can you change the LED fading code values so that you get the full range of output voltages from the LED when using your FSR?

Now experiment with the [flex sensor](https://www.adafruit.com/product/1070), [photo cell](https://www.adafruit.com/product/161) and [softpot](https://www.adafruit.com/product/178).

a. What resistance do you need to have in series to get a reasonable range of voltages from each sensor?

b. What kind of relationship does the resistance have as a function of stimulus? (e.g., linear?)


### 2. Accelerometer

Some more sophisticated sensors have ICs that measure physical phenomena and then output an analog voltage level, varying voltage much as a voltage divider circuit would. 

<img src=https://cdn-shop.adafruit.com/1200x900/2809-00.jpg alt="Accelerometer" width=250>
 
The accelerometer is a 3-axis, accelerometer based on the LIS3DH. The LIS3DH is a 3.3V part, but the Adafruit board has an onboard voltage regulator so that the part can be powered on 5V power on the Vin pin.
 
[Datasheet](https://cdn-shop.adafruit.com/datasheets/LIS3DH.pdf)
[Product Page](https://www.adafruit.com/product/2809)
 
Unlike the other parts we've used to date, this is a "smart sensor" which can communicate the sensor readings digitally (rather than through an analog voltage) using communication protocols I2C and SPI. We'll be using I2C.
 
[This example code](https://learn.adafruit.com/adafruit-lis3dh-triple-axis-accelerometer-breakout/arduino) is meant to read values from a 3-axis accelerometer out to a computer over the serial monitor. Test it out!
 
Adapt the code to indicate what your readings are on the X, Y and Z axes of the accelerometer on your 16x2 LCD panel.

Now set up the RGB LED so that each color is mapped to the X, Y and Z axes accelerations.
 
Get a feel for the data the accelerometer provides. Pick up the Arduino+accelerometer board and tilt it in various directions. Start by holding it so that the accelerometer board is parallel to the ground. Find in which direction the X reading increases and decreases; do the same for the Y reading.
 
**a. Include your accelerometer read-out code in your write-up.**

### 3. IR Proximity Sensor

<img src=https://cdn-shop.adafruit.com/1200x900/466-02.jpg alt="Proximity Sensor" width=250>

Solder together your IR proximity sensor.

[Product page](https://www.adafruit.com/product/466) 

[IR Proximity sensor Datasheet](https://cdn-shop.adafruit.com/datasheets/vcnl4000.pdf)
 
[JD, Andrea, we need to modify these instructions to show that we can hook these two sensors on the same I2C line]

Use [these instructions and code from Adafruit](https://learn.adafruit.com/using-vcnl4010-proximity-sensor/arduino) to look at the data the sensor returns. What happens when the field of view is clear? Move your hand or a piece of paper over the sensor and see how the readings vary with distance.
 
**a. Describe the voltage change over the sensing range of the sensor. A sketch of voltage vs. distance would work also. Does it match up with what you expect from the datasheet?**

## Optional. Graphic Display

<img src=https://cdn-shop.adafruit.com/1200x900/338-03.jpg alt="LCD display" width=250>

Since you've learned to hook up sensors via I2C, we can also use this serial communication protocol to add displays that use less pins than the 16x2 display we previously used. In your kit is a graphical LCD display with a level shifter, and instructions to hook it up and get it running are [here](https://www.adafruit.com/product/338).

## Part D. Logging values to the EEPROM and reading them back
 
### 1. Design your logger
You've been thinking at a high level about a data logger and what it is used for; now you need to adapt that to the specific implementation. 

In addition to the sensors in your kit, we have sensors from this variety kit: [VKmaker T30 Sensor Module](https://www.amazon.com/VKmaker-Sensors-Modules-Starter-Arduino/dp/B01CS6UMKQ) the separate sensor documentation is [available for download](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/SensorDocumentation.zip).

A lot of the art of data logging is being clever about how to use the sensor. Feel free to engage the teaching team for advice.

Your data logger will have two main modes: one where it logs data and another where it plays the data back. Think a little about what sensors you would like to log data from and how you would like to display your data. Create a state diagram sketch that indicates how you'd like to switch between one mode and the other, and also what you'd like the program to do in each state. This can help you decide what buttons or knobs might be useful for your design.
 
You might make changes to your design before this lab is complete.
 
**a. Turn in a copy of your final state diagram.**

### 2. Reading and writing values to the Arduino EEPROM
The [Atmega 328P](https://www.microchip.com/wwwproducts/en/atmega328p) at the heart of the Arduino has 1024 bytes of internal [EEPROM](http://en.wikipedia.org/wiki/EEPROM) Memory (which is separate from the 32KB of [Program memory](https://en.wikipedia.org/wiki/Read-only_memory) it has for the code it is running.)

**a. How many byte-sized data samples can you store on the Atmega328?**
**b. How would you get your analog data from the ADC to be byte-sized?**

Use the code in the `File->Examples->EEPROM` as a template to write and read your own analog values to Arduino's EEPROM. (Ignore what they say about the EEPROM having only 512 bytes. You'll have to adjust your code to match the EEPROM size of the Arduino Micro. The [Atmega328 datasheet](https://www.microchip.com/wwwproducts/en/atmega328p) tells you how much EEPROM it has too).
 
[Arduino EEPROM Library](https://www.arduino.cc/en/Reference/EEPROM)

### 3. Create your data logger!
Now it's up to you to integrate the software and hardware necessary to interface with your data logger! Your logger should be able to record a stream of analog data (at a sample rate of your desire) and then play it back at some later point in time on the 16x2 LCD display.
 
**a. Record and upload a short demo video of your logger in action.**