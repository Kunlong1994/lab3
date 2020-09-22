

## In the Report

For the report, use a copy of this page of the README.md in the directory for this lab in your own repository. You can delete everything but the headers and the sections between the stars. Write the answers to the questions under the starred sentences. Include code that you wrote.

Deliverables are due next Tuesday. Post a link to the wiki page on your main class hub page.


## Part A. Actuating DC motors



## Part B. Actuating Servo motors


### Part 1. Connect the Servo to your breadboard



**a. Which color wires correspond to power, ground and signal?**
red to power
yellow to signal
brown to ground


### Part 2. Connect the Servo to your Arduino



**a. Which Arduino pin should the signal line of the servo be attached to?**
9 (10 or 11 also works)

**b. What aspects of the Servo code control angle or speed?**
 for (pos = 0; pos <= 180; pos += 3)
    // in steps of 1 degree
    myservo.write(pos);             
    delay(15);                      
  }
  for (pos = 180; pos >= 0; pos -= 1)
    myservo.write(pos);             
    delay(15);   
    pos += 3 controls speed by step angle,  delay(15)controls by step time
    pos <= 180  and pos >= 0 controls angle
## Part C. Integrating input and output
   /* Sweep
    by BARRAGAN <http://barraganstudio.com>
    This example code is in the public domain.

    modified 8 Nov 2013
    by Scott Fitzgerald
    http://www.arduino.cc/en/Tutorial/Sweep
   */

   #include <Servo.h>

   Servo myservo;  // create servo object to control a servo
   // twelve servo objects can be created on most boards

   int pos = 0;    // variable to store the servo position

   void setup() {
     myservo.attach(9);  // attaches the servo on pin 9 to the servo object
   }

   void loop() {
     for (pos = 0; pos <= 180; pos += 3) { // goes from 0 degrees to 180 degrees
       // in steps of 1 degree
       myservo.write(pos);              // tell servo to go to position in variable 'pos'
       delay(15);                       // waits 15ms for the servo to reach the position
     }
     for (pos = 180; pos >= 0; pos -= 1) { // goes from 180 degrees to 0 degrees
       myservo.write(pos);              // tell servo to go to position in variable 'pos'
       delay(10);                       // waits 15ms for the servo to reach the position
     }
     for (pos = 0; pos >= 90; pos -= 3) { // goes from 180 degrees to 0 degrees
       myservo.write(pos);              // tell servo to go to position in variable 'pos'
       delay(8);                       // waits 15ms for the servo to reach the position
     }
     for (pos = 90; pos >= 90; pos -= 1) { // goes from 180 degrees to 0 degrees
       myservo.write(pos);              // tell servo to go to position in variable 'pos'
       delay(6);                       // waits 15ms for the servo to reach the position
     }
   }
![DCmotors](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab3/customized%20servo%20movement.mp4)

## Part D. Autonomy!

I broke the servo motor by directing connect it to 9V battery by mistake, I will make it up as I got the new motor, but this is what it should look like

![DCmotors](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab3/Connect9V%20battery.jpg)


**Include a photo/movie of your autonomous device in action.**

## Part E. Paper display

What I have in mind is a stopwatch that could display time on a LCD screen
![DCmotors](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab3/stopwatch.jpg)

**a. Make a video of your paper display in action.**

## Part F. Make it your own

I broke the servo motor by directing connect it to 9V battery by mistake, I will make it up as I got the new motor

**a. Make a video of your final design in action.**
 
