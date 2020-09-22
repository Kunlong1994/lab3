

## In the Report

For the report, use a copy of this page of the README.md in the directory for this lab in your own repository. You can delete everything but the headers and the sections between the stars. Write the answers to the questions under the starred sentences. Include code that you wrote.

Deliverables are due next Tuesday. Post a link to the wiki page on your main class hub page.


## Part A. Actuating DC motors
![DCmotor](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab3/DCmotor.jpg)


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
 
 
![Customizedservo](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab3/customized%20servo%20movement.mp4)

## Part D. Autonomy!

I broke the servo motor by directing connect it to 9V battery by mistake, I will make it up as I got the new motor, but this is what it should look like

![Autonomy](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab3/Connect9V%20battery.jpg)


**Include a photo/movie of your autonomous device in action.**

## Part E. Paper display

What I have in mind is a stopwatch that could display time on a LCD screen
![Paperdisplay](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab3/stopwatch.jpg)

**a. Make a video of your paper display in action.**

## Part F. Make it your own

I broke the servo motor by directing connect it to 9V battery by mistake, I will make it up as I got the new motor

**a. Make a video of your final design in action.**
 
