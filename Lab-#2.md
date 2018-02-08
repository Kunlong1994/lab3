In this Lab, we will use the Interaction Engine for an interactive webcam application.

## Overview
1. Set up Arduino connection
* Connect Arduino
* Flash sample `Blink.ino` program.
* Check that Arduino is running program.
2. HelloYou test
* Flash helloYou firmware to Arduino.
* Run the node program.
* Test the functionality with a remote browser.
3. Distant Pictures 
* [Fork](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Forking-a-GitHub-project) the [distant-picture](https://github.com/FAR-Lab/distant-pictures) example project.
* Plug the webcam into the Pi.
* Run the node program.
* Test the functionality with the remote browser.
4. Make your own variation on this lab assignment: [Change the behavior](#change-the-interaction) of the interaction. 

## Detailed steps

1. Set up Arduino connection
* You will need to power the Raspberry Pi with the AC adapter because you will need the USB cable from the class kit to connect the Pi to the Arduino.
* Physically connect Arduino to the Pi using the USB cable.

<img src="https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/images/pi+arduino.JPG" width="400px">

* Flash the sample `Blink.ino` program to make sure the connection to the Arduino is sound. _(We will go into more detail on how to program the Arduino, compile code, etc. in the next lab.)_
  * Login into your Raspberry Pi.
  * In the `~/sketchbook/blink` directory, type `make upload` to flash the pre-compiled `Blink.ino` code to the Arduino
```
pi@ixeXX:~ $ cd sketchbook/blink
pi@ixeXX:~/sketchbook/blink $ ls
blink.ino  build-uno  makefile
pi@ixeXX:~/sketchbook/blink $ make upload
```
 The Arduino LEDs should flash rapidly while the code is being flashed onto the Arduino, and then the red onboard LED should blink on and off at a 10 Hz rate.
  * Problems? Try [checking the port assigned to the Arduino.](#check-port-of-arduino-board).
  * Curious how things work? Try [looking at the `Blink.ino` code] <--david, need you to add

2. HelloYou test

We have demonstrated this example in class. We will have a button connected to an Arduino attached to the IxE via a USB cable change the background color of our webpage. Then we can use a button on the webpage to turn an LED on the Arduino on and off.
* Set up the Arduino button circuit (We will also go deeper into the electronics in the next lab.)
On your breadboard, make this [basic button circuit](#basic-button-circuit) connected to `pin 2` of the Arduino. (The LED is built in on the board and connected to `pin 13`.)
David, can we add a photo of the board here, too?
<img src="https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/images/metroCircuit.png" width="400px">

* Flash the pre-compiled `HelloYou.ino` code onto the Arduino. 
```
pi@ixeXX:~ $ cd ~/sketchbook/helloYouSketch/
pi@ixeXX:~/sketchbook/helloYouSketch $ make upload
```
Now that the Arduino code is uploaded, you should see your LED is off (because it isn't running the Blink sketch anymore).

* Run the HelloYou webserver.
```
pi@ixeXX ~/sketchbook/helloYouSketch $ cd
pi@ixeXX ~ $ cd helloYou/
pi@ixeXX ~/helloYou $ ls
helloYouSketch.ino  package.json  public  README.md  server.js
pi@ixeXX ~/helloYou $ node server.js /dev/ttyUSB0
listening on *:8000
```
* Test the functionality with remote browser.
If everything is working, you should see a message in the terminal that the webserver is listening on port 8000.

Now, you can go to you web browser and type your 'ixe[hostnumber]:8000' in the address bar.

* *David* add debug stuff

3. Distant Pictures
* Fork the 'distant-picture' example project
On your IxE, [fork](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Forking-a-GitHub-project) and git clone the [distant-picture](https://github.com/FAR-Lab/distant-pictures) example project.

`pi@ixeXX:~ $ git clone https://github.com/**_YourUserName_**/distant-pictures.git`

In the `distant-pictures` directory, install the basic components for the node server by executing `npm install` 
```
pi@ixeXX:~ $ cd distant-pictures
pi@ixeXX:~/distant-pictures $ git clone https://github.com/**_YourUserName_**/distant-pictures.git
```
* We are using the helloYou Arduino circuit and code, so no adjustment is necessary on the Arduino side.
* Plug in the web camera
* Check the web camera is working 
* Running the webserver with node.js
First navigate out of the 'ArduinoCode' directory with 'cd ..'.
Then run the code similar to last weeks assignment. However, we also need to pass reference to the Arduino port to the server.  The command should look something like `node server.js /dev/ttyUSB0`.

```shell
pi@ixe05 ~/distant-pictures $ node server.js /dev/ttyUSB0
listening on *:8000
```

If everything is working, you should see a message in the terminal that the webserver is listening on port 8000.

Just like in the [previous assignment](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Lab-%231#connect-to-your-interaction-engine) you can now go to the browser to control the Arduino and webcam. 

To shut down the server, type `control + C` in the terminal.

```shell
ledOFF
ledON
^C
pi@ixe05 ~/helloYou $
```
4.  Change the Interaction
For this lab we want to you to extend the functionality of this basic setup. As a start, we want you to change its behavior so that it takes a picture whenever someone presses the physical button.