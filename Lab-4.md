Make a Digital Timer!
 
Overview
For this assignment, you are going to 1) make sounds with your Arduino, 2) write to a text LCD panel, 3) explore cool inputs, and 4) make your very own timer.
 
In The Report
Include your responses to the green questions. Include snippets of code that explain what you did, and please follow the Lab Report Guidelines. Deliverables are due next Tuesday. Post your lab reports as 'wiki' pages on your GitHub, and post the link to Slack under your own channel and #Lab4.

 
Part A. Making Sounds
Remember that greeting card project dissection we did during the first lecture? Let's make the Arduino make some noise! We are going to start with the Tone example program:
 
Examples->Digital->toneMelody
 
A nice tutorial for this code is [here](https://www.arduino.cc/en/Tutorial/ToneMelody?from=Tutorial.Tone).
 
Solder jumper wires to the leads on the back of the speaker. Add a 75 Ohm resistor to limit the current to the speaker when you hook it up on your breadboard. If you would like it a little louder, you can use a lower value resistor, up to a minimum of 5 Ohms.


 

 
And a circuit diagram:

 
Wire it to your circuit with the black to ground and the red to Arduino Micro pin 8. By now, you should be able to wire circuits up from an electrical schematic without looking at a physical breadboard picture. In future labs, we won't give a breadboard photo. For this lab, we link photos for circuit diagram.  
 
Try out the program!
 
a. How would you change the code to make the song play twice as fast?
 
Now change the speed back, and replace the melody[] and noteDurations[] arrays with the following:
 
int melody[] = {
  NOTE_D3,NOTE_D3,NOTE_D3,NOTE_G3,NOTE_D4,NOTE_C4,NOTE_B3,NOTE_A3,NOTE_G4,NOTE_D4, \
  NOTE_C4,NOTE_B3,NOTE_A3,NOTE_G4,NOTE_D4,NOTE_C4,NOTE_B3,NOTE_C4,NOTE_A3,0};
 
int noteDurations[] = {
  10,10,10,2,2,10,10,10,2,4, \
  10,10,10,2,4,10,10,10,2,4};
 
You'll also have to increase the for() loop index max from 8 to 20:
 
  for (int thisNote = 0; thisNote < 20; thisNote++) {
 
b. What song is playing? ;-)
 

Part B. Writing to the LCD
Let's use your LCD screen to display some interesting information! There is a good deal of example code for playing with your LCD in the Arduino Examples:
 
File->Examples->LiquidCrystal
 
Let's start with the "Display" program, which just flashes "Hello World!" This summer's LCDs are a custom part, but there's a lot of information at Standard LED (16*2, model: LCM1602A-NSW-BBW)  page, the pinout and dimensions page and the LCD controller page.
 
a. What voltage level do you need to power your display?
 
Solder a 16 pin breakaway header to the LCD so you can connect it to your breadboard. You can find these in the part shelf labelled 'Breakaway Headers Male.'
 

Wire up your LCD according to the schematic below. If you didn't have our diagram, you would use the data sheets for the LCD and follow the comments in the "Display" code to figure out how to wire it up. 
 
**Be very careful not to connect together Pin 1 and Pin 2 on the LCD**, as this can **destroy** your Arduino. Check for a short between power and ground before you plug in power or the USB cable.


 
See Tutorial for more information. See LCD Library for the various functions you can use.
 
The 10K pot connected to Vo on the LCD adjusts the contrast, so try adjusting that if your LCD won't turn on. If it's still not working, try to disconnect your speaker from part A—and check your wiring.
 
LCD pin 15 and 16 (LED+, LED-) are designed for background lighting. If you feel the whole screen too dark, you may try connect pin15(LED+) to +3V or +3.3V and pin16(LED-) to ground. Don't connect pin15(LED+) to +5V as it may burn background light!
 
This is the last lab where we'll show images of the circuits you need to build with the schematics, so do try to set this up before peeking at this photo.
 
Try compiling and running the code. If it doesn't work the first time, check your pinouts...
 
b. What was one mistake you made when wiring up the display? How did you fix it?
c. What line of code do you need to change to make it flash your name instead of "Hello World"?
 
Try a few of the other examples in the folder to get a feel for the capabilities of your LCD. There is a list of all the possible functions at the Arduino LiquidCrystal Library.
 
Leave your LCD set up for Part C and D of the Lab, and leave it set up when you finish Lab, as we'll use the display again next week.
 
Part C. Fancy Inputs
In Lab 1, you used a potentiometer to control the brightness of LEDs. Now let's do that again, but with the Arduino in the mix.
 
First, it's important for you to understand that analog input ("analog pin 0") on your Arduino board shares pins with digital input. Below is pinout for Arduino Micro.  The pins with name A0-A12 are analog pins. 
 

 
So while a digitalRead or digitalWrite command reads or sends only a logic-level high or low, an analogRead or analogWrite command reads or sends a range of values. Nice! [Example: if you want to read analog pin 0—which corresponds to pin A0 on the right side of Arduino, you would call analogRead(A0)]. Note that the analogWrite function has nothing to do with analog pins; it uses the PWM pins.
 
1. Potentiometer
Set up the LED output and potentiometer input circuits from the following schematic on your breadboard. This setup is much like lab 2's LED fade, except now we're using analogRead to control the fade.
 

[Peek at the breadboard photos.]
 
Now, try the code in File->Examples->Analog->AnalogInput. 
 
Drawing on your Lab 1 work, change the code so that the LED fades and brightens with the analog value of the potentiometer, like a dimmer. (Save this code! We'll be using it again soon...)
 
a. Post a copy of your new code in your lab writeup.
 
2. Flex Sensor

The potentiometer is an instance of a voltage divider circuit, which we discussed in class. As you might recall:

The Flex sensor changes resistance between 8k-10k Ohms (straight) and 20k-50k Ohms (bent). The datasheet is here. Note that the datasheet states they should be 10k Ohms straight and 60-110k Ohms while bent ±30%. The change between the datasheet and the actual parts can be reflected as a result of either the parts aging (stressed by temperature/humidity), poor quality control, or different test conditions. We'll build a voltage divider circuit with a 27k resistor, using the flex sensor with the fading LED/potentiometer code from the last exercise:
 

Circuit Schematic for Flex sensor. Note: The schematic shows a 24k resistor but we will use a 27k for this lab.
 
[Peek at photos of the breadboard.]
 
a. What resistance do you see with a Multimeter when the sensor is flat? When it is bent?
b. What kind of voltages should we expect for the Arduino analog pin based on the sensor resistance?
c. How does the range of the LED's brightness change compared to the potentiometer?
 
Incorporate the LCD into your fading LED/potentiometer code so that you can read out the exact analog value that you are reading in on Analog Pin 0. It's your own lowly multimeter! Change the LED fading code values so that you get the full range of output voltages from using your Flex sensor.
 
d. Include a copy of your Lowly Multimeter code in your lab write-up.
 
3. Force Sensitive Resistor

Just like the Flex sensor, the FSR changes resistance—in this case, when pressure is applied to the FSR. Here's the datasheet. We can reuse the same circuit as before. (It's okay to remove the LED, though.)
 
Now build two FSR circuits to enable a game of thumb wrestling. Take another FSR from the parts shelf, but be sure to return it when done! (We don't have enough for everyone to have 2). Use the LCD to indicate who is squeezing their FSR harder!
 
a. What resistance values do you see from your force sensor?
b. What kind of relationship does the resistance have as a function of force applied? (e.g., linear?)
c. Include a copy of your FSR thumb wrestling code in your lab write-up.
 
Part D. Timer
Make a timer that uses your fancy inputs (or any other sensor that you want to try—check out Lab 4) to set a time, and then automatically (or manually, if you prefer) begins counting down, displaying the time left. Make your timer beep, ring or sing when time is up! (Hint: the sample code for Examples->LiquidCrystal->HelloWorld displays the time in seconds since the Arduino was reset...)
 
Note that for some of you, the time may seem to be decrementing by 10 each second (that is, from 670=>660). Why is this? Do you think it's a hardware of software issue? Think about how 100 vs 99 is written to the screen, and ask an instructor
 
a. Make a short video showing how your timer works, and what happens when time is up!
b. Post a link to the Lab 3 Timers Hall of Fame.
 