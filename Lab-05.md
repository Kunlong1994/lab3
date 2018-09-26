# Useless box

For this week’s lab, we will be building a useless box; this is a project inspired by [Make Magazine](https://makezine.com/projects/the-most-useless-machine/) and a [similar lab](https://web.stanford.edu/class/engr40m/labs/lab2a.pdf) at Stanford's [ENGR40m](https://web.stanford.edu/class/engr40m/). We will use this lab to help you to experiment with digital fabrication tools. The methods that will be used are 3D printing and laser cutting.  

## 3D printing -- Andrea will edit these instructions

3D print this servo mount [include link]. Modify on OnShape to include your initials. 

1. Complete the first [Tinkercad](https://www.tinkercad.com/) tutorial. You’ll need to create an account.
1. Create a new project (outside the tutorial file) and make a cylinder 5mm tall and 6.9mm that you’ll use as your button.
1. Personalize the button to make it your own.
1. Export the object as a `.stl` file.
1. Download and install the [Makerbot Print](https://www.makerbot.com/print/)
1. Create a MakerBot account.
1. Start the Makerbot Print Application and log in.
1. Load the exported `.stl` button into the printer.
1. Connect your laptop to the printer over USB.
1. Once the Printer is connected hit "print".
1. After the printer has started the USB cable can be disconnected from your laptop.

## Laser cutting -- Andrea will edit these instructions

Laser cut this box in the Maker Lab[include link to ai file]--before printing, modify the file to have a hole for the switch, and draw parts that will work as the finger. 


1. Make sure you have followed the safety instructions from Niti.
2. Download a vector editing program like [Inkscape](https://inkscape.org/en/) (free) or [Adobe Illustrator](https://www.adobe.com/products/illustrator.html) (free for 30 day trial).
3. Download the laser cutter template file for the [CameraButtonStand](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/master/CameraButtonStand.svg).
4. Try to understand how these cuts lead to the 3D object.
[[images/lasercut-box.JPG|alt=Laser cut box with Andrea holding servo on 3D-printed mount on the moving side of the box. Where should the Arduino be mounted?]]
5. Personalize the stand to make it your own by adding vectors to the template file.
6. Save the file -> Move it to a USB drive. -> Connect the USB drive to the laser cutting computer.
7.  Open the file in Adobe Illustrator on the lab’s computer.
8.  Set the line-width to 0.001pt.
9.  Follow the instructions to cut:
    * Load the machine with 4-millimeter cardboard.
    * Disable X/Y.
    *  Move the laser to its starting position(top left corner of the material.
    *  Focus the laser. (Don't forget to put the focus tool up again!)
    *  Set home(button).
    *  Close the lid.
    *   Open the printer preferences.
    *   Make sure you set the different power levels for the normal cut and blue scoring-cut. See for values below.
    *   Turn on the air assist compressor on the floor and the suction system (big blue box).
    *   Print the job.
    *   Press 'go' on the laser cutter.

## Electronics --
Create this circuit. [Include diagram with switch, servo, 9V battery, and Arduino]. 
Bonus: use a prototoboard instead of a breadboard.

## Putting it all together --
Assemble your useless box. So that it works like this: show video.

# LAB SUBMISSION (Due before the lecture on Tue: 2/27/2018):
Post your files to GitHub. Make sure to include at least one video of your final object. Consider using the lightbox in the MakerLab to take high-quality product footage and images.
[[images/lightBox.jpg|alt=Image of a light box used to make evenly lit pictures of products and designs.]]  
Post a link to your GitHub submission on your Slack channel with your photo, cross post to the #lab3 channel, and tag the TAs with questions/requests for feedback.

---
General resources:
* [Reference sheets](reference_sheets/)
* [MakerLab Master document](https://docs.google.com/document/d/1ozET_Qy7wzQgwnNVcyp3mp056LdwB8jiCJiZLjYnwcU/edit)
* [MakerLab spring schedule](https://docs.google.com/document/d/15j1kPK74rHL6tj_sHqOJCFg3vdi1BD75TXnQPZ1bJaI/edit)
* For anyone who had trouble with the programming assignments from last weeks. You can use the following weeks to catch up with these [handy resources](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Programming-introduction-materials).
---
Power settings for 5/32" thickness cardboard.

Cutting (Standard Black Lines):
    Speed: 45%
    Power: 70%
    Frequency: 500Hz

Scoring (Color code Blue Lines):
    Speed: 65%
    Power: 45%
    Frequency: 500Hz