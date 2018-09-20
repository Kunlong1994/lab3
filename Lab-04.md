# Paper Puppets

```
FYI: This is a new lab we developed this year because 
last year's students wanted more exposure to motors and actuators. 
Please let us know what you think! Also, help us fish out any bugs...
```
## Overview
For this assignment, you are going to 

A) [Actuating DC Motors](#part-a-actuating-dc-motors) 

B) [Actuating Servo Motors](#part-b-actuating-servo-motors) 

C) [Integrating Input and Output](#part-c-integrating-input-and-output)

D) [Paper Puppet](#part-d-paper-puppet) 

E) [Make it your own](#part-e-make-it-your-own)



The physical housing and mechanisms of interactive devices are as important as the electronic components or the microcontroller code! They are the interface for the raw parts to users and the rest of the world. In this lab, we will learn to use some actuators, and then design Arduino-controlled puppets.

This lab is inspired by Google's [Paper Signals](https://papersignals.withgoogle.com) project. For now, we will be using the paper displays to make paper puppets controlled by the Arduino, but you are welcome to revisit the "voice control" part later in the quarter with the Raspberry Pi. 

![](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/raw/docs/wave.gif)
## In the Report

To submit your lab, clone [this repository](https://github.com/FAR-Lab/IDD-Fa18-Lab4). You'll need to describe your design, include a video of your paper display in operation, and upload any code you wrote to make it move.


## Part A. Actuating DC motors


Your kit has a vibration motor. Vibration motors are actually DC motors that have an asymmetrical weight on the main rotor, which causes the device to shake when power is applied and the motor rotates. 

![image of vibration motor](https://cdn-shop.adafruit.com/145x109/1201-01.jpg)

Use the [Fade](https://www.arduino.cc/en/tutorial/fade) circuit from Lab 01 (```Examples > 01 Basics > Fade```) and connect the vibration motor to the pin which normally would be supplying a LED with PWM'd voltage. (Remember PWM from Lab 1, Part E? [Pulse width modulation](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-01#part-e-fade-a-led-using-arduino) )  SECURE THE MOTOR TO KEEP IT FROM SHAKING ITSELF OUT OF THE CIRCUIT!

## Part B. Actuating Servo motors
![Image of servo motor](https://cdn-shop.adafruit.com/145x109/169-06.jpg)

A servo is a DC motor, geartrain, potentiometer and feedback circuit, all in a single housing.

By sending a PWM signal from your Arduino to the servo, you’re telling it what angular position you’d like it go to.

The potentiometer tells the feedback circuit the servo’s current position, and the circuit drives the motor to match the desired position.

### Part 1. Connect the Servo to your breadboard

Servo motors generally have 3 wires; power, ground and signal. [Here](https://www.adafruit.com/product/169) is the product page for the servos in your kit. 

**a. Which color wires correspond to power, ground and signal?**

Connect the servo to your breadboard, supplying power and ground to the appropriate pins. 

### Part 2. Connect the Servo to your Arduino

Now open the [Sweep](https://www.arduino.cc/en/Tutorial/Sweep) sketch in the Arduino IDE. 

```File > Examples > Servo > Sweep```

**a. Which Arduino pin should the signal line of the servo be attached to?**
Upload the sketch to the Arduino. Your servo should start sweeping back and forth, by about 180 degrees.

Change some parameters in the sketch to make the servo sweep slower, or over a smaller angle.

**b. What aspects of the Servo code control angle or speed?**

## Part C. Integrating input and output

Using what you've learned already, write code to control the servo motor circuit, either:
* adjusting the servo motor rotation to reflect the reading on a potentiometer voltage divider circuit, (Yes, it is fine to use any other analog voltage sensor!), or, 
* reflecting pre-programmed actions you design. 

**Include a photo/movie of your raw circuit in action.**

## Part D. Paper puppet

![](https://papersignals.withgoogle.com/static/images/instructions/slides/stretch_00011.png)

Use the [Stretch paper templates](https://papersignals.withgoogle.com/static/files/stretch.pdf) from the Google Paper Signals project. [Here are instructions to put these together](https://papersignals.withgoogle.com/getstarted#put-it-all-together) (make sure to choose the instructions for the STRETCH signal you're building) with the Arduino and the microservo.

**a. Make a video of your proto puppet.**

## Part E. Make it your own

Now modify this set up to make this your own design. You can use a different paper template, you can set the design in a particular setting, you can enact a mini puppet show. If your design involves having someone controlling the puppet in real time, please film that happening. Otherwise, film the puppet performing it's moves. 

**a. Make a video of your final design.**
 