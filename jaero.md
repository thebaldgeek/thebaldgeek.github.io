# Ins and outs of Jaero.   
   
Navigation: [home](README.md)  

The core of this whole project is the software called Jaero.  
This page will grow over time, but as of July 2021 the most pressing thing was to document one way to build Jaero from source on a Raspberry Pi 4 (4 gig RAM version - 8 Gig SD card minium).   
## Building Jaero on Linux    
~~I started with the SDRplay image since I wanted to test both the RSP1a and the RTLSDRv3 receivers.    
Pull down the v0.7 image here: <https://www.sdrplay.com/raspberry-pi-images/>~~  
Update. I had HUGE issues with sound drivers on the SDRplay image. Spent hours and hours and never got it sorted.   
I switched to the PiSDR image and had everything working in minutes. (Note - I did not test many aloop virtual sound devices - its on my todo list).  
<https://github.com/luigifcruz/pisdr-image>  
Burn it to your Pi SD card with the usual software.   
Put it in the Pi and boot it up. Note it is not a headless install, you will need an HDMI monitor, keyboard and mouse (for the start up at any rate). You will also need a network connection to install the required software.   
Once you boot up, you can run ```sudo raspi-config``` if you like, I expand the file system and set the clock to UTC (instructions [here](raspberrypi.md)) if nothing else.    

Note that this will build Jaero version 1.0.4.11 - the last 'stable' release. The March / August 2021 versions of Jaero require a new version of QT and is it tricky to build on the Pi - also the new `ci-linux-build.sh` script has some errors in it and I could not figure out how to resolve them, so opted to build the last stable release for the Pi to test things out.  

Time to open the terminal and copy paste the following commands. Do them one at a time and let them finish before doing the next. All up should take about 15 minutes from start to finish.   
    
    sudo apt-get install libvorbis-dev   
    sudo apt-get install qt5-default  
    sudo apt-get install libqt5svg5*  
    sudo apt-get install qtmultimedia5-dev  
    sudo apt-get install libqcustomplot-dev  
    sudo apt-get install libqt5multimedia5-plugins  
    
    cd ~  
    mkdir git && cd git  
    git clone https://github.com/jontio/libaeroambe.git  
    cd libaeroambe/mbelib-master/  
    mkdir build && cd build  
    cmake ..  
    make -j4  
    sudo make install  
    sudo ldconfig  
    
    cd ../../libaeroambe/  
    qmake  
    make -j4  
    sudo make install  
    
    cd ~/git  
    wget https://github.com/jontio/JAERO/archive/refs/tags/v1.0.4.11.zip  
    unzip v1.0.4.11.zip  
    cd JAERO-1.0.4.11/libacars-1.1.0/  
    mkdir build && cd build  
    cmake ..  
    make -j4  
    sudo make install  

    cd ~/git/JAERO-1.0.4.11/libcorrect/  
    mkdir build && cd build  
    cmake ..  
    make -j4  
    sudo make install  
    sudo ldconfig  


    cd ~/git/JAERO-1.0.4.11/JAERO/  
    qmake  
    make -j4  
    sudo make install  
   
   
You will find Jaero in the 'Internet' menu option of the Pi menu.  
Here we are using SDRangel to feed a 10500 downlink channel into Jaero.  
  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/jareoonlinux.PNG" height="580">  
     
Not a lot to see really, but 10s and 10s of hours went into this screenshot.  
## Jaero on Windows   
Use the March 1.0.4.12 and the August 1.0.4.13 Alpha versions, you don't need to install it, just run it from the directory you unzip it from. This version fixes the local time stamp and uses UTC instead. It also allows you to use BaseStation.sqb for its logging aircraft database lookup. The 1.0.4.13 of Jaero adds the ZMQ input for data. You should be using at lest this version.   
    
basestation.sqb. This is a pseudo 'standard' of aircraft details database. As Jaero decodes aircraft messages, it looks up each ICAO (Jaero calls them AES) in the database and provides type and owner information in its log file. If you are going to use Node-RED to track the aircraft, skip this step.   
The basestation.sqb file that this version of Jaero includes has around 188,000 aircraft details, but we can quickly do better.    
Visit the flightairmap page and download their basestation.sqb file: <https://data.flightairmap.com/>  
The link is at the bottom of that page.   
Unzip it on your computer and copy the file to your Jaero subdirectory and replace (over write) the one in there. The flightairmap database has 380,000 aircraft, so almost double the chances of Jaero showing the information for any satcom ACARS messages you decode.   
If you are using Node-RED I will walk you through building an even larger database with around 558,000 aircraft details. Or you can get creative and modify your own database to use with Jaero.    
    
Once you have copied the database over, you can now double click Jaero and run it.   
But lets just do one more tweak for those of you running standalone (ie, no Node-RED).   

### Jaero Log Link   
Click on the gear icon, then click on the second tab in the settings, the 'Log Window'.   
Here you will see the link that will be opened in your web browser when you click on the aircraft drawing in the Jaero log.   
Out of the box it is set to: `http://www.flightradar24.com/data/airplanes/{REG}`  
This is Ok for some people, but many would rather it open to ADSBExcahnge, good news, we can change it.    
Delete the fightradar24 link and replace it with: `https://globe.adsbexchange.com/?icao={AES}`   
Now when you click on that drawing (and first highlighting the aircraft of interest in the Jaero log list), you will open that aircraft last known position on the ADSBExchange map.   
If you are going to be using Node-RED, I will show you how to make those links in a function node so we can skip this step.