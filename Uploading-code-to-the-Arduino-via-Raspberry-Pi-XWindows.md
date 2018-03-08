A different way to upload code to the Arduino is by using an X-11 connection. 
You connect to your RasperryPi with x windows enable using the `-X` attribute like this
```shell
ssh -X pi@ixe[00]
```
In this way, X11 is enabled. The connection does not look in any way different. 
Once the connection is established you can use normal Arduino remotely.
So just run:
```shell
arduino
```

This will open a x-windows session with the Arduino window. Caution the connection is slow!
