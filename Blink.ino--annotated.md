The Blink.ino program is a simple Arduino program written in C++. It will periodically flash the LED that is on the board connected to Pin 13. Whenever this pin 13 is turned HIGH the LED turns on; off when pin 13 is turned LOW.  


Arduino Programs typically have three parts.

First, the main global variables are being defined. These variables that need to be kept track of over the runtime of the program. In this example, it is the pin on which the led is connected. 
```c++
int led = 13;
```
void setup(void) {
  pinMode(led, OUTPUT);
}

