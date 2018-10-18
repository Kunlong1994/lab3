# Video Doorbell

This week, we will integrate the Arduino with the Raspberry Pi to complete the Interaction Engine system.

### In Your Report

1. Upload a video of your version of the camera lab to your lab Github repository
1. As usual, update your class Hub repository to add your [forked IDD-Fa18-Lab7](/FAR-Lab/IDD-Fa18-Lab7) repository.
1. Answer the questions in-line below on your README.md.

## Part A. HelloYou from the Raspberry Pi

First, make sure you completed the steps in [the prelab](preLab-07). Next, connect your Arduino to a USB port on your Raspberry Pi and plug in your Pi to turn it on.

### Run the HelloYou webserver.

Like for Lab 6, you should receive an email from your Pi with an IP address. Use `ssh` to connect to your Pi, as you also did for the previous lab. Then run the following commands:

```
pi@ixeXX:~ $ cd helloYou/
pi@ixeXX:~/helloYou $ ls
helloYouSketch.ino  package.json  public  README.md  server.js
pi@ixeXX:~/helloYou $ node server.js /dev/ttyUSB0
listening on *:8000
```
### Test the functionality with remote browser.

If everything is working, you should see a message in the terminal that the webserver is listening on port 8000.

Now, you can go to your web browser and type your `http://<yourPiAddress>:8000` in the address bar.

Look at the `server.js`, `public/client.js` and `public/index.html` code to understand what parts of the code do various things. 

## Part B. Web Camera

This next section adds a web camera to the HelloYou example. We make use of the 'node-webcam' from [[https://www.npmjs.com/package/node-webcam]] to add the camera functionality.

### Fork the 'IDD-Fa18-Lab7' repository

On your IxE, [fork](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Forking-a-GitHub-project) and git clone the [IDD-Fa18-Lab7](https://github.com/FAR-Lab/IDD-Fa18-Lab7) example project.

```
pi@ixeXX:~ $ cd
pi@ixeXX:~ $ git clone https://github.com/**_YourUserName_**/IDD-Fa18-Lab7.git
```

In the `IDD-Fa18-Lab7` directory, install the basic components for the node server by executing `npm install` 
```
pi@ixeXX:~ $ cd IDD-Fa18-Lab7
pi@ixeXX:~/IDD-Fa18-Lab7 $ npm install
...blah blah warnings etc. here...
added 258 packages from 138 contributors and audited 721 packages in 112.798s
found 1 low severity vulnerability
  run `npm audit fix` to fix them, or `npm audit` for details
```

This may take a minute or two to run. Please be patient.

### Connect the webcamera to your Pi

* We are using the helloYou Arduino circuit and code, so no adjustment is necessary on the Arduino side. Keep it plugged into the USB port of the Pi.
* Plug in the web camera to another USB port of the Raspberry Pi.
* Install the `fswebcam` software that your code will use to communicate with the webcam using this command:

```
pi@ixeXX:~/IDD-Fa18-Lab7 $ sudo apt install fswebcam
```

### Try pictureServer with node.js
```
pi@ixeXX:~/IDD-Fa18-Lab7 $ node pictureServer.js /dev/ttyUSB0
listening on *:8000
```
If everything is working, you should see a message in the terminal that the webserver is listening on port 8000.

Just like in the previous section, you can now go to the browser to control the Arduino and webcam. 
<img src="https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/images/distantPicture.png" width="400px">

To shut down the server, type `control + C` in the terminal.

```shell
ledOFF
ledON
^C
pi@ixeXX ~/IDD-Fa18-Lab7 $
```
*Compare `helloYou/server.js` and `IDD-Fa18-Lab7/pictureServer.js`. What elements had to be added or changed to enable the web camera? (Hint: It might be good to know that there is a UNIX command called `diff` that compares files.)*

### Video doorbell

Now, modify the `pictureServer.js` code to make a video doorbell. When a person presses the doorbell (here, the button on your Arduino), the application should snap a photo of the person in front of the doorbell, and post it to a remote webpage. 

Please submit the code for the Video doorbell as part of your lab report.

## Part C.  Make it your own

Now, extend the functionality of this basic setup. 

* Your own distributed camera app

As in the previous lab, modify the template for the lab to make it your own. You can do this just through text, better html and reframing the point of view, or you can incorporate technical improvements from the next part of the assignment...

* Try a new node library/package

Find, install, and try out a node-based library and try to incorporate into your lab. 

Document your successes and failures (totally okay!) for your report, and post them to the class Discord. This will help others in class figure out cool new tools and capabilities.

Here is an example of how to try this. Following the directions on the `https://www.npmjs.com/package/nyancat` package, for example:
```
pi@ixeXX:~/test $ sudo npm install -g nyancat
```

Some ideas, in case you are stuck:

On Linux, `node-webcam` uses `fswebcam`. https://www.npmjs.com/package/node-webcam shows other commands available using node-webcam, and typing `man fswebcam` describes a variety of image capture options. Try out some modifications, and show us the screen capture of the resulting webpage.

Another package to try: `gm`. GM is GraphicsMagick and ImageMagick for node. https://www.npmjs.com/package/gm 

**Note**: You can also upload code directly from the Raspberry Pi to the Arduino. The code that comes pre-installed on your Pi is slightly older, and assumes your button is connected to pin 11. (You can use `nano` to change the file to use pin 2 instead of 11.)

```
pi@ixeXX:~ $ cd ~/sketchbook/helloYou
pi@ixeXX:~ $ nano helloYouSketch.ino
pi@ixeXX:~/sketchbook/helloYou $ make
... compiling your code ...
pi@ixeXX:~/sketchbook/helloYou $ make upload
... uploading to your Arduino ...
```

Then re-run the server you need, and it should connect to your Arduino's new code!