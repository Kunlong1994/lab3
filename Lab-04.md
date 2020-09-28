# Data Logger (and using cool sensors!)


## Overview



## Part A.  Writing to the Serial Monitor
 
![analogread](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab4/analogread.jpg)
 
**a. Based on the readings from the serial monitor, what is the range of the analog values being read?**
 
 0-1023
**b. How many bits of resolution does the analog to digital converter (ADC) on the Arduino have** (hint: where might you look to find this sort of thing)? How many are you using 

10
## Part B. RGB LED

https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab4/LEDtrial.mp4

**You should add the LEDs in the schematic below.**


## Part C. Resistance & Voltage Varying Sensors 

### FSR


**a. What voltage values do you see from your force sensor?**

0-4.95
**b. What kind of relationship does the voltage have as a function of the force applied? (e.g., linear?)**

linear relationship, as I press harder the voltage increase
**c. In `Examples->Basic->Fading` the RGB LED values range from 0-255. What do you have to do so that you get the full range of output voltages from the RGB LED when using your FSR to change the LED color?**

Use this code to transfer the 0-1023 range to 0-255: map(output, 0 ,1023, 0, 255);
## Flex Sensor, Photo cell, Softpot

**a. What resistance do you need to have in series to get a reasonable range of voltages from each sensor?**

About 10k
**b. What kind of relationship does the resistance have as a function of stimulus? (e.g., linear?)**

linear , but drops as I press it, so for resistance it's R = TotalR - k*(allied force)

## Part D. I2C Sensors 


### Accelerometer
 

 
**a. Include your accelerometer read-out code in your write-up.**

please cheak acceldemo0928

## Part E. Logging values to the EEPROM and reading them back
 
### 1. Reading and writing values to the Arduino EEPROM


**a. Does it matter what actions are assigned to which state? Why?**

Yes, the states happen in series
**b. Why is the code here all in the setup() functions and not in the loop() functions?**

Because the state is conducted in one loop for on time, the compiler would fail if there are more than one loop in a system 

**c. How many byte-sized data samples can you store on the Atmega328?**

1024bits
**d. How would you get analog data from the Arduino analog pins to be byte-sized? How about analog data from the I2C devices?**
 
 divide anlog data by 4 and eliminate the decimals. 
 For I2C devices, we need to map the imput signal range to 0-255.
 
**e. Alternately, how would we store the data if it were bigger than a byte? (hint: take a look at the [EEPROMPut](https://www.arduino.cc/en/Reference/EEPROMPut) example)**

If the data is larger than a byte we could use EEPROM.put to store it to consecutive addresses 

### 2. Design your logger

please check EEPROM0928

https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab4/EEPROM0928.ino
 
**a. Turn in a copy of your final state diagram.**

![state diagram](https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab4/statediagram.jpg)

## Part G. Create your own data logger!

It is a pressure controlled bedlight, I don't have light sensors in the kit otherwise it could be modified into lighr and human action sensor light

https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab4/PressureappliedLED.ino

https://github.com/Kunlong1994/-Interactive-Lab-Hub/blob/master/Lab4/PressureappliedLED.mp4
 
**a. Record and upload a short demo video of your logger in action.**
