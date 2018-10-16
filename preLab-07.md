In preparation for this week's lab, you'll build a small circuit with your Arduino and test it with some code. You don't need the Pi for this preLab.

### Button Circuit

On your breadboard, make this basic button circuit connected to `pin 2` of the Arduino. (The LED is built in on the board and connected to `pin 13`.)

<img src="https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/images/button_circuit.png" width="200px">

<img src="https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/images/metroCircuit.png" width="400px"> 

<img src="https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/images/realCircuit.jpg" width="400px">

Remember that the orientation of the button matters. Of the four pins, the pairs of pins closest to each other are the two that get connected when you push the button. And in fact, each pin of the close pair is **always connected** to the corresponding pin of the other close pair. This diagram my help:

<img src="../images/button-deal.png" width="400px" />

### Upload the `HelloYou` code

`HelloYou` is Arduino code that communicates over Serial to a Raspberry Pi (or any computer with a serial interface), sending any button events **out** to the computer, and turning on or off the built-in LED in response to message events coming **in**.

Copy this [HelloYou.ino](https://github.com/FAR-Lab/interaction-engine/blob/master/helloYouSketch.ino) sketch into a new Arduino window and upload it to your board. (The built-in LED marked `L` should be off.)

Open the Serial Monitor in Arduino and observe what happens when you press the button in your circuit -- you should see a change!