# Radiosonde - Weather Balloon Tracking.   
   
Navigation: [home](README.md)  

Radiosondes or weather balloons are launched around twice a day from a lot of different locations around the world.  
You can quickly visit https://sondehub.org and find your location and see what flights are going on around you. Zoom out and find the little gray circle that is a launch site (usually near or on large airports) and then right click on the circle and check out the frequency of launches and the history of flights from that site.  

Its a lot of fun to track these flights and then sometimes you can go to where they land and recover the sondes (scoring yourself a little GPS, temperature/humidity sensor and 400Mhz transmitter - many of which can run modified firmware and pressed into other uses.)   
This page is less about the chasing and recovering the sonde (there are many websites and Facebook groups dedicated to that aspect of the hobby) and more about setting up the station and getting more station centric data from the payload data stream.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/radiosonde/recovery3.jpg" height="320">   
   

## Software -> auto_rx     
There are a few different sonde decoder software packages, some for Windows, some for Linux, a quick Google search can guide you on them, this page is going to focus on the Linux only 'auto_rx' package.   
You can run auto_rx on a Raspberry Pi 3/4 or x86 computer running Ubuntu or Debian. (Other distros might be possible, but I don't have any experience on them).   
The auto_rx people have done a great job writing up the code and installation guide, you can visit the wiki here: https://github.com/projecthorus/radiosonde_auto_rx/wiki    
Some notes: I am not a fan of docker, so usually go with the native build. One comment on Docker.... You can not install their Docker container on an x86 computer, the Docker 'image' is CPU architecture specific and its been built only for the Raspberry Pi CPU so you will get an error trying to run their Docker container on anything else.   
The wiki native install guide is very clear and results in a smooth install.   
I recommend getting up and running with just the one RTLSDR v3 dongle at first. Do note that while the Airspy Mini and R2 SDR's are supported, its somewhat more complicated and fragile to get and keep running and so I have not ventured into those hardware platforms.    
Also note that things like RSP1a, HackRF and other such SDR's are not supported, only the NooElec and RTLSDR type receivers are supported at this time.   
At this time you can leave the SDR at its default serial of usually 00000001 or what ever serial you have changed it to. You will need to know its sn# as part of the install so make note of it when you get to the step of running `rtl_test`.    
    
## Hardware    
Depending on how far away the sondes tend to float past your location will depend on the antenna you will need to hear their signal.   
If you are very close by, a simple indoor vertical whip might be enough to get your first bit of data, but most people reading this want to push their range a bit more and so will run an outdoor antenna. There are only a few off the shelf options here. The sondes in use in North America transmit between 400Mhz and 406Mhz. There are not a lot of off the shelf antennas that cover this range. (A lot more will be said about antennas further down the page). And yes, you are quite right, the discone will cover that range, but please keep reading....   
A lot of people get started with a ham radio dual band 70cm/2m vertical. Many also press a typical wide band 'scanner' vertical antenna into use, and all are fine starter antennas.
The SDR is pretty much pre-chosen for us, the blue ADSB dongles are no good, they have a filter in them that will reject the sondes signal. The orange 978 or 1090 dongles are ok, they have an amplifier and no filter, so that will get you running Ok as well. The RadarBox airband dongle is so deaf at every frequency known that most have given up on them.  

Coax is not too critical at 400Mhz. Many use good quality 75 Ohm tv coax.   
    
LNA. There is no question a good quality LNA mounted at the antenna will make a huge difference in the range and amount of data packets you decode from any given flight.   
While you can use a general wide band LNA that are very cheap and popular, a filtered LNA will always bring better results.    
https://store.uputronics.com/index.php?route=product/product&product_id=54   
This is the current popular LNA for radiosonde work, there is talk of a new sonde specific LNA in the works, but it has not been released yet.
     
Ok, now that we have an outdoor antenna mounted up as high as you can, quality LNA, good coax and your SDR connected to the software, we wait.    
The twice a day launches usually happen around zero and 12 UTC. But at times of unusual weather or if you live near a rocket launch site, you may catch many more flights at all times of the day or night.   
Jan 2023 we had some nasty weather in California and my station logged the following flights over about 24 hours.    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/radiosonde/badweather.png" height="420">   
     
## station.conf file tweaks     
We will now review the auto_rx station.conf file.
I use nano to edit mine, you can use what ever your comfortable in.   

The first thing to consider is the gain settings.   
Most people run AGC or -1. These are the valid RTL gain values:    
```
# SDR Gain Setting
0.0 0.9 1.4 2.7 3.7 7.7 8.7 12.5 14.4 15.7 16.6 19.7 20.7 22.9 25.4 28.0 29.7 32.8 33.8 36.4 37.2 38.6 40.2 42.1 43.4 43.9 44.5 48.0 49.6
```
I usually copy these into the file at the gain setting area to keep them handy.   
Be sure and set `bias = True` if you need your SDR to power the LNA. Be sure and use an SDR that has a Bias-T output and is powerful enough to drive the LNA.
One of the best ways I have found to find the best gain for your setup is to plug the dongle into a laptop and run some SDR software to see the sonde signal during a flight and then just adjust the gain for the best signal to noise and make a note of the that gain value and then put it in the station.conf file and restart auto_rx.    
This can be tricky if you don't have a laptop and are running a headless Pi.   
In this case, careful notes and some experimentation over time will be required.   
    
Next up down the .conf file is the sonde frequency settings.    
Be sure and look at the notes in the file and set your mix and max frequencies to follow the advice.   
    
Next up is the only/never/always scan section.   
Since I see some common spikes in my area that never seem to go away unless I disconnect the antenna I have added those to the never_scan section, but before you do that, I suggest you make careful note for a few weeks of all the sonde frequencies in use in your area to make sure you don't accidentally add one of those to the never_scan list.  
The list should be comma separated, something like this (don't use these!):   
 ```
never_scan = [403.2,403.06,405.76,401.92,404.97]
```   
If you don't have more than about 5-8 constant spikes, there is probably no need to record them and lock them out.   
    
Next is station location.   
Its very important to fill out this section, but as it says in the comments, it does not have to be super accurate.   
A nearby cross road is fine. I find the alt to be important and helpful. It should be in meters and include your antenna hight.   
The section 'Uploader Antenna Description' will be what shows up on your station on sondehub website, so make it friendly and helpful.    

Thats the critical sections that need to be tweaked.   
I find the email notifications helpful and enjoy them, note you should use a throw away or 'computer only' email address here, not your main one and you should be using two factor application specific passwords in this section. Lots of docs on how to set that up.   
(If I get time I will show how I use Telegram via Node-RED for my launch notifications).   

## Single SDR Operation    
auto_rx will now start scanning the frequency range you have specified and any peaks will be analyzed for a short time to see if they contain any of its known sonde type modulated data. If so, the first data packets it finds it will stop scanning and just listen to that one frequency to decode the data.   
It will camp on that frequency till the sondes signal drops below your noise floor for 180 seconds (adjustable and we will talk about it in a moment).   
Once the 180 second timer is up, the SDR will go back into scan mode.   
Over the space of a few weeks while you get the feel for the flight pattern you will find if you have the chance to hear more than one sonde at a time.   
If so, its time for.....

## More SDRs. More sonde flights    
If you are lucky enough to live in an area that see's perhaps a few sondes a day, you might like to add more SDR's to your setup.  
    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/radiosonde/4sdrandsplitter.png" height="580"><img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/radiosonde/4sdrsinhub.png" height="580"><img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/radiosonde/44sdrsaplitter.png" height="580">    
    
You can go with 2 or more SDR's. As many as you have signal strength to drive through the 3db to 6db of loss that the splitter introduces
A critical aspect of running more than one SDR is to set the serial numbers. Here is how to do that.....    
    
First, stop auto_rx from running. (how you do this will depend on how you installed it and are running it).  
Unplug all your SDRs but one.   
Now, from the Linux command prompt, enter: `rtl_test` and see if your computer sees just the one SDR plugged in and that its not in use.   
Hit CTRL + C to stop that running.   
Now enter `rtl_eeprom -s 401` and hit enter.  
Answer Y and see that your new serial number as been applied by running `rtl_test` again and checking the SN#.   
Hit CTRL + C to top that running.   
So we chose 401 for 400Mhz and 1 because the SDR's are numbered 1,2,3,4 etc in auto_rx.   
Unplug that SDR and mark it clearly with '401' and plug in the next.   
Now, from the Linux command prompt, enter: `rtl_test` and see if your computer sees just the one SDR plugged in and that its not in use.   
Hit CTRL + C to stop that running.   
Now enter `rtl_eeprom -s 402` and hit enter.  
Answer Y and see that your new serial number as been applied by running `rtl_test` again and checking the SN#.   
Hit CTRL + C to top that running.   
Set that SDR aside and make it '402' clearly.   
You get the flow now, so do the next two SDR's and make them '403' and '404'.    
Ok, now plug all 4 into your powered USB hub and plug it into the computer and issue the command `rtl_test` and make sure all 4 show up.   
We are almost ready to go....    
Note which port on your splitter has the power pass.   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/radiosonde/4waytvsplitter.jpg" height="580">   
Note in this photo of my splitter it is the port on the very left. What ever SDR Sn you put  SDR you will need to ensure has the bias-t turned on to run your LNA. Note which serial number you put in there so you can set the `bias = True` command in the station.conf file with the correct SDR.   
My 4 SDR station .conf looks like this:    
```[sdr_1]
device_idx = 401
ppm = 0
# SDR Gain Setting
# 0.0 0.9 1.4 2.7 3.7 7.7 8.7 12.5 14.4 15.7 16.6 19.7 20.7 22.9 25.4 28.0 29.7 32.8 33.8 36.4 37.2 38.6 40.2 42.1 43.4 43.9 44.5 48.0 49.6
#gain = -1
gain = 40.2
bias = True

[sdr_2]
# As above, for the next SDR, if used. Note the warning about serial numbers.
device_idx = 402
ppm = 0
#gain = -1
gain = 40.2
bias = False

[sdr_3]
# As above, for the next SDR, if used. Note the warning about serial numbers.
device_idx = 403
ppm = 0
#gain = -1
gain = 40.2
bias = False

[sdr_4]
# As above, for the next SDR, if used. Note the warning about serial numbers.
device_idx = 404
ppm = 0
#gain = -1
gain = 40.2
bias = False```

Note I put the AGC on comment so I can test either setting pretty quick.   
I also updated my station antenna description to reflect that Im using 4 SDR's.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/radiosonde/4sdrandmap.png" height="320">

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/radiosonde/4sdrdecode.png" height="320">
  
The order of operations for auto_rx now becomes something like this.   
The lowest SN SDR will be scanning. When it finds a peak with sonde data on it, it passes it off to the next highest SN SDR and goes back to scanning.   
If it finds another it will check if the next highest SN is already decoding, if so, it passes it up to the next highest serial number and goes back to scanning.  
If all three are decoding and it finds another sonde to decode, it will stop scanning and start decoding with no more SDR's left, your station can not scan for a 5th or more sondes till one of the current decoding SDR's timeouts.  
This timeout is adjustable just under the min and max frequency setting:   
```rx_timeout = 900```  
Its default is 180 seconds, you can see I have bumped it up since I have 4 SDRs I can afford to keep listening to each sonde longer before giving up and going back in the 'not tasked' pool and wait for the 'scanning' SDR to hand it a task.  
This time extension is also helpful for me as there are lot of mountains around my location and the sondes will drop into my noise floor while they go behind a peak.