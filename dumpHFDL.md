# dumpHFDL - ACARS over HF Frequencies.   
   
Navigation: [home](README.md)  
   
## July 2024. This page is out of date.    
Ignore this entire page. Hit the airframes Discord server and ask about setting up HFDL there.   
   

Radio waves can go a long way on HF. Its also cheaper than satellite data.   
HFDL stands for "High Frequency Data Link".
    
## Antenna   
HF antennas, longer is better than shorter. End fed long wire, active loop or HF whip on a very good ground plane for example.  

## SDR
Airspy or SDRPlay devices (ie RSP1a).   
Airspy is more stable, the SDRPlay API is a known CPU hog and very crash prone, that said a ton of people are using the RSP1a with a Raspberry Pi 4 (forget about using any CPU lower than a Pi 4 on HFDL - its pretty CPU intense - and on the Pi 4, don't scan too much, its very easy to overwhelm the CPU and or USB port and drop samples - keep reading).   
Some people have tried using the RTLSDR v3 in HF mode, its very deaf on HF and they were not happy with the performance even at the price.   
Some have also tried using an up converter on the front of them and were frustrated needing to add/subtract an offset required to all the HFDL ground station frequencies.

## Build from source or DragonOS    
If you just want to get up and running install DragonOS and dumpHFDL is built ready to go.   
Note that dumphfdl does not have any graphics to display, its all run from the command line, so you wont find it in the menu of DragonOS, just open a terminal and run the commands or the script you make.    

If you want to run Raspberry PiOS, get the 32 bit desktopless version. Since there is no GUI, there is no need for the wasted CPU cycles of a desktop. Go lean and mean.    
    
### Build from source   
You will need libacars so lets get the dependencies and get that built.   

    sudo apt install build-essential cmake pkg-config libglib2.0-dev libconfig++-dev libliquid-dev libfftw3-dev g++ libpython3-dev python3-numpy swig zlib1g-dev libxml2-dev
    cd ~
    git clone https://github.com/szpajder/libacars 
    cd libacars
    mkdir build
    cd build
    cmake ../
    make -j4
    sudo make install; 
    sudo ldconfig

Ok now we need SoapySDR, so lets build that.

    cd ~
    git clone https://github.com/pothosware/SoapySDR.git   
    cd SoapySDR
    mkdir build   
    cd build   
    cmake ..   
    make -j4   
    sudo make install   
    sudo ldconfig #needed on debian systems   


Ok now you need to install the Soapy driver for your SDR, if you are using an Airspy, Google it, sorry, cant help.   
If you are using an SDRPlay device, here is how to install their API/driver (this is for a Pi (ARM) use your CPU file (try dropping the '-ARM-' from the file name here) from SDRPlay if on x86)   

    cd ~
    wget https://www.sdrplay.com/software/SDRplay_RSP_API-ARM-3.09.1.run   
    chmod 755 ./SDRplay_RSP_API-ARM-3.09.1.run  
    ./SDRplay_RSP_API-ARM-3.09.1.run  
    git clone https://github.com/pothosware/SoapySDRPlay  
    cd SoapySDRPlay/  
    mkdir build  
    cd build  
    cmake ..  
    sudo make install  

You can test and see if it finds your SoapySDR with `SoapySDR --find`   
Also `SoapySDR --info` is helpful at times.   
You can search for a specific device with something like: `SoapySDRUtil --find "driver=sdrplay"`  Just swap out the driver for your SDR hardware.

Ok, now lets build dumphfdl  

    cd ~  
    git clone https://github.com/szpajder/dumphfdl.git  
    cd dumphfdl/  
    mkdir build  
    cd build  
    cmake ../  
    make  
    sudo make install  

And we are done.   
Lets test it out   
`dumphfdl --soapysdr driver=sdrplay --sample-rate 250000 8834 8885 8894 8912 8927 8939 8942 8948 8957 8977`

You may or may not get any hits on those ground station frequencies depending on your antenna and time of day and it could take many many minutes for something to show up, so take a breath or just keep pounding onwards with the autoscan script.....   

When (not if, when) the sdrplay_api hangs up, you can kill it with `sudo systemctl stop sdrplay.service` and wait a solid 30 seconds (no, not kidding, its a mess and it takes time to die, if you restart it too quick you will need to do a full reboot) and then start it again with `sudo systemctl start sdrplay.service`. Yes, I know about the 'restart' option, but that does not wait the 30 seconds and thus messes things up more than it helps.   
Here is a little script I call `restartapi.sh` make it by doing `nano restartapi.sh` then copy in the following:   

    sudo kill $(ps -e | grep dumphfdl | awk '{print $1}')
    sudo systemctl stop sdrplay
    sudo pkill sdrplay_apiService
    sudo rm -f /dev/shm/Glbl\\sdrSrv*
    sudo systemctl start sdrplay
 
 Save with ctrl+o, then enter, then ctrl+x
 Then make it runable with `chmod 766 restartapi.sh` now you can run it anytime with `sudo ./restartapi.sh` or even put in your sudo crontab to run every few hours.


## Auto Scan Script   

This - like a lot of stuff in the avgeek world it seems - is very contentious.... So its not a must do thing... But take a read and give it a moments consideration.   

In short, in the early dumphfdl days we ran one set of frequencies at daytime and one at night (HF propagation follows the sun - roughly). That manual switching got old real quick and so was quickly automated to switch between banks of ground station frequencies.  
Then we started to dig into the bands and global locations and people asked constantly what two banks they should use for their location... So this auto scan script came into play. Was massively crowed sourced and edited and here we are.   
We now have a script that will allow dumphfdl to run on a Pi4 and auto select one of 5 banks of frequencies every hour.   
In short, it listens to each bank for a default of 2 minutes (but can be adjusted), counts (scores) how many messages of each type it hears and then at the end of the 10 minutes parks itself on the highest scoring bank for the remaining 50 minutes then does the scanning and scoring again at the top of the hour (or what ever you set the cronjob to run the script to be).    
Why is that contentious then? Sounds perfect right? Well, avgeeks know best and if that is not how you want to run your station, then don't run the script or edit it to suit your needs. No hard feelings - honest.   
     
To run the script use `./scriptname.sh`
   
### Auto scan warning   
If you are going to edit things, do so carefully.  
The five groups have been very carefully chosen to not overload the Pi 4. If you are running on something beefier, then you can open things up.   
You can of course just comment out an entire group and not scan it.   
    
Ok, here is the script:    
[https://github.com/wiedehopf/hfdlscript/blob/main/hfdl.sh](https://github.com/wiedehopf/hfdlscript/blob/main/hfdl.sh)  
Read the comments at the start.   
Tweak the feeds as you need.   
If your pi username is not 'pi', then change the pathing in the script to suit your username.  
Do note that you can add more --output feeds, so you can feed your own VRS and your mates for example.   
You can also feed the ACARS to airframes.io (please and thanks) and your own local Node-RED for logging and live dashboards for example. Also each feed can be a different type, so JSON for one or text for the other is Ok.

## VRS   
If you want to feed your dumphfdl positions to your local VRS you can.   
DO NOT FEED to a global feed or to any of the ADSB sites. Its not the same as ADSB!!!  
Just configure a receiver location or use your current local one, being HF, it does not need to be very accurate.   
Add a basestation feed.   
I prefer to add a port and use 'client' (not the 'server' that is in the example) in the dumphfdl config.   
Tick the 'is SatCom' so the aircraft hang around (hfdl like satcom only report now and then, if you don't plot longer, the aircraft drop off the map very quick - you can adjust the dwell time in the VRS settings under Jaero timeout.)    
Lastly, its CRITAL that each feed to VRS be on a unique port. You can NOT feed more than one dumpHFDL (or more of any basestation feed) to the same port on VRS. So each command for dumphfdl must have a unique port number in that command and the port number must match on VRS. Simply make a merged feed on VRS for all your dumpHFDL feeds.


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>