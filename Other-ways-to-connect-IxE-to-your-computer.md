
## Connect IxE to your computer via the computer Ethernet port

(based off of instructions from [Nikmart's IxE Git](https://github.com/nikmart/interaction-engine/wiki/Connect-IxE-to-your-computer-via-Ethernet-port))

### Instructions for Mac

1. Plug an ethernet cable from your Mac to the Raspberry Pi (note you may need to use a Thunderbolt to Ethernet or USB to Ethernet adapter if your Mac does not have a built-in Ethernet port).

2. Check that the IxE are getting a self-assigned IP in System Preferences -> Network. It should have an orange color.

3. To get Internet on your Pi, use Internet Sharing and share your Wifi with your Ethernet. (Note: This will not work on 802.11X like eduroam. If you are trying to do this on campus, connect to Cornell Visitor and then share your wifi)

3. Try pinging your IxE with the .local extension: ping ixe05.local

If the ping work, you can ssh in just like normal.

### Instructions for PC

[someone with a pc, please update this...]

## Connect IxE to your computer via a separate WiFI card

You can share a WiFi connection to the wider internet from your laptop if you can bring up a separate Wifi interface on your computer (for example by using a USB Wifi adapter).

### Instructions for Mac

1. Bring up the new WiFi interface. This will likely involve installing the drivers for the device, registering the new interface (for example, by using http://mycomputers.cit.cornell.edu at Cornell), and getting it online.

1. Go to the Sharing control panel to enable Internet sharing from your newly installed interface to the WiFi network which you will share locally. Go to WiFi Options to configure your network to be named DeviceFarm, and the WPA2 password to be the the DeviceFarm password. Finally, check Internet Sharing to turn the sharing on.

1. Power up your IxE. It should come up on your local network, and you should be able to access it via ssh like you would on the class network.

[someone with a pc, please update this...]

## Connect your IxE to your own WiFi

Based on instructions found here: [https://howchoo.com/g/ndy1zte2yjn/how-to-set-up-wifi-on-your-raspberry-pi-without-ethernet](https://howchoo.com/g/ndy1zte2yjn/how-to-set-up-wifi-on-your-raspberry-pi-without-ethernet)

If you have a WiFi router at home that you control, you can connect to it by setting the wifi configuration of your Pi. To do this:

1. Use a text editor on your computer to create a file called `wpa_supplicant.conf` with the following text in it:

```shell
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="DeviceFarm"
    psk="device@theFarm"
    key_mgmt=WPA-PSK
}

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="YOUR WIFI NAME HERE"
    psk="YOUR WIFI PASSWORD HERE"
    key_mgmt=WPA-PSK
}
```
2. Plug the SD card with the IxE image on it into your computer.
You should see a disk drive called `boot` mount to your computer.

3. Open `boot` and copy the `wpa_supplicant.conf` file into the directory.

4. Safely eject the SD card from your computer.

5. Plug the SD card back into your IxE, then plug it into USB power.

When the Pi boots up, it will copy the `wpa_supplicant.conf` file into the WiFi settings directory in `/etc/wpa_wupplicant/`. This will update your WiFi setting and should get the Pi on your home wifi.

## Connecting to The HOUSE Wifi

1. Register the MAC address of your Raspberry Pi on The House network at https://myelauwit.com/ using Add a Device.
1. Edit the `/etc/wpa_supplicant/wpa_supplicant.conf` file as explained in the section above

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
3. Try logging into your device using ssh from a terminal.
4. If you need to see what device your IxE is on, use `iwconfig` or find it in this list [here](https://interactivedevice18.slack.com/files/U90LA9TLH/F92HXB020/ixe_ip_mac_hostname.xlsx):

```shell
pi@ixe42:~ $ iwconfig wlan0
wlan0     IEEE 802.11  ESSID:"The House"  
          Mode:Managed  Frequency:2.462 GHz  Access Point: 24:79:2A:21:58:C8   
          Bit Rate=72.2 Mb/s   Tx-Power=31 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=67/70  Signal level=-43 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0
```

## Connecting to RedRover
You can get your Pi working on Cornell's `RedRover` network by:

### Registering your Pi's MAC address to your Cornel account at: [https://dnsdb.cit.cornell.edu/dnsdb-cgi/mycomputers.cgi](https://dnsdb.cit.cornell.edu/dnsdb-cgi/mycomputers.cgi)

You can find your MAC address using the spreadsheet (IXE_IP_MAC_HOSTNAME) we provided on the class Slack. The MAC address is associated with you ixe hostname in the form ixe[00] where [00] are your numbers.

Register your MAC address as one of your devices. We recommend you name is ixe[00] so you know which registration this is for.

### Adding a python script to your machine to email the ixe's IP to you

1. While you are logged into you Pi (from DeviceFarm, The House, or through ethernet), create a new file for the `python` script that will email the IP to you

```shell
nano startup_mailer.py
```

2. Copy and paste this python code into the editor

```pyhton
import subprocess
import smtplib
import socket
from email.mime.text import MIMEText
import datetime

# Change to your own account information
to = 'YOUREMAIL@DOMAIN.com'
gmail_user = 'interactiveDeviceDesign@gmail.com'
gmail_password = 'device@theFarm'
smtpserver = smtplib.SMTP('smtp.gmail.com', 587)
smtpserver.ehlo()
smtpserver.starttls()
smtpserver.ehlo
smtpserver.login(gmail_user, gmail_password)
today = datetime.date.today()

# Very Linux Specific
arg='ip route list'
p=subprocess.Popen(arg,shell=True,stdout=subprocess.PIPE)
data = p.communicate()
split_data = data[0].split()
ipaddr = split_data[split_data.index('src')+1]
my_ip = 'ixe58 ip is %s' %  ipaddr
msg = MIMEText(my_ip)
msg['Subject'] = 'IP For ixe58 on %s' % today.strftime('%b %d %Y')
msg['From'] = gmail_user
msg['To'] = to
smtpserver.sendmail(gmail_user, [to], msg.as_string())
smtpserver.quit()
```

1. Look for the line `to = 'YOUREMAIL@DOMAIN.com'` and replace the email address with your email. Any email like your GMail or Cornell Email should work fine.


 

### Connecting to your Pi using the IP it has with your laptop on `RedRover` or `eduroam`

