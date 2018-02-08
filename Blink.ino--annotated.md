The Blink.ino program is a simple Arduino program written in C++. It will periodically flash the LED that is on the board connected to Pin 13. Whenever this pin 13 is turned HIGH the LED turns on; off when pin 13 is turned LOW.  


Arduino Programs typically have three parts.

First, the main global variables are being defined. These variables that need to be kept track of over the runtime of the program. In this example, it is the pin on which the led is connected. 
```c++
int led = 13;
```

The second part is initializing any libraries, inputs, and outputs. This is done in the `void setup(void){}` function. In this case the led pin, pin 13 is initialized as an output. 
```c++
void setup(void) {
  pinMode(led, OUTPUT);
}
```
The third part of the program is the main loop.  All instructions that continuously need to be executed in this `void loop(){}` function. In this example, the LED is turned on(`digitalWrite(led, HIGH);`) and off(`digitalWrite(led, LOW);`) every 100 milliseconds. `delay(100);` causes the arduino to wait for 100 milliseconds. 
```c++
void loop() {
  digitalWrite(led, LOW);
  delay(100);
  digitalWrite(led, HIGH);
  delay(100);
}
```