# Introducing the **Raspberry Pi**

## Preparing your Raspberry Pi

The following steps set up your Raspberry Pi so that it emails you the IP address that the RPi gains from the local DHCP server on boot-up. It is specifically looking for the Cornell [RedRover](https://it.cornell.edu/topic/redrover-wi-fi) network.

* Connect the microSD card to your laptop computer 
* Open the boot volume and find the  ```email_ip_on_start.py``` script.
* Open this script and find the section where the target email address is defined.


```python
##############################################################################
# PUT YOUR EMAIL HERE
to = 'youremail@here.maybe'

# PUT YOUR IXE HOSTNAME HERE (ex. "ixe00")
hostname = "ixe00"
##############################################################################
```
* Put in your email address there.
* Save the file and eject the drive.
* Then plug the microSD card into your RPi and plug the power in.

(Instructions on modifying this to get online in other places are here.)

# Chatbot

In this tutorial, we will use a Raspberry Pi to create a chatbot! Your Pi will be serving up it's own webpages with an interface that allows people to type in text entries and receive your Chatbot's replies.

The Pis we are giving you have a specific set and configuration of files known as [Interaction Engine](https://github.com/nikmart/interaction-engine/wiki), created by [Nikolas Martelaro](http://nikmartelaro.com). Those files were pre-copied onto the microSD card in your Raspberry Pi that you received from us.

## Connect to your Interaction Engine

The Pi is a single-board computer, but it doesn't have its own keyboard or mouse, so we will be connecting to the Pi remotely from your laptop over wifi. 

We will [ssh](https://en.wikipedia.org/wiki/Secure_Shell) into the system so that we can control the computer via [Terminal on Mac](http://blog.teamtreehouse.com/introduction-to-the-mac-os-x-command-line) or [PuTTy on Windows](https://www.ssh.com/ssh/putty/download).

These instructions assume your laptop and Pi are both connected to the same network, [RedRover](https://it.cornell.edu/wifi). If you have followed the preparatory instructions earlier, your Pi should have booted up and sent you an email with its wifi IP address. This IP address is available from the local network (i.e., RedRover) and we will use it to talk and control the Pi. 

In the following section, we will refer to your IP address with the name `$Address`. Whenever you see this, replace the text (`$Address`) with the IP address your received in your mail.


### 1. Verify the Pi is online

First, in your terminal program, `ping` your Pi to make sure it is online. Open your terminal (or `cmd` on Windows) and type `ping $Address` where your replace `$Address` with the IP address you received in the email. 

```shell
you@your-machine:~$ ping 192.168.2.2
PING 192.168.2.2: 56 data bytes
64 bytes from 192.168.2.2: icmp_seq=0 ttl=64 time=0.467 ms
64 bytes from 192.168.2.2: icmp_seq=1 ttl=64 time=0.471 ms
64 bytes from 192.168.2.2: icmp_seq=2 ttl=64 time=0.550 ms
64 bytes from 192.168.2.2: icmp_seq=3 ttl=64 time=0.670 ms
64 bytes from 192.168.2.2: icmp_seq=4 ttl=64 time=0.720 ms
^C
--- 192.168.2.2 ping statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.467/0.576/0.720/0.103 ms
```

You can use `control-C` to interrupt and exit the ping (press the `control` key, and while holding it down, also press the `C` key, then let go of both together--this looks like `^C` in the terminal).

If you do not see the response from the `ping` command, [troubleshoot](Getting-an-IxE-based-Pi-on-your-Wi-Fi#troubleshooting) to get your Pi online.  

### 2.  SSH into the Pi.
From your terminal, log in to your Pi using the command `ssh pi@$Address` with the password: `raspberry`

When you first log in it will show you a "fingerprint" and ask you whether you want to continue connecting. Say `yes`.

```shell
ssh pi@192.168.2.2
The authenticity of host '192.168.2.2' can't be established.
ECDSA key fingerprint is SHA256:Y9S4oMH2H70fz3K/L42Kw39k+zkpyfr0DmGdzBx7SKk.
Are you sure you want to continue connecting (yes/no)? yes
```
After you say yes, type the password `raspberry` and hit Enter. You should see this:

```shell
pi@192.168.2.2's password:
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

Once you are signed in, your terminal will now connected directly to the 'terminal' on your Pi, via `ssh`. You can tell this by looking at the user and hostname at the beginning of each line, which should now look like:

```shell
pi@ixe00 ~ $
```

## Setup and run the ChatBot Example

### Installation
Clone (download) the repository from GitHub to the Pi. 

1. From the terminal window which is logged into the Pi, go to the home folder with `cd ~`
1. In a web browser on your laptop, fork the github project [IDD-Fa18-lab6](https://www.gitHub.com/far-lab/IDD-Fa18-Lab6), by clicking the fork button on the top right side.
1. Copy the link to your forked version of the project.<!--(for more information on forking look [here](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Forking-a-GitHub-project)). -->
1. From the terminal window which is logged into the Pi, clone the git repository with the copied information
```shell
git clone https://github.com/**_YOURUSERNAME_**/IDD-Fa18-Lab6
```
1. Change directory into the downloaded folder with `cd IDD-Fa18-Lab6`
1. Use `npm` to install the required node packages; run the command `npm install`.

At this point, you have now downloaded the main program and all required packages to run the simple chatbot. 

### Start-Up

Now start the server on the Pi, then access the chatbot page served by the Pi with a browser on your laptop.

On the Pi's terminal, start the server by typing `node chatServer.js`.

Then, in a browser on your laptop, go to `$Address:8000` (Don't forget to replace the `$Address` with the actual IP address of your Pi).

Once the webpage is loaded on your laptop browser, you should see a text field and the first greeting from the ChatBot on the webpage.
[[images/chatBotConnected.png]]

#### Debugging
If the previous steps did not work, there are a few things you can easily check/debug:

First, verify that the server is running. The command line window should say
```shell 
pi@$Address:~/IDD-Fa18-Lab6 $ node chatServer.js 
listening on *:8000
a new user connected
```
If that is not the case, verify that you are in the right folder and have done all the necessary steps to installing the additional packages. One way to verify that is by typing ```pwd``` (which stands for **P**rint **W**orking **D**irectory) to see if you really are working in the correct directory. The printed response in the terminal should be something like ```/home/pi/IDD-Fa18-Lab6```. Verify that you have all files in the folder with `ls`. The item list should be:
```shell 
pi@$Address:~/IDD-Fa18-Lab6 $ ls
chatServer.js  license.txt  node_modules  package.json  package-lock.json  public  README.txt
```
If files are missing, or you are not in the correct folder, then change to the correct folder location and try to re-run the instructions from the tutorial.
  
Second, make sure that your laptop is connected to RedRover, the same network as the Pi. This type of server is typically only routed/addressable locally, i.e., when you are on the same network.

## Understanding the code

### chatServer.js (The RPi code)
The chatServer.js code is written in javascript. It is run on the IxE using [node.js](https://en.wikipedia.org/wiki/Node.js). This code handles the different client interactions and manages the network connections. 

### index.html and index.js (The browser code)
`index.html` is written in HTML, but includes a link to the `index.js` javascript file via the `<script src='js/index.js'></script>` tag. The `index.js` code links to the elements created in `index.html`, and is written in javascript. These files are served from the IxE when Node is running `chatServer.js`. Both index.html and `index.js` are transmitted as text from the Node server to the browser, and then run within the web browser.

#### Annotated code tours

Please take a self-guided trip through the following code tours:

* [chatServer.js](chatServer.js,-annotated)
* [index.js](index.js,-annotated)

## Make the ChatBot your own

Now, please modify the `chatServer.js` file to make your own chatbot. It might, for example, act like [WoeBot](https://woebot.io) and find out what is bringing a person down. Or! Maybe it helps people fall asleep like [Insomnobot](http://insomnobot3000.com). You have a finite amount of time, so narrow the purpose of the chatbot so that it does not have to have [Turing-complete](https://en.wikipedia.org/wiki/Turing_completeness) conversational ability.

### Editing the Code ###
To change how your chatbot behaves, you will need to edit the code. To edit the code files, you can use `nano` a command line text editor.

To edit your `chatServer.js` code, make sure you are in the `IDD-Fa18-Lab6/` directory and then open the code file using the command:

```shell
nano chatServer.js
```

The files should then open up on your screen. You can move around the file using your arrow keys. Note: `nano` is a very simple editor. There is no mouse-click support. You will need to move around the file using just the arrow keys **up**, **down**, **left**, and **right**.

Let's edit the name of your chatbot first.

Move to the line of code that says:

```shell
socket.emit('answer', "Hey, Hello I am \"___*-\" a simple chat bot example."); // We start with the introduction;
```

Then move your cursor to the `\"___*-\"`, delete it using backspace, and type in the name you would like to call your chatbot.

Once you change the name, you will want to save your file then exit.
### Exit and Save

To exit the `nano` editor, type `^X` or `Ctrl` + `X`. This will then return you to the terminal console. 
In `nano` if you just hit `^X` (without saving before hand with `^o`), it will ask you if you want to `Save modified buffer?  (Answering "No" will DISCARD changes.)`. You can then type `y`, `Y`, or `Yes` then hit `Enter` and it will save and exit.

You should then be able to re-run your chatbot using `node chatServer.js` and you should see that your chatbot now has the name you gave it.

#### Pro-tips and other commands
Notice on the bottom of the terminal window that there is some text showing things like `^G Get Help` and `^O Write Out`. These are the commands that you can use in `nano`. The `^` character stands for `Ctrl`. So to `Write Out` (which means to save the file), you would type `Ctrl` and `O` (that's the letter `O`, not the number `0`). When you've typed these, you will see a bar appear at the bottom of the terminal that says `File Name to Write: chatServer.js`. This is the file name you are saving to. In this case, we want the same name, so we can just hit the `Enter` key. You will then see a message on the bottom that tells you how many lines were written, something like `[ Wrote 116 lines ]`.


`nano` is a general purpose text editor, so you can use it for any type of text file like the `.js`, `.html`, and `.css` files in this project.

## Record someone trying out your ChatBot

Using a phone or other video device, record someone trying out your ChatBot. (This does not need to be an advertisement for your ChatBot; it is okay if the person is confused or asks questions or doesn't like it. We like the drama.) Post the video to your README.md page!

## Submitting the Code
This project is going to be the submission of this week. You will need to upload the changes you made on the Pi to the GitHub page. To do that you need to follow three simple steps: Stage => Commit => Push! 
1. Add the files you want to `push` to GitHub. By using the command `git add`. If you changed the `chatServer.js`, for example, type `git add chatServer.js`. Now `chatServer.js` is "staged". You can view the current status of changed and staged files by running the `git status` command.
1. Now we create a new commit with that staged file. For that we use the `git commit` command like so:
`git commit -m 'Added new intro message.'`. The -m option allows to add a short message between the `'` signs. It helps you and everyone else keep track of the changes to the file, and the `git commit` command requires it.
1. The last step is pushing this commit to GitHub. Type `git push` to contact GitHub and upload your changes to your repository.

You might be required to login in the terminal to your GitHub account. For more details on how the Git commands work or what other commands are available checkout this [cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf).  

As usual, please submit your code by linking to **your forked copy** of the lab's GitHub repository on your class Hub page.