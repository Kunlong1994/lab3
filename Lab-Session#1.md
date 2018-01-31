# LabSession #1

## Task overview:
1. Familiarize yourself with the [UNIX Commands](https://www.tjhsst.edu/~dhyatt/superap/unixcmd.html). This [UNIX cheatsheet](https://ubuntudanmark.dk/filer/fwunixref.pdf) might also help.
1. Connect to your [Interaction Engine(IxE) / Raspberry Pi](#Connect-to-your-Interaction-Engine)
1. Run the [ChatBot Example](#Set-up-and-run-the-ChatBot-Example)


## Connect to your Interaction Engine(#Connect-to-your-Interaction-Engine)

This is a copy of the [original resources](https://github.com/nikmart/interaction-engine/wiki/Log-on-to-your-Interaction-Engine)

### Set-up and run the ChatBot Example(#Set-up-and-run-the-ChatBot-Example)
This is a copy of the original file from[](https://github.com/FAR-Lab/simple-ChatBot/wiki/Running-ChatBot)
Welcome to the simple-ChatBot wiki!
### Installation
Clone(download) the repository from GitHub to the IxE. 
1. Go to the home folder with ```cd ~```
1. Clone the git repository with
```
git clone https://github.com/FAR-Lab/simple-ChatBot simple-ChatBot
```
1. Change directory into the downloaded folder with ```cd simple-ChatBot```
1. Let npm install the required node packages with ```npm install```
At this point, you will have downloaded the main program and all required packages to run it. 

### Start-Up
Now we need to start the server and connect to it with a browser.
We start the server by typing ```node chatServer.js```
In a browser go to ```ixe[00].local:8001``` (replace the [00] with the number associated with that interaction engine).
Once loaded, you should see a text field and the first greeting from the ChatBot.

#### Debugging
If the previous steps did not work there are a few things you can easily check/debug:
First, verify that the server is running. The command line window from your ixe[00] should say
```shell 
pi@ixe[00]:~/simple-ChatBot $node chatServer.js 
listening on *:8001
a new user connected
```
If that is not the case, verify that you are in the right folder and have done all the necessary steps to installing the additional packages. One way to very fy that is by typing ```pwd``` to see if you really are working in the correct directory. The answer that pops-up should be something like ```/home/pi/simple-ChatBot```.  Very fy that you have all files in the folder with ```ls ```. The item list should be 
```shell 
pi@ixe[00]:~/test/simple-ChatBot $ ls
chatServer.js  license.txt  node_modules  package.json  package-lock.json  public  README.txt
```
If files are missing or you are not in the correct folder change to the correct folder location and try to re-run the instructions from the tutorial.  
Second, make sure that you are connected to the same network as the interaction engine. This type of server is typically only routed/addressable locally i.e. when you are on the same network.

### Understanding the code


What does the server do?

What does the client do?

How do they communicate?

Where does the chatbot actually live?

How can we change the chatbot?





