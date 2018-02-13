Sometimes the Arduino or other devices connected to the PI over USB get a different port assign by the system. If the standard port `/dev/ttyUSB0` does not work it is possible that it got assigned a different port number. 

To see what port the Arduino is on we can use `ls /dev/tty*` (`*` is a wildcard, giving us al listings with anything after the `*`). In this case, the Arduino Uno we use is usually at `/dev/ttyUSB*` where `*` will be a number and most of the time is 0.

```shell
pi@ixe05 ~/sketchbook/blink $ ls /dev/ttyUSB*
/dev/ttyUSB0
```

This tells us that we have a port at `/dev/ttyUSB0`.

Sometimes the Arduino can be found under `/dev/tty/ACM*` and the like. 
If the Arduino still does not show up there is one more thing to try on the port side.

1. Disconnect the Arduino 
1. Run the command `ls /dev/tty*`
1. Connect the Arduino
1. Run the command `ls /dev/tty*` again
1. Finally, compare the two lists that were generated and see which device `tty` port was added. This is likely the connected Arduino. 