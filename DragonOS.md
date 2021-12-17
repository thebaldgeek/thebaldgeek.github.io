# Care and feeding of DragonOS.   
   
Navigation: [home](README.md)  

No matter your interest in AERO data, be it HF-DL, VHF VDL2, L-Band Data, L-Band voice, C-Band Data or C-Band voice or any combination (up to your CPUs ability to keep up), if you are running Linux, DragonOS should be strongly considered as you go-do distro to get up and running.  
To this end, this page will try and help smooth out that process.   
## DragonOS or Windows?   
Lets get this out the way first.  
If you only want to run SDRReciver and Jaero (For C or L-Band work), you can do that on Win7, Win10 or Win11. Both program's _require_ a desktop GUI, both run fine under Windows.  
dumpVDL2 and dumpHFDL on the other hand, do not use any graphics at all, they are both command line programs and more so, both only run under Linux, for VHF and HF ACARS, you must go the Linux route.    
## Raspberry Pi or old PC/Laptop?  
There are two builds of DragonOS, one for the Pi4 and one for PC's and laptops.   
If you want to erase Windows and put DragonOS on an old bit of hardware, thats your call. The old laptop/PC should have more bang for the CPU buck than the Pi, so you might be able to run more programs at once. (Jaero and dumpHFDL are CPU intensive - you cant run both on a Pi4 for example).    
## DragonOS on a Pi 4   
It seems from early adopters / testers that the Pi 4 with 4 gig of RAM is plenty (2 gig RAM is a bit light on, and 8 gig of RAM is a waste of money - the CPU will max out long before the RAM will).   
Start by downloading the latest image of DragonOS and burn it to a 32 Gigabyte (minimum) microSD card.  
From here on this page is about getting set up and running on a Pi 4, so that should be noted.
<https://sourceforge.net/projects/dragonos-pi64/>   
Burn it using your tool of choice.   
Note that SSH is enabled by default.
## Enable HDMI
Once the image is burnt, open up the `usercfg.txt` and make sure that `hdmi_force_hotplug=1` is uncommented.   
To that same file, just below that line, add `hdmi_group=2` and on the next line add `hdmi_mode=82` (this adds a monitor resolution of 1920x1080, use mode=47 for a 1440x900 monitor, mode=35 for a 1280x1024. You can look up other modes from this table [here](https://www.raspberrypi.com/documentation/computers/config_txt.html#:~:text=These%20values%20are%20valid%20if%20hdmi_group%3D2%20(DMT)%3A))  
Now you can unmount the microSD card and put it in the Pi 4.   
## Headless Setup
Once that is done insert it into your Pi 4 and power up.   
Make sure you are connected to an Ethernet port the first few boots. Once you can VNC in, then you can join your wifi.   
You will need to find the IP address the Pi got from your router. You can look on your router or Fingbox or network scanning app on your phone or PC and find the IP address the Pi was given on your network and shell (MobaXterm, PuTTY or Power Shell are my go-tos in that order) into the Pi using the default user/pass of ubuntu / dragon  

Note. You must shell in and do the following commands before you can VNC to the desktop.
## Run raspi-config

Once you are in shell, run `sudo raspi-config` and from there the first thing I do is to [set the time to UTC](raspberrypi.md), expand the file system to the full SD card and turn on the VNC server. None of these three things are optional. Of course you can also change the hostname and any other tweaks you might know of, but those 3 things a must-do in my setup.   
I _do not_ recommend changing the default *username* of `ubuntu`. If you do, know what you are doing as a lot of paths and system settings are going to change. Changing the *hostname* (as it will show on your network) is fine and probably recommended depending on how many 'ubuntu' hosts you currently have on your network.   
After setting those 3 values, reboot and log back in with shell.  
### Enable auto login    
Once back in, we need to enable auto desktop log in, this is critical for VNC to to work.    
`sudo nano /etc/gdm3/custom.conf` in that file, uncomment the auto log in line and uncoment the user name and change it from user1 to ubuntu.   
It should look like this:   
```
# Enabling automatic login
  AutomaticLoginEnable = true
  AutomaticLogin = ubuntu
  ```   
Reboot the pi and log in via your VNC client.
## ZeroTeir ##
Next is optional, but I always add my ZeroTeir network. (Its simply a small VPN - Virtual Private Network - a secure tunnel over any network, including the Internet)    

I access all my local and remote Pis (and a few Windows PCs needed for Jaero etc) via ZeroTier.com and can not speak more highly of it. .  
Here is how to quickly install it on a fresh Pi:  
`curl -s https://install.zerotier.com/ | sudo bash`  
`sudo zerotier-cli join YourZeroTeirNetworkID`  
Authenticate and name this Pi by going to your network on their website then continue.  
`sudo touch /var/lib/zerotier-one/networks.d/YourZeroTeirNetworkID.conf`    
   
## VNC server
Enable cut/paste in VNC by adding ubuntu as a user in the VNC server.   
Note that you should be able to connect to this VNC server no matter what VNC client you use, TIGHTVNC or OpenVNC for exampe.

### Enable Wifi
If you must (I really don't like or trust any wifi on any Raspberry Pi. Have been burnt by its ultra poor performance far too many times) enable and join your wifi from the desktop. NOTE: this is the best way to get wifi going on DragonOS at this time - the usual Pi methods of wpa_suplicent don't work on the Dragon.
    
## *Read* the start up doc on desktop   
Be sure - this is not optional - and read the start up doc on the desktop.   
It has notes on enabling SDRPlay devices and many other DragonOS specific notes you *will* want to read.
## AERO Software - Quick start    
For L-Band work, start SDRReceiver from the terminal using your .ini file.  
`SDRReceiver -s 98w.ini`  
Start a single instance of Jaero from the DragonOS menu.   
Start many Jaeros from another terminal by making a `jaerostart.sh` file setup as follows:    
`nano jaerostart.sh` then add the following.   
```    
jaero -s VFO01 &   
jaero -s VFO02 &   
jaero -s VFO03 &   
```   
Save with ctrl+o and then exit with ctrl+x   
Add as many instances of Jaero as you need. BE SURE and turn off logging and voice decoding in each when running on a Raspberry Pi. Those two features use a lot of CPU and will cause bad/dropped decodes.   

Once you create that .sh file, make it executable by the command `sudo chmod +x jaerostart.sh`   
Then run it with `./jaerostart.sh`
    
   
## dumpxxxx quick start  
For dumpVDL2 and dumphfdl, run them from a terminal. They are not in the DragonOS menu. Just run them from the terminal prompt.

Quick and dirty guide to get you going, more to come on each of these....  

For dumpvdl2, just open a terminal on the desktop, plug in your RTLSDR v3 dongle connected to the Pi and 136mhz antenna connected and enter this command into the terminal:   
`dumpvdl2 --msg-filter all,-avlc_s,-acars_nodata,-gsif,-x25_control,-idrp_keepalive,-esis --rtlsdr 2 --gain 40 --correction -1 --output decoded:text:file:path=vdl.log,rotate=hourly 136650000 136975000 136800000`   
Then to see the messages, do a tail on the log file it creates in your home directory.   
(I don't log locally, since I use Node-RED).   
Set your gain and correction as required by your station - max gain is not always the best. Correction will depend on your dongle. The dumpvdl message headers have important information to help adjust these. More to come.   
Those are the three frequencies in use on mainland USA. Adjust them as per this [table](https://app.airframes.io/about#:~:text=you%20receive%20traffic.-,VDL%20(VHF%20Data%20Link),-We%20currently%20support) and your location (note, you might need more than three, but don't add them needlessly as the more you scan, the more the CPU is taxed. Also note that I don't use acarsdeco2 and can not help with that program, dumpvdl2 works better for my needs and has a richer output).   
If you want to feed a website or Node-RED:   
`dumpvdl2 --msg-filter all,-avlc_s,-acars_nodata,-gsif,-x25_control,-idrp_keepalive,-esis --rtlsdr 2 --gain 40 --correction -1 --output decoded:text:udp:address=thebaldgeek.net,port=xxxxx 136650000 136975000 136800000`
Where xxxxx is the port number of the website.   
My URL is there as an example, but it could be an IP address of a local computer on your network or even localhost if you are running Node-RED on the same PC.

For dumphfdl, run the command to install the RSPlay API as per the desktop text document. Then plug in your RSP1a (or RSPlay SDR) and run the command:   
`dumphfdl --soapysdr driver=sdrplay --sample-rate 250000 8834 8885 8894 8912 8912 8927 8939 8942 8948 8957 8977 --output decoded:text:file:path=hfdl.log,rotate=hourly --device-settings rfnotch_ctrl=false,dabnotch_ctrl=false`   
Note that you might get an error the first time your run this, just press up arrow and run the command again. (It takes a moment for the SDRPlay API to start)   
Then to see your logs, you can do a tail on the log file it creates in your home directory.   
Change the HF frequencies for time of day and your location or ground stations of interest (this is a work in progress for me and I will be using Node-RED to control dumphfdl frequency sets).   

In both dump programs you can have more than `--output` option, so you can for example, log locally and forward to a website without any issues.