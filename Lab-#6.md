#Make an Etch-a-Sketch! 
 
##Overview
Let's get some hands-on experience with a graphical LCD and SD Cards for large storage. We'll then make an electronic Etch-a-Sketch.
 
##In The Report
Include your responses and uploads to the green questions. Include snippets of code that explain what you did. Embed a video demo of your data logger, and please follow the Lab Report Guidelines. Deliverables are due one week after your lab session. Post your lab reports as 'wiki' pages.
 
##Parts
Don't forget to collect the new parts for your kits by the printer!
 
###Part A. Graphical LCD
The datasheet for the controller on the LCD display is here. Graphical LCD needs to be powered at 3.3V, so we use a voltage shfiter (HEF 4050BP) attached with GLCD pakcage. You may find datasheet and pinout information for HEF 4050BP here.
 
1. Install the Graphical LCD libraries using Arduino's Sketch > Import Library > Add Library menu. It's already installed on the lab computer(s). 
2. Wire up the Graphical LCD like so. Note that the pin ordering is labelled on the bottom of the board, and that pin 1 is designated by a square pad. Also note that you only need to solder one row of headers of the LCD, not both. 
3. We use digital pin3 of Arduino to send reset signal to the LCD reset pin. However, since pin3 only outputs 5V, you will need to down-convert it to 3.3V, which is the voltage that the LCD works with. Here is a schematic of how you should design your voltage divider. Pick your own choice of R1 and R2 to make the voltage divider work. Credit to Kuilin for his contribution to this part of lab! 

 
 
Graphical LCD	 
Connection
1 - GND	 -->	GND
2 - VCC	  -->
3.3V
3 - CLK	  -->	4050 Pin 10
4 - DIN 	  -->	4050 Pin 12
5 - D/C	  -->	4050 Pin 15
6 - CS	  -->	GND
7 -  RST	  -->	Voltage Divider at 3.3V
8 - LED	  -->	3.3V (no pullup required)
 
Arduino Pin 3                                	  -->          	Voltage Divider at 5V                                                   
 
 
4050 	 
Connection 
Pin 1	   -->	3.3V
Pin 8	   -->
GND
Pin 9	   -->	Arduino D7
Pin 11	   -->	Arduino D6
Pin 14	   -->	Arduino D5
 
3. Try the code from Sketchbook->Strings (instruction for getting this sketch are here: Graphical LCD). Unlike your LCD (where the LCD controller controls the font rendering), the graphical lcd is controlled pixel by pixel, so that the Arduino Micro handles what the text will look like. (So you can get different fonts!). You may have to adjust the contrast.
 
Note: It is very likely that image is not showing right for the first uploading, press "reset" button on Arduino and see if it gets better. You can also try adding display.setContrast(50); after the display.begin() line. 
 
If you see a light image then your display is probably working, but something is funny. Power your board with an external power supply (Use the lab power supply and plug 5V into the 5V pin and ground into ground. Make sure not to put 5V into any components that want 3.3V or you might blow them). 
 
a. With the standard font, what is the longest message you can write across one line of the display? How many lines can you write?
 
4. Try the code from Sketchbook->GraphicsExample.
 
5. (OPTIONAL) Modify the code to display a logo for yourself (the screen is 84x48 pixels, though we have found that graphics at 64x48 work better). You can either use the graphical library's functions (to make circles, rectangles, etc), or you can use whatever program you like to create an approximately 84x48 monochrome bitmap file (.bmp), such as in MS Paint or the GIMP. You can also convert another image into a monochrome .bmp format suitable for our display. 
 
To convert it to C code (see the pony_bmp.h file in the example), you can follow this tutorial: LCD Assistant Convert .bmp or other images into a format suitable for display on our monochrome graphic LCD.
 
This software is Windows only. If you have a Mac with a Windows virtual machine, then use it there. If not, the lab PC will have the software.
 
Note: Be VERY careful about width and height of the figure you put into LCD Assistant as it only converts image but NEVER scale it.
 
It is very likely that image is not showing right for the first uploading, press "reset" button on Arduino and see if it gets better.
 
a. Upload a photo of your personal logo, shown on your LCD screen, to your Lab 5 page.
 
###Part B. microSD Card
The microSD card communicates with the Arduino Micro using SPI. We'll be using modified SD card adapters as microSD card readers.
 

  
1. Using the right-angle headers, solder 7 pins of single row headers onto the microSD adapter as shown so that we can use it as a cheap microSD card to protoboard adapter. Make sure that you don't short any adjacent pins, and note that the two outer-most pins are unused (don't solder anything to them.) Find the sheet of label stickers next to the printer, and cut out a label for your pins. Use the photo above to make sure you put the stickers on in the right direction! 
 
2. Set up communications with your Micro so that:
 
 microSD card	 
 Connection 
MISO	   -->	Arduino MISO (MI)
GND	   -->
GND
SCK
   -->
4050 Pin 2
3.3V+
   -->
3.3V
GND	   -->	GND
MOSI	   --> 	4050 Pin 4
CS	   --> 	4050 Pin 6
 
Retain your previous 4050 wiring, but add:
4050 	 
Arduino 
Pin 3	   -->	Arduino SCK
Pin 5
   -->
Arduino MOSI (MO)
Pin 7	   -->	Arduino SS
 
Double check your pin assignments, power and ground short, etc, and then connect your USB cable.
 
3. Use this code to read the datalog.txt file from the microSD card and print out the contents to the serial terminal.  
 
Modify the code to: (a) append "He who must not be named!" (or another suitable quote!) to the end of the file's current contents, and (b) print out the updated file to the serial terminal. You'll want to use some of the functions from the example code in the Examples->SD folder. This should only take about 3-5 lines of code.
 
You'll want to review these SD Library Functions.
 
a. Include the code that you had to insert to do this in your lab writeup. 
b. Explain what would you do differently to insert the same text string, but at the beginning of the file (without over-writing the current contents). You don't have to code this: just explain the process. If you're interested and have time make it work, show us your program.
c. Now tell us if your approach would work if the file were larger than your Arduino's memory (which is 2.5KB). If not, how could you work around that limitation?
 
4. Merge your code from Part A above and your code from step B3 to output data from the text file on the microSD card to your graphical LCD.
 
Note: Your fellow students have found that you have to init your SD card before your LCD in the setup function. 
 
a. Post your code.
 
5. Modify your data logger code from last lab so that you can write to the microSD card. If you took apart your data logger already, make the changes to your old code that you would need to make it write to the SD card.
 
a. Tell us what you had to change to make this work.
 
Part D. Create an Etch-a-Sketch!
Use any combination of input sensors and switches with the Graphical LCD  to create your own unique Etch a Sketch. You are welcome to make as liberal an interpretation of the Etch a Sketch concept as you like, as long as you:
 
- Allow a user to control the creation of a drawing
- Give users real-time feedback of what they're drawing
- Make it possible to clear a drawing
 
Optional: Make it possible to save a drawing.
Optional: Make it possible to recall a drawing after it has been cleared from the screen.
 
Note: Your fellow students have found that you have to init your SD card before your LCD in the setup function.
 
Hint: The Adafriut_PCD8544 library includes a variable, named nokia_5110_lcd, which is a buffer to store the LCD's entire screen. We've made this variable public, so you can use it. Just so you know what it looks like, here's its library definition:
 
#define LCDWIDTH  84
#define LCDHEIGHT 48
 
class Adafruit_PCD8544 : public Adafruit_GFX {
public:
...
uint8_t pcd8544_buffer[LCDWIDTH * LCDHEIGHT / 8];
 
By the way, the cryptic "uint8_t" data type is just a C/C++ way of defining (exactly) an unsigned 8 bit integer. You can copy the contents of the screen buffer to a file just by saving the pcd_8544_buffer variable, like this:
 
myFile.write(display.pcd8544_buffer, 504);
 
You can then read the data back from the file, and restore the screen buffer, like this:
 
myFile.readBytes((char *)display.pcd8544_buffer, 504);
 
a. Upload video of your Etch-a-Sketch in action!
b. Post a link to the Lab 5 Etch-a-Sketch Hall of Fame.
 
The best Etch-a-Sketch wins a $10 gift certificate at Sparkfun. This is the last chance for swag...