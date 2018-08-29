# Blink!
 
## Overview
For this assignment, you are going to 
A) [Set up a breadboard](#part-a-set-up-a-breadboard) 
B) [Manually blink a LED](#part-b-manually-blink-a-led) 
C) [Blink a LED using the Arduino](#part-c-blink-led-using-the-Arduino)
D) [Manually fade a LED](#part-d-manually-face-a-led) and 
E) [Fade a LED using Arduino](#part-e-timer)
F) Frankenlight (#part-f-frankenlight)
BONUS) [make your timer sing!](#part-e-tone).
 
## In The Report
Include your responses to the bold questions on your own fork of the lab activities. Include snippets of code that explain what you did. Deliverables are due next Tuesday. Post your lab reports as README.md pages on your GitHub, and post a link to that on your main class hub page.

## Part A. Set Up a Breadboard

For this lab, we'll be using the [Adafruit Metro Mini](https://www.adafruit.com/product/2590) development board as our hardware platform. This board is a derivative of the [Arduino UNO R3](https://store.arduino.cc/usa/arduino-uno-rev3). 

You should have already have installed the [Arduino software](http://arduino.cc/en/Main/Software) on your laptop.

Wire the power rails of your breadboard so that the red rails are connected to the +5V pin of the Metro Mini, and the blue or black rails are connected to the GND pin.  

[insert photo of breadboard setup]

## Part B. Manually Blink a LED

**a. What color stripes are on a 100 Ohm resistor?**
With the Arduino unplugged, build the circuit below. Use a 100 Ohm resistor. (Hint, this is not what is shown in the image below.)

![Button LED Resistor schematic]()
If you need a diagram of what this looks like on your board, [here's a hint](docs/button_led_resistor_diagram.png)

**a. What color stripes are on a 100 Ohm resistor?**



## Part C. Blink a LED using Arduino


For this lab, we'll be using the [Adafruit Metro Mini](https://www.adafruit.com/product/2590) development board as our hardware platform. This board is a derivative of the [Arduino UNO R3](https://store.arduino.cc/usa/arduino-uno-rev3). As a platform, Arduino comprises both hardware and software. We'll be using the [Arduino hardware](http://arduino.cc/en/Main/Hardware); for an [IDE](http://en.wikipedia.org/wiki/Integrated_development_environment), you have the option of using the [Arduino software](http://arduino.cc/en/Main/Software) on your laptop.
 
To use your laptop computer for programming the Metro Mini, you will need to download and install the software on your machine:
* [Arduino IDE](https://www.arduino.cc/en/Main/Software) 
* [SiLabs CP210x drivers](http://www.silabs.com/products/mcu/pages/usbtouartbridgevcpdrivers.aspx)
 
**1. Blinking LEDs with Arduino**

Connect the Metro Mini to your computer using the USB cable. Arduino boards typically come preloaded with a version of the Blink program on it. This code lets its LED (connected on pin 13) blink as soon as the USB cable starts powering the board. In this class, we have previously uploaded a different program to the Arduino. (Remember the [helloYouSketch from Lab1](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-%232#2-helloyou-test)). 

To get set up, we will use the Blink example code to see how to upload code to the Arduino from our computer. The Blink program itself can be found in the Arduino IDE's example code folder under [File->Examples->Basics->Blink](https://www.arduino.cc/en/Tutorial/Blink). Check it out!

**a. What line(s) of code do you need to change to make the LED blink (like, at all)?**

**b. What line(s) of code do you need to change to change the rate of blinking?**

**c. What circuit element would you want to add to protect the board and external LED?**
 
To compile and upload your code, take the following steps (note that 1, 2 should only have to be done once):