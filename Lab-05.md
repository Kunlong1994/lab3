# Jack in the Box

***

For this week’s lab, we will be building a Jack in the box; this is a project inspired by the known toy. We will use this lab to help you to experiment with digital fabrication tools. The methods that will be used are 3D printing and laser cutting.
[Video of similar box](https://www.youtube.com/watch?v=Z70TRaKqUbs)

## In the report
To submit your lab, clone this repository -- and include all files / images / code that is requested!

## Laser Cutting
Laser cut cardboard to make your box in the Maker Lab.
1.	Download a vector editing program like [Inkscape](https://inkscape.org) (free) or [Adobe Illustrator](https://www.adobe.com/products/illustrator.html) (free for 30 day trial).
4.	On [this page](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/tree/2019Fall/Lab5), download the PDF (boxTall.pdf) and the STL files.
2.	Open the laser cutter template file (PDF) for the Box in your vector editing program (i.e. Ink scape).
3.	Add holes for the servo mount, and Arduino wires. This time, make sure you don't use images, but instead vectors. Make sure the all lines that you want the printer to recognize are 0.001pt thick and the proper color (red= 255, green= 0, blue =0) for cutting. Also make sure that the page size is the same size as your cardboard (or you will have to change the home on the laser cutter). Save your file as a PDF. BONUS: include lines or images that you don't plan to cut all the way through to experiment with etching.
4.	To laser cut, open your modified file in Adobe Illustrator on the lab’s computer. Look around the laser cutting room for instructions, reference sheets, and scrap materials. The step by step instructions are attached on the suction system to the left of the computer.
5.	Keeping in mind Niti's safety instructions, follow the instructions to cut (these are summarized for our purposes):
* 	Load the machine with the 5/32" thick cardboard we provided. If the material is bent, tape the ends using duct tape to the sides of the printing bed to make it as flat as possible.
* 	Disable X/Y.
* 	Move the laser to its starting position on top left corner of the material.
* 	Focus the laser using the focus tool and up and down arrows. Flip the focus tool up again after you're done.
* 	Press the set home button.
* 	Close the lid.
* 	Open the printer preferences.
* 	Make sure you set the different power levels for the cut values pertaining to the material you're using. 

For the cardboard we are providing, the values should be: Speed 45%, Power 70%, and Frequency: 500Hz. On the same window, adjust the printing bed size to 24" horizontal, and 18" vertical. When you save the settings, make sure the image on the preview is well positioned (not too close to the edges and fitting well in the space). Under Page Sizing and Handling, click actual size. Press print.
*	Turn on the air assist compressor on the floor on.
*	Turn the suction system, the big blue box, on.
*	Print the job on the computer.
*	Find the job you're printing on the laser cutter, and press 'go'.

6.	Assemble the parts. Make sure the holes for the servo mount, and Arduino wires fit. Once the configuration makes sense, hot glue them together. Pay attention that part “D” is the top of the box and should not be hot glued- you can attach it with tape or or some other hinge.

Notice that part G is not part of the Box itself. It will be used as the top lifter.

![Picture1](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/2019Fall/BOX%20diagram.png)

## 3D Printing

3D print [this servo mount](https://www.thingiverse.com/thing:1926568):
1.	Download and install [Ultimaker Cura](https://ultimaker.com/software/ultimaker-cura).
2.	Import the .stl file from the files you downloaded into the printer software.
3.	Make sure the orientation of your part makes sense. What orientation makes the most sense for 3D printing?
4.	Turn off the raft. There is no need to print a raft for this part.
5.	Connect your laptop to the printer over USB, or via WiFi. Ask any member of the teaching team for WiFi credentials.
6.	Once the Printer is connected hit "print".


## Electronics

![electronics circuit](https://user-images.githubusercontent.com/54110697/64988326-35758180-d899-11e9-9473-b1610101d91b.jpg)

Tip: If you don't have the 9V connector, you just need to make sure that the micro controller is plugged into your computer, for power. 

### Program your device

Load the [example](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/2019Fall/Lab5/JackInABox.ino) previously downloaded.

You can also make your own program but make sure you put HIGH digital value to pin 5 if you connected the circuit as the one in the electronics part.

Pay attention that you can change the position of close and open box in the following lines:

#define closePos  10

#define openPos   110


## Putting it all together
***
Think about where each component should go, and assemble your box so it would work as the one in the video from the beginning.

## Create Jack

To make the character in the box a 3D printed part:
1.	Create a free education [OnShape](https://www.onshape.com/products/education) account using your student email.
2.	Do the [sketching tutorial](https://learn.onshape.com/courses/fundamentals-sketching) and [part design tutorial](https://learn.onshape.com/courses/fundamentals-part-design-using-part-studios) to learn the basics of Computer Aided Design (CAD) on OnShape.
3.	Create a character to 3D print.

To make the character in the box a laser cut part:
1.	Create a free education [OnShape](https://www.onshape.com/products/education) account using your student email.
2.	Do the [sketching tutorial](https://learn.onshape.com/courses/fundamentals-sketching) and [part design tutorial](https://learn.onshape.com/courses/fundamentals-part-design-using-part-studios) to learn the basics of Computer Aided Design (CAD) on OnShape.
3.	Create a 3D character
4. Use the KiriMoto app from the OnShape app store (it’s free to edu users) to slice the shape into laser cuttable parts.

## Lab Submission
***
For your write up, include:
1.	Your Arduino code.
2.	.stl or .svg files for your Jack — if you use some other technique, include the respective supporting material.
3.	At least one photo of your box taken in the MakerLab's Portable Photo Studio (or somewhere else, but of similar quality).

4.	A video of your box in action.

