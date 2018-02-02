
## Connect IxE to your computer via the computer Ethernet port

(based off of instructions from [Nikmart's IxE Git](https://github.com/nikmart/interaction-engine/wiki/Connect-IxE-to-your-computer-via-Ethernet-port))

Instructions for Mac

1. Plug an ethernet cable from your Mac to the Raspberry Pi (note you may need to use a Thunderbolt to Ethernet or USB to Ethernet adapter if your Mac does not have a built in Ethernet port).

2. Check that the IxE are getting a self assigned IP in System Preferences -> Network. It should have an orange color.

3. Try pinging your IxE with the .local extension: ping ixe05.local

If the ping work, you can ssh in just like normal.

Instructions for PC

[someone with a pc, please update this...]

## Connect IxE to your computer via a separate WiFI card

You can share a WiFi connection to the wider internet from your laptop if you can bring up a separate Wifi interface on your computer (for example by using a USB Wifi adapter).
Instructions for Mac

1. Bring up the new WiFi interface. This will likely involve installing the drivers for the device, registering the new interface (for example, by using http://mycomputers.cit.cornell.edu at Cornell), and getting it online.

1. Go to the Sharing control panel to enable Internet sharing from your newly installed interface to the WiFi network which you will share locally. Go to WiFi Options to configure your network to be named DeviceFarm, and the WPA2 password to be the the DeviceFarm password. Finally, check Internet Sharing to turn the sharing on.

1. Power up your IxE. It should come up on your local network, and you should be able to access it via ssh like you would on the class network.

[someone with a pc, please update this...]

## Connect your IxE to your own WiFi

Based on instructions found here: [https://howchoo.com/g/ndy1zte2yjn/how-to-set-up-wifi-on-your-raspberry-pi-without-ethernet](https://howchoo.com/g/ndy1zte2yjn/how-to-set-up-wifi-on-your-raspberry-pi-without-ethernet)

If you have a WiFi router at home that you control, you can connect to it by setting the wifi configuration of your Pi. To do this, you will need to create a file called `wpa_supplicant.conf` with the following text in it:

```shell
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="DeviceFarm"
    psk="device@theFarm"
    key_mgmt=WPA-PSK
}

network={
    ssid="YOUR WIFI NAME HERE"
    psk="YOUR WIFI PASSWORD HERE"
    key_mgmt=WPA-PSK
}
```

You can create this file with a text editor on your laptop.

Once you have saved the file, make sure your IxE is shutdown.

Take out the SD card and plug it into your laptop so you can see the files.

You should see a disk drive called `boot` mount to your computer.

Open `boot`

## Connecting to The HOUSE Wifi

```shell
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="DeviceFarm"
    psk="device@theFarm"
    key_mgmt=WPA-PSK
}

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="The House"
    key_mgmt=NONE
}
```