# Make a Digital Timer!
 
## Overview
For this assignment, you are going to 1) make sounds with your Arduino, 2) write to a text LCD panel, 3) explore cool inputs, and 4) make your very own timer.
 
## In The Report
Include your responses to the green questions. Include snippets of code that explain what you did, and please follow the Lab Report Guidelines. Deliverables are due next Tuesday. Post your lab reports as 'wiki' pages on your GitHub, and post the link to Slack under your own channel and #Lab4.

## Part A. Revisiting Blink

For this lab, we'll be using the [Adafruit Metro Mini](https://www.adafruit.com/product/2590) development board as our hardware platform. This board is derivative of the [Arduino UNO R3](https://store.arduino.cc/usa/arduino-uno-rev3). As a platform, Arduino comprises both hardware and software. We'll be using the the [Arduino hardware](http://arduino.cc/en/Main/Hardware); for an [IDE](http://en.wikipedia.org/wiki/Integrated_development_environment), you have the option of using the [Arduino software](http://arduino.cc/en/Main/Software) on your laptop or the command line compiler on on the Pi.
[David & Andrea, need you to describe how to do the command line bits clearly below]
 
If you'd like to use your own laptop computer for programming the Metro Mini, you will need to download and install the software on your machine. 
 
** 1. Blinking LEDs with Arduino **

Connect the Arduino Micro to your computer using the USB cable. The Arduino Micro board comes preloaded with a version of the Blink program on it, so its LED should start blinking as soon as the USB cable starts powering the board. This LED is hardwired to pin 13 of Arduino Micro. 
 
The Blink program itself can be found in the Arduino IDE's example code folder under [File->Examples->Basics->Blink](https://www.arduino.cc/en/Tutorial/Blink). Check it out!
** a. What line(s) of code do you need to change to make the LED blink (like, at all)? **
** b. What line(s) of code do you need to change to change the rate of blinking? **
** c. What circuit element would you want to add to protect the board and LED? **
 
To compile and upload your code, take the following steps (note that 1, 2 should only have to be done once):
 
1) In the Arduino program, select the board we are using: Tools -> Board -> Arduino UNO R3
[please double check this]
2) You may also have to select a communications (or COM) port (Tools -> Serial Port). Ask an instructor to help you choose the right port.
3) To compile your code, click on the "checkmark" on the upper far left of the Arduino development window.
4) To upload compiled code to the Arduino, click on "right arrow" besides "checkmark".
5) When the code is uploaded, the Arduino should automatically start running your new code.
 
Now modify the circuit and program so that you can blink an external LED on pin 9. Don't forget about question (c) above! (Also, don't forget to power and ground the power and ground rails of your breadboard, respectively!)
 
Some tips and reminders:
 
We don't have extra Arduinos, so be careful.
Remember that the USB connected to the Arduino supplies power.
Check that there are no shorts between power and ground before you plug in the USB cable (and apply power).
Unplug power before modifying circuits!
 
** 2. Toggle LEDs on and off using Arduino **
With your LED still connected on digital pin 9, hook up a button circuit on digital pin 2, so that the pushbutton attaches from pin 2 to ground, and so that there is a 10K resistor attached between pin 2 and Vcc. (Vcc is the supply voltage. In this case, it is 5 V.).
 
Use either the same circuit you used for the previous part for the LED or the alternative design below. The alternate circuit causes the "on" state of the LED to occur when Arduino pin = LOW, not HIGH, as before.
 
The Arduino pin configured as an input has a 'high input impedance.' This means that it can sense the voltage without affecting the circuit, like a probe.
 
Use the Button program ([File->Examples->Digital->Button](https://www.arduino.cc/en/Tutorial/Button)) to make your Arduino into a light switch.
** a. Which lines do you need to modify to correspond with your button and LED pins? **
** b. Modify the code or the circuit so that the LED lights only while the button is depressed. Include your code in your lab write-up. **
 
**3. Fading LEDs on and off using Arduino**
What about those "breathing" LEDs on Macs? The fading from bright to dim and back is done using pulse-width modulation (PWM). In essence, the LED is toggled on and off very rapidly, say 1,000 times a second, faster than your eye can follow. The percentage of time the LED is on (the duty) controls the perceived brightness. To control an LED using PWM, you'll have to connect it to one of the pins that support PWM output—which are 4, 5, 6, 9, 10, 11, 12 on the Arduino.
 
Use the Fading program ([File->Examples->Analog->Fading](https://www.arduino.cc/en/Tutorial/Fading)) to make your LED fade in and out.
a) Which line(s) of code do you need to modify to correspond with your LED pin?
b) How would you change the rate of fading?
c) (Extra) Since the human eye doesn't see increases in brightness linearly and the diode brightness is also nonlinear with voltage, how could you change the code to make the light appear to fade linearly?
 
## Part B. Writing to the LCD
Let's use your LCD screen to display some interesting information! There is a good deal of example code for playing with your LCD in the Arduino Examples:
 
> File->Examples->LiquidCrystal
 
Let's start with the "Display" program, which just flashes "Hello World!" This summer's LCDs are a custom part, but there's a lot of information at [this](http://cdn.shopify.com/s/files/1/0038/9582/files/Blue_16x2_5V.pdf?853)  page, the [pinout and dimensions](http://www.longtech-display.com/produts/LCD%20MODULES/longtech%20pdf/LCM1602A.pdf) page and the [LCD controller](http://www.longtech-display.com/produts/LCD%20MODULES/longtech%20pdf/LCM1602A.pdf) page.
 
**a. What voltage level do you need to power your display?**
 
Solder a 16 pin breakaway header to the LCD so you can connect it to your breadboard. 

**If you haven't soldered before, we're happy to show you how! PLEASE ASK.**

Wire up your LCD according to the schematic below. If you didn't have our diagram, you would use the data sheets for the LCD and follow the comments in the "Display" code to figure out how to wire it up. 

[insert images]
 
**Be very careful not to connect together Pin 1 and Pin 2 on the LCD**, as this can **destroy** your Arduino. Check for a short between power and ground before you plug in power or the USB cable.

[insert wiring diagram]
 
See [Tutorial](http://www.arduino.cc/en/Tutorial/LiquidCrystal) for more information. See [LCD Library](http://arduino.cc/en/Reference/LiquidCrystal) for the various functions you can use.
 
The 10K pot connected to Vo on the LCD adjusts the contrast, so try adjusting that if your LCD won't turn on. If it's still not working, try to disconnect your speaker from part A—and check your wiring.
 
LCD pin 15 and 16 (LED+, LED-) are designed for background lighting. If you feel the whole screen too dark, you may try connect pin15(LED+) to +3V or +3.3V and pin16(LED-) to ground. **Don't connect pin15(LED+) to +5V as it may burn background light!**
 
Do try to set this up before peeking at this [diagram](https://www.arduino.cc/en/uploads/Tutorial/LCD_bb.png).
 
Try compiling and running the code. If it doesn't work the first time, check your pinouts...
 
**b. What was one mistake you made when wiring up the display? How did you fix it?**
**c. What line of code do you need to change to make it flash your name instead of "Hello World"?**
 
Try a few of the other examples in the folder to get a feel for the capabilities of your LCD. There is a list of all the possible functions at the [Arduino LiquidCrystal Library](http://arduino.cc/en/Reference/LiquidCrystal?from=Tutorial.LCDLibrary).
 
Leave your LCD set up for Part C and D of the Lab, and leave it set up when you finish Lab, as we'll use the display again next week.
 
## Part C. Advanced Inputs

First, it's important for you to understand that **_analog_** input ("analog pin 0") on your Arduino board shares pins with _**digital**_ input. Below is pinout for the Metro Mini.  The pins with name A0-A12 are analog pins. 
 
[insert diagram]
 
So while a [digitalRead](http://www.arduino.cc/en/Reference/DigitalRead) or [digitalWrite](http://www.arduino.cc/en/Reference/DigitalWrite) command reads or sends only a logic-level high or low, an [analogRead](http://www.arduino.cc/en/Reference/AnalogRead) or [analogWrite](http://www.arduino.cc/en/Reference/AnalogWrite) command reads or sends a range of values.[Example: if you want to read analog pin 0—which corresponds to pin A0 on the right side of Arduino, you would call analogRead(A0)]. Note that the analogWrite function has nothing to do with analog pins; it uses the PWM pins.
 
### 1. Potentiometer
Set up the LED output and potentiometer input circuits from the following schematic on your breadboard. This setup is much like the LED fade, except now we're using analogRead to control the fade.
 

[Peek at the breadboard photos.]

The potentiometer is an instance of a voltage divider circuit, which we discussed in class. As you might recall:
[insert circuit schematic]
 
> Now, try the code in File->Examples->Analog->AnalogInput. 
 
Change the code so that the LED fades and brightens with the analog value of the potentiometer, like a dimmer. (Save this code! We'll be using it again soon...)
 
**a. Post a copy of your new code in your lab writeup.**

Incorporate the LCD into your fading LED/potentiometer code so that you can read out the exact analog value that you are reading in on Analog Pin 0. It's your own lowly multimeter! Change the LED fading code values so that you get the full range of output voltages from using your Flex sensor.

**b. Include a copy of your Lowly Multimeter code in your lab write-up.**
 
### 2. Force Sensitive Sensor

The [FSR](http://en.wikipedia.org/wiki/Force-Sensing_Resistor) changes resistance—in this case, when pressure is applied to the FSR. Here's the [datasheet](http://www.sparkfun.com/datasheets/Sensors/Pressure/fsrguide.pdf). We'll use a voltage divider with a 27kOhm resistor, using the analog input with the previous potentiometer code.

[insert schematic]
 
Now borrow a FSR from a fellow student to build two FSR circuits to enable a game of thumb wrestling. Use the LCD to indicate who is squeezing their FSR harder!
 
**a. What resistance values do you see from your force sensor?**
**b. What kind of relationship does the resistance have as a function of force applied? (e.g., linear?)**
**c. Include a copy of your FSR thumb wrestling code in your lab write-up.**

## Part D. Timer

Make a timer that uses any of the input devices to set a time, and then automatically (or manually, if you prefer) begin counting down, displaying the time left. Make your timer beep, ring or sing when time is up! (Hint: the sample code for [Examples->LiquidCrystal->HelloWorld](https://www.arduino.cc/en/Tutorial/HelloWorld) displays the time in seconds since the Arduino was reset...)
 
Note that for some of you, the time may seem to be decrementing by 10 each second (that is, from 670=>660). Why is this? Do you think it's a hardware or software issue? Think about how 100 vs 99 is written to the screen, and ask an instructor
 
**a. Make a short video showing how your timer works, and what happens when time is up!**
**b. Post a link to the class Slack.**
 