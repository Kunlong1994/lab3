
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