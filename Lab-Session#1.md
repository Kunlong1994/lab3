# LabSession #1 - overview:
1. Familiarize yourself with the [UNIX Commands](https://www.tjhsst.edu/~dhyatt/superap/unixcmd.html). This [UNIX cheatsheet](https://ubuntudanmark.dk/filer/fwunixref.pdf) might also help.
1. Connect to your [Interaction Engine(IxE) / Raspberry Pi](#connect-to-your-interaction-engine)
1. Run the [ChatBot Example](#setup-and-run-the-chatbot-example)
1. Modify the ChatBot to make it your own. 
1. Record someone else trying out your ChatBot.


## Connect to your Interaction Engine

This is a copy of the [original resources](https://github.com/nikmart/interaction-engine/wiki/Log-on-to-your-Interaction-Engine)
In this tutorial we will ssh into the system so that we can control the computer via Terminal or Putty on Windows.

### 1. Verify IxE is online
TL,DR
1. `ping` + `ixe[00].local` (change the last digits, and remove the brackets to match yours)
2. Is it running? If yes, cool. `control + C` and move on to step 2.

LONGER VERSION

First, `ping` the system to make sure it is online. (If not, [troubleshoot](Getting-an-IxE-based-Pi-on-your-Wi-Fi#troubleshooting) to get it online). Remember your IxE will be named something like `ixe##` where the number corresponds to the number on the SD card (ex: ixe01, ixe04, ixe11). You can use `control + C` to exit the ping (this looks like `^C` in the terminal).

```shell
nik@DN51sk9s:~$ ping ixe05.local
PING ixe05.local (192.168.2.2): 56 data bytes
64 bytes from 192.168.2.2: icmp_seq=0 ttl=64 time=0.467 ms
64 bytes from 192.168.2.2: icmp_seq=1 ttl=64 time=0.471 ms
64 bytes from 192.168.2.2: icmp_seq=2 ttl=64 time=0.550 ms
64 bytes from 192.168.2.2: icmp_seq=3 ttl=64 time=0.670 ms
64 bytes from 192.168.2.2: icmp_seq=4 ttl=64 time=0.720 ms
^C
--- ixe05.local ping statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.467/0.576/0.720/0.103 ms
```

### 2.  SSH into the IxE.
Log in to your Pi using the command `ssh pi@ixe[00].local` with the password: `raspberry`

When you first log in it will ask you if you want to continue connecting. Say `yes`

```shell
ssh pi@ixe00.local
The authenticity of host 'ixe00.local (fe80::1216:6c33:ec58:34a5%en0)' can't be established.
ECDSA key fingerprint is SHA256:Y9S4oMH2H70fz3K/L42Kw39k+zkpyfr0DmGdzBx7SKk.
Are you sure you want to continue connecting (yes/no)? yes
```
After you say yes, type the password `raspberry` and hit Enter. You should see this:

```shell
i@ixe00.local's password:
Linux ixe00 4.9.59-v7+ #1047 SMP Sun Oct 29 12:19:23 GMT 2017 armv7l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Jan 17 10:42:03 2018

SSH is enabled and the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set a new password.

pi@ixe00:~ $ 
```

Once you are signed in, your terminal will now be the terminal for the IxE. You can tell this by looking at the user and hostname at the beginning of each line, which should now look like:

```shell
pi@ixe05 ~ $
```





## Setup and run the ChatBot Example
This is a copy of the [original wiki](https://github.com/FAR-Lab/simple-ChatBot/wiki/Running-ChatBot)
Welcome to the simple-ChatBot wiki!
### Installation
Clone(download) the repository from GitHub to the IxE. 
1. Go to the home folder with ```cd ~```
1. Clone the git repository with
```
git clone https://github.com/FAR-Lab/simple-ChatBot simple-ChatBot
```
1. Change directory into the downloaded folder with ```cd simple-ChatBot```
1. Let ```npm``` install the required node packages with ```npm install```
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

## Make the ChatBot your own

Now, please modify the chatServer.js file to make your own chatbot. It might, for example, act like [WoeBot](https://woebot.io) and find out what is bringing a person down. Or! Maybe it helps people fall asleep like [Insomnobot](http://insomnobot3000.com). You have a finite amount of time, so narrow the purpose of the chatbot so that does not have to have [Turing-complete](https://en.wikipedia.org/wiki/Turing_completeness) conversational ability.
