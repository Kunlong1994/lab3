# Make a Digital Timer!
 
## Overview
For this assignment, you are going to 

A) [Solder your LCD panel](#part-a-solder-your-lcd-panel)

B) [Write text to an LCD Panel](#part-b-writing-to-the-lcd) 

c) [Using a time-based digital sensor!](#part-c-using-a-time-based-digital-sensor)

D) [Make your Arduino sing!](#part-d-make-your-arduino-sing)

E) [Make your own timer](#part-e-make-your-own-timer) 
 
## In The Report
Include your responses to the bold questions on your own fork of [this lab report template](https://github.com/FAR-Lab/IDD-Fa18-Lab2). Include snippets of code that explain what you did. Deliverables are due next Tuesday. Post your lab reports as README.md pages on your GitHub, and post a link to that on your main class hub page.

## Part A. Solder your LCD panel

You'll need to attach the header pins that came with your LCD character panel to your actual panel. Easiest is to insert the short end of the header pins into the back of the LCD panel, so that the long pins stick out the back and you can insert your LCD panel into a breadboard for easy use.

**If you have never soldered before, we're happy to show you how! PLEASE ASK!!**

## Part B. Writing to the LCD
Let's use your LCD screen to display some interesting information! There is a good deal of example code for playing with your LCD in the Arduino Examples:
 
`File->Examples->LiquidCrystal`
 
Let's start with the "Display" program, which just flashes "Hello World!" These LCDs are a custom part, but there's a lot of information at [this](https://www.adafruit.com/product/181) page, the [pinout and dimensions](https://cdn-shop.adafruit.com/product-files/181/p181.pdf) page and the [LCD controller](https://www.adafruit.com/datasheets/HD44780.pdf) page.
 
**a. What voltage level do you need to power your display?**

**b. What voltage level do you need to power the display backlight?**
 
![](https://cdn-shop.adafruit.com/1200x900/181-03.jpg)

Wire up your LCD according to the schematic below. If you didn't have our diagram, you would use the data sheets for the LCD and follow the comments in the "Display" code to figure out how to wire it up. 

[[images/lcd_arduino_schematic.png]]
 
**Be very careful not to connect Pin 1 to Pin 2 on the LCD**, as this can **destroy** your Arduino. Check the connections for a short between power and ground before you plug in power or the USB cable.
 
See [Tutorial](http://www.arduino.cc/en/Tutorial/LiquidCrystal) for more information. See [LCD Library](http://arduino.cc/en/Reference/LiquidCrystal) for the various functions you can use.

Try compiling and running the code. If it doesn't work the first time, check your pinouts...
 
The 10K pot connected to Vo on the LCD adjusts the contrast, so try adjusting that if your LCD won't turn on. The contrast might be so low that you're not able to see it, so make sure you've checked both extremes.
 
LCD pin 15 and 16 (LED+, LED-) are designed for background lighting. If you feel the whole screen too dark, you may try to connect pin15(LED+) to +3V or +3.3V and pin16(LED-) to ground. **Don't connect pin15(LED+) to +5V as it may burn background light!**
 
Do try to set this up before peeking at this [diagram](images/lcd_arduino_diagram.png).
  
**c. What was one mistake you made when wiring up the display? How did you fix it?**

**d. What line of code do you need to change to make it flash your name instead of "Hello World"?**
 
Try a few of the other examples in the folder to get a feel for the capabilities of your LCD. There is a list of all the possible functions at the [Arduino LiquidCrystal Library](http://arduino.cc/en/Reference/LiquidCrystal?from=Tutorial.LCDLibrary).

Incorporate the LCD into your fading LED/potentiometer code so that you can read out the exact analog value that you are reading in on Analog Pin 0. It's your own lowly multimeter!

**e. Include a copy of your Lowly Multimeter code in your lab write-up.**

<!-- Now build a circuit with two FSR sensors (one from your self and one borrowed from a fellow student) to enable a game of thumb wrestling. Use the LCD to indicate who is squeezing their FSR harder!

**f. Include a copy of your FSR thumb wrestling code in your lab write-up.** -->

Leave your LCD set up for the rest of Lab, and leave it set up when you finish Lab, as we'll use the display again next week.



## Part C. Using a time-based digital sensor

![Rotary Encoder](https://cdn-shop.adafruit.com/1200x900/377-02.jpg)
We have a high-quality 24 pulse encoder with knob and nice, click-y rotation detents.
 
[Product Page](https://www.adafruit.com/product/377)
[Datasheet](https://cdn-shop.adafruit.com/datasheets/pec11.pdf)
 
Like a potentiometer, a rotary encoder has 3 pins; unlike a potentiometer, an encoder can be spun round and round without stop. Rotary encoders use [quadrature](http://en.wikipedia.org/wiki/Rotary_encoder) to tell how fast and in which direction you are turning a knob. To connect the encoder to your breadboard, you can insert three pins directly into motherboard like picture below.
 
The circuit below is the "correct" way of hooking up a rotary encoder with your Arduino; the resistors and capacitors help to filter out noise from the mechanical operation of the encoder - this circuit diagram is from the datasheet.

[[https://ccrma.stanford.edu/wiki/images/c/c1/Encoder_filter.png]]
 
However, to _actually_ hook up your encoder, just use the 3-pin side. Hook the middle to ground, and the "A" and "B" pins to digital pins 2 and 3 of your Arduino.
 
What is going on in this circuit? The Phase A and Phase B pins actually behave like switches, so the pins have pull-ups so that they will be high by default, until they are pulled low by the encoder (your Arduino actually uses its own internal pull-ups). The resistor and capacitor combo also forms a low-pass circuit to eliminate stray voltage spikes that might occur from the quick switching (this is called "debouncing"). You can use any capacitor that is up to an order of magnitude away from the 10nF value.
 
Use [this rotary encoder code](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Rotary-Encoder-test-Code) to see if you have hooked the encoder up correctly! You should see data coming in on the serial monitor -- which you can open by clicking on the magnifying glass icon in the upper-right corner of the Arduino window (or by going to `Tools` > `Serial Monitor` in the menu).

## Part D. Make your Arduino sing!

Let's make the Arduino make some noise! We are going to start with the Tone example program:
 
`Examples->Digital->toneMelody`

The official Arduino tutorial for this code is [here](https://www.arduino.cc/en/Tutorial/ToneMelody?from=Tutorial.Tone)
Add a 75 Ohm resistor to limit the current to the speaker when you hook it up on your breadboard. If you would like it a little louder, you can use a lower value resistor, up to a minimum of 5 Ohms.

Wire it to your circuit with the black to ground and the red to Arduino Micro pin 8. 

**a. How would you change the code to make the song play twice as fast?**
 
Now change the speed back, and replace the melody[] and noteDurations[] arrays with the following:
```c++

int melody[] = {
  NOTE_D3,NOTE_D3,NOTE_D3,NOTE_G3,NOTE_D4,NOTE_C4,NOTE_B3,NOTE_A3,NOTE_G4,NOTE_D4, \
  NOTE_C4,NOTE_B3,NOTE_A3,NOTE_G4,NOTE_D4,NOTE_C4,NOTE_B3,NOTE_C4,NOTE_A3,0};
 
int noteDurations[] = {
  10,10,10,2,2,10,10,10,2,4, \
  10,10,10,2,4,10,10,10,2,4};
 ```
You'll also have to increase the for() loop index max from 8 to 20:
 ```c++
  for (int thisNote = 0; thisNote < 20; thisNote++) {
 ```
**b. What song is playing?**
 
## Part E. Make your own timer

Make a timer that uses any of the input devices to set a time, and then automatically (or manually, if you prefer) begin counting down, displaying the time left. Make your timer show an alert once the time is up with one of the output devices we connected during this lab, or you have available. (Hint: the sample code for [Examples->LiquidCrystal->HelloWorld](https://www.arduino.cc/en/Tutorial/HelloWorld) displays the time in seconds since the Arduino was reset...)

You should be able to draw upon awesome ideas you generated for the PreLab. 
 
Note that for some of you, the time may seem to be decremented by 10 each second (that is, from 670=>660). Why is this? Do you think it's a hardware or software issue? Think about how 100 vs. 99 is written to the screen, and ask an instructor.

**a. Make a short video showing how your timer works, and what happens when time is up!**

**b. Post a link to the completed lab report your GitHub repo.**