# gateway-iC880a

Gateway config
This installer targets the SPI version of the board. IMST iC880a + Raspberry Pi.

- Download [Raspbian Jessie Lite](https://www.raspberrypi.org/downloads/)
- Follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to create the SD card
- Start your RPi connected to Ethernet
- Plug the iC880a (**WARNING**: first power plug to the wall socket, then to the gateway DC jack, and ONLY THEN USB to RPi!)
- Login with the default user pi and password raspberry
- Run raspi-config
```
		$ sudo raspi-config
```
- Enable SSH mode in Interface Options
- Enable SPI in Advanced Options
- Save
- Write down your IP address if you want to use your machine to connect to the Rpi. By default DHCP is enabled.
```
		ifconfig
```
- Reboot
- Now if you want you can ssh into the RPi using the default hostname
```
	local $ ssh pi@<youripaddress>
```
- Configure locales and time zone:
```
	$ sudo dpkg-reconfigure locales
	$ sudo dpkg-reconfigure tzdata
```
- Make sure you have an updated installation and install git
```
	$ sudo apt-get update
	$ sudo apt-get upgrade
	$ sudo apt-get install git
```
- Create new user for ResIOT and add it to sudoers
```
	$ sudo adduser resiot
	$ sudo adduser resiot sudo
```
- Logout and login as resiot and remove the default pi user
```
	$ sudo userdel -rf pi
```
- Now You can setup a wifi connection if you wish to:
```
	$ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
And add the following block at the end of the file, replacing SSID and password to match your network:
```
	network={
		ssid="The_SSID_of_your_wifi"
		psk="Your_wifi_password"
	}
```
- Clone the installer and start the installation
```
	$ git clone https://github.com/resiot/gateway-iC880a.git ~/resiot
	$ cd ~/resiot/<yourserver>
	$ sudo chmod 775 ./install.sh
	$ sudo chmod 775 ./start.sh
	$ sudo ./install.sh
```