# Video Doorbell


## Button circuit

![button](https://github.com/Kunlong1994/Interactive-Lab-Hub/blob/master/lab7/buttoncircuit.JPG)

## Serving webpages 
 
![kunlong'swebsite](https://github.com/Kunlong1994/Interactive-Lab-Hub/blob/master/lab7/servingwebpages.png)
 
**customize the code enough that the webpage served up is clearly your own, and include a screenshot and any modified code in the lab folder. **
 I changed the text to "Hello Kunlong"
 
## Set up and Run Interaction Engine

![interaction](https://github.com/Kunlong1994/Interactive-Lab-Hub/blob/master/lab7/Interactionmachine.png)

**What messages are sent from the Arduino to the Pi?**

the Arduino sends "light" when the button is pressed, then "dark" when it is released.

**What messages are expected from the Pi to the Arduino?**

light or dark/ H or L

**What happens if the Pi sends an unexpected message to the Arduino?**

The LED stays off

**How fast does the Arduino communicate with the Pi? What would you change to make it send messages less often?**

9600 as shown from serial monitor

## Run the HelloYou server on the RPi

**Look at the code. What interface does the Pi use to communicate with the Arduino when the code is running?**

SocketIO

**What messages are sent from the Pi to the Arduino?**

H/L

**What part of the code controls what is served when a browser requests a page from the server?**

index.html

**What messages are sent to the console? When?**

ledON or ledOFF

## Internet of Cornell Tech Things




## Video doorbell
 

