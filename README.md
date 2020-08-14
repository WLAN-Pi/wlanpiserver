# WLAN Pi Server Mode
*Turn your WLAN Pi into a DHCP server and TFTP server*

The WLAN Pi server mode has been added to provide a lab build, upgrade and staging capabilities without any additional servers or apps. Simply plug your WLAN Pi into your lab switch and let it provide basic network services to the lab kit.

If you plug a Wi-Fi adapter to its USB port, the WLAN Pi will broadcast wlanpi_server SSID which makes it easier for you to wirelessly access the wired lab subnet 192.168.73.0/24.

## A word of caution
!!! Server mode enables DHCP server on the wired Ethernet interface of the WLAN Pi. Only plug this interface to a lab, staging or network which is under your own management. Never connect this to a production network as it can cause service disruption !!!

## Requirements

To use server mode on your WLAN Pi, you will need:

 - a supported USB Wi-Fi adapter plugged into the WLAN Pi (e.g. Comfast CF-912AC, adapter with MediaTek MTK7612U chipset)
 - WLAN Pi running release 2.0 or newer

## Configurations Options

It is very likely that you will not want to use this utility with the default shared key, channel and SSID. The defaults are:

* shared key: wifipros
* ssid: wlanpi_server
* channel: 36

To change from default settings, ensure that the WLANPi is operating in standard "classic" mode (i.e. it has not already been switched in to another node such as hotspot or wireless console mode). Then, edit the file: /etc/wlanpiserver/conf/hostapd.conf. This can be done by opening an SSH session to the WLANPi and using the 'nano' editor:

```
 sudo nano /etc/wlanpiserver/conf/hostapd.conf
```

There are numerous fields you can configure to change the behaviour of the hotspot access point feature, but here are some of the more likely fields you'll want to look at and perhaps update (note that lines beginning with a # character are comments and do not affect operation):

```
    # WLAN SSID
    ssid=wlanpi_server

    # WPA-PSK
    wpa_passphrase=wifipros

    # Mode options: a=5GHz / g=2.4GHz
    hw_mode=a

    # Set 2.4GHz Channel - 1,6,11
    # Set 5GHz Channel - 36,40,44,48,149,153,157,161,165
    channel=36

    # Set Country Code (Use your own country code here)
    country_code=UK
```

Once you have made your changes, hit Ctrl-X in the nano editor to exit and hit "Y" to save the changes when prompted.

Next, flip the WLAN Pi in to "Server" mode using the front panel controls of the WLAN Pi. The required front panel option is: "Menu > Modes > Server > Confirm". This will trigger a reboot of the WPAN Pi to switch it into to hotpot mode.  After the accompanying reboot, the WLANPi should operate using the parameters configured in hostapd.conf.

If you need to make any subsequent alterations to the parameters configured in hostapd.conf, after making your edits, reboot the WLAN Pi so that they take effect.

# Using Server Mode

Following the WLAN Pi reboot, your configured server mode SSID should be available in the network list shown on your wireless client.

Once you have joined the SSID, an IP address is assigned to your client device via DHCP and you will have access to the WLAN Pi itself (e.g. SSH to 192.168.74.1). You will be able to access features such as the built-in speedtest utility using a browser pointed at : http://192.168.74.1/

Plug the Ethernet port of the WLAN Pi to your lab switch and it will provide  IP addresses to the wired devices.
