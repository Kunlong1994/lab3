This is an experimental lab where you will make your own Arduino. It has never been tried before! Please help to build out the activity.

## In The Report
For the report, make a copy of this wiki page for your own repository, and then delete everything but the headers and the sections between the **stars**. Write the answers to the questions under the starred sentences. Include snippets of code that explain what you did.

Deliverables are due next Tuesday. Post a link to the wiki page on your main class hub page.
 
## Overview
For this assignment, you are going to 

A) [Design your Arduino+](#part-a-design-your-arduino) 

B) [Order parts for your Arduino+](#part-b-order-parts-for-your-arduino) 

C) [Prototype your Arduino+](#part-c-prototype-your-arduino)

D) [Layout your Arduino+](#part-d-layout-your-arduino) 

E) [Send your board off to be made](#part-e-send-your-board-off-to-be-made)


## Part A. Design your Arduino+

Think of a small (emphasis on small) improvement that can be made to the basic design of an Arduino. For example, you could make an Arduino with a real time clock. Or you could make an Arduino that was laid out in a different shaped board. Please keep your design to be an Arduino *plus one thing*. 

The questions below should help scaffold important considerations when you are making your design. The plan is for this week's lab to be about designing, laying out and sending out the board; if you need to order parts to prototype and test your design before sending out the board, please outline the expected plan.

Use [PCBShopper](https://pcbshopper.com) to look at the trade offs between different quick turn PCB fab shops in time, cost, number of boards, design constraints, etc. Depending on your design needs and risk tolerance, different companies might suit your needs better. 

Please document the design of your Arduino+:

**a) What is the + improvement of your Arduino+**

**b) What Arduino form-factor/design are you basing your design off of?**

**c) What features/parts need to be incorporated for your Arduino+? Include your research!**

**d) What is the timeline for the overall development of your Arduino?**

**e) Which fabrication company are you using, what do you plan to order, and what is the design rationale for the selection?**

## Part B. Order parts for your Arduino+

Develop a bill of materials for your Arduino +.

This is a spreadsheet/table to help you keep tabs on what parts you need to order to populate your board. [Here is an example of a BOM](http://solderpad.com/solderpad/arduino-uno/) for an Arduino Uno, from Solderpad.com. 

**Bill of Materials**
Use the table below, or just include a link to a spreadsheet or pdf.
| Part name | Part ID | Part description | # of units | link to data sheet | link to source | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Atmega 328P    |   U1 |   Microcontroller  |  1   |  [datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-7810-Automotive-Microcontrollers-ATmega328P_Datasheet.pdf)   |   [Amazon](https://www.amazon.com/dp/B004G51AMW)  |  Bootloader   |
|     |    |     |     |     |     |     |
|     |    |     |     |     |     |     |


## Part C. Prototype your Arduino+

As much as is possible, prototype the design of your Arduino +. This step may require time. For example, if you have to order breadboard able parts that you don't have on hand, you might have to order those and wait for them to arrive. On the other hand, for other aspects of your design, like layout, you might be able to use sketches to figure out how everything will fit together, or if it will be large enough or small enough for the application you have in mind. 

Sometimes you're just testing out design constraints. For example, if you are making an Arduino + speaker to be a musical dog collar for your pet, you can see how heavy a collar your dog will tolerate by making a dummy board and case.

**Describe key design questions (how big are the parts? what pins need to be connected?) and how you used/will use prototyping to answer them.**

## Part D. Layout your Arduino+

Use EAGLE, KiCAD, Fritzing or the ECAD program of your choice to layout your Arduino +. The source files for the existing Arduino designs is available from Arduino.cc. For example, [here is the page](https://store.arduino.cc/usa/arduino-uno-rev3) with the open source designs for the Arduino UNO R3. 

**Document what you files, with enough specificity that anyone else could have the same thing made.**

## Part E. Send your board off to be made

When you have laid out your board, send it off to be fabricated. You might need to order components, tools or other apparatus (like programmers or FTDI interfaces) to complete the design at this time too.

**Document what you sent, and to where, with enough specificity that anyone else could have the same thing made.**

**In the report, please tell us any pain points you faced in this lab, and how we could make this process easier for future students.**