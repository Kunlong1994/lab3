We can use an open source image streamer to live stream the Pi Camera to a web page. This will allow you to embed a live camera stream into your web page apps.

First, make sure to plug in the webcam using the USB cable.

Next, log into you IxE and navigate to the `mjpg-streamer/mjpg-streamer-experimental/` directory

```shell
cd mjpg-streamer/mjpg-streamer-experimental/
```

Next, configure the library path

```shell
export LD_LIBRARY_PATH=.
```

Then start MJPG-STREAMER using

```shell
./mjpg_streamer -o "output_http.so -w ./www" -i "input_uvc.so -q 85 -f 15 -y -n"
```

You should see some output that looks like this:

```shell
WENDY PLACE OUTPUT HERE
```