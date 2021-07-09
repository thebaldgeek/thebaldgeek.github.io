# Ins and outs of Jaero.   
   
Navigation: [home](README.md)  

The core of this whole project is the software called Jaero.  
This page will grow over time, but as of July 2021 the most pressing thing was to document one way to build Jaero from source on a Raspberry Pi 4 (4 gig RAM version - 8 Gig SD card minium).   
    
~~I started with the SDRplay image since I wanted to test both the RSP1a and the RTLSDRv3 receivers.    
Pull down the v0.7 image here: <https://www.sdrplay.com/raspberry-pi-images/>~~  
Update. I had HUGE issues with sound drivers on the SDRplay image. Spent hours and hours and never got it sorted.   
I switched to the PiSDR image and had everything working in minutes. (Note - I did not test many aloop virtual sound devices - its on my todo list).  
<https://github.com/luigifcruz/pisdr-image>  
Burn it to your Pi SD card with the usual software.   
Put it in the Pi and boot it up. Note it is not a headless install, you will need an HDMI monitor, keyboard and mouse (for the start up at any rate). You will also need a network connection to install the required software.   
Once you boot up, you can run ```sudo raspi-config``` if you like, I expand the file system and set the clock to UTC if nothing else.    

Note that this will build Jaero version 1.0.4.11 - the last 'stable' release. The March 2021 version of Jaero requires a new version of QT and is it tricky to build on the Pi - also the new `ci-linux-build.sh` script has some errors in it and I could not figure out how to resolve them, so opted to build the last stable release for the Pi to test things out.  

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