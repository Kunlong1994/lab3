# Useless Box

For this week’s lab, we will be building a useless box; this is a project inspired by [Make Magazine](https://makezine.com/projects/the-most-useless-machine/), which you used as reference for the preLab, and a [similar lab](https://web.stanford.edu/class/engr40m/labs/lab2a.pdf) at Stanford's [ENGR40m](https://web.stanford.edu/class/engr40m/). We will use this lab to help you to experiment with digital fabrication tools. The methods that will be used are 3D printing and laser cutting.  

## 3D Printing

3D print this [servo mount](https://www.thingiverse.com/thing:1926568).

1. Export the object as a `.stl` file.
1. Download and install [Makerbot Print](https://www.makerbot.com/print/).
1. Create a MakerBot account.
1. Start the Makerbot Print Application and log in.
1. Load the exported `.stl` button into the printer.
1. Connect your laptop to the printer over USB.
1. Once the Printer is connected hit "print".
1. After the printer has started the USB cable can be disconnected from your laptop.

**An option for making the "finger":**
1. Create a free education [OnShape](https://www.onshape.com/products/education) account using your student email.
1. Do the [sketching tutorial](https://learn.onshape.com/courses/fundamentals-sketching) and [part design tutorial](https://learn.onshape.com/courses/fundamentals-part-design-using-part-studios) to learn the basics of Computer Aided Design (CAD) on OnShape.
1. Create a finger to 3D print.


## Laser Cutting

Laser cut cardboard to make your useless box in the Maker Lab. 

2. Download a vector editing program like [Inkscape](https://inkscape.org/en/) (free) or [Adobe Illustrator](https://www.adobe.com/products/illustrator.html) (free for 30 day trial).
3. Open the laser cutter template file for the [useless box](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/uselessbox.ai) in your vector editing program.
[[images/lasercut-box.JPG|alt=Laser cut box with Andrea holding servo on 3D-printed mount on the moving side of the box. Where should the Arduino be mounted?]]
5. Modify the vector drawing as you please. Make sure the all lines that you want the printer to recognize are 0.001pt thick and the proper color (black for cutting). Save your file. BONUS: experiment with etching.
7.  To laser cut, open your modified file in Adobe Illustrator on the lab’s computer.
9.  Keeping in mind Niti's safety instructions, follow the instructions to cut:
    * Load the machine with the 5/32" thick cardboard we provided. If the material is bent, tape the ends using duct tape to the sides of the printing bed to make it as flat as possible.
    * Disable X/Y.
    *  Move the laser to its starting position on top left corner of the material.
    *  Focus the laser using the focus tool and up and down arrows. Flip the focus tool up again after you're done.
    *  Press the set home button.
    *  Close the lid.
    *   Open the printer preferences.
    *   Make sure you set the different power levels for the cut values pertaining to the material you're using. For the cardboard we are providing, the values should be: Speed 45%, Power 70%, and Frequency: 500Hz.
    *   Turn on the air assist compressor on the floor on.
    *   Turn the suction system, the big blue box, on.
    *   Print the job on the computer.
    *   Find the job you're printing on the laser cutter, and press 'go'.
9.  Assemble the parts, once the configuration makes sense, hot glue them together. Tip: don't hot glue the part where you'll attach the servo until you've attached the servo!

**An option for making the "finger":**
Now that you know how to use the laser cutter, draw something on the vector software to use a the "finger" — there are a lot of cool scrap materials available on the scrap pile, like acrylics that will work well for this. Make sure to adjust the speed, power, and frequency settings for the material you decide to use.   

## Electronics --
Create this circuit. [Include diagram with switch, servo, 9V battery, and Arduino]. 
Bonus: use a prototoboard instead of a breadboard.

[[https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/docs/circuit_image_lab5.png]]

## Putting it All Together
Insert the electronics, install the mechanical components, glue anything that has not been glued yet, and test your useless box!

# Lab Submission
Write-up a **How To Make a Useless Box** guide for yourself to use in the future. Include at least one photo of your useless box taken in the MakerLab's Portable Photo Studio (or somewhere else, but of similar quality), and a video of your useless box in action.

[[images/lightBox.jpg|alt=Image of a light box used to make evenly lit pictures of products and designs.]]  

---
General resources:
* [Reference sheets](reference_sheets.zip)
* [MakerLab Master document](https://docs.google.com/document/d/1ozET_Qy7wzQgwnNVcyp3mp056LdwB8jiCJiZLjYnwcU/edit)
---