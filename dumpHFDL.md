# dumpHFDL - ACARS over HF Frequencies.   
   
Navigation: [home](README.md)  

Radio waves can go a long way on HF. Its also cheaper than satellite data.   
HFDL stands for "High Frequency Data Link".

## Antenna   
HF antennas, longer is better than shorter. End fed long wire or HF whip on a very good ground plane for example.  

## SDR
Airspy or SDRPlay devices (ie RSP1a).   
Airspy is more stable, the SDRPlay API is a known CPU hog and very crash prone, that said a ton of people are using the RSP1a with a Raspberry Pi 4 (forget about using any CPU lower than a Pi 4 on HFDL - its pretty CPU intense - and on the Pi 4, don't scan too much, its very easy to overwhelm the CPU and drop samples - keep reading).   
Some people have tried using the RTLSDR v3 in HF mode, its very deaf on HF and they were not happy with the performance even at the price.   
Some have also tried using an up converter on the front of them and were frustrated needing to add/subtract to the offset required to all the HFDL ground station frequencies.

## Build from source or DragonOS    
If you just want to get running quick install DragonOS and dumpHFDL is built ready to go.   
Note that dumphfdl does not have any graphics, its all run from the command line, so you wont find it in the menu of DragonOS, open a terminal and run the commands or the script you make.    

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

    git clone https://github.com/pothosware/SoapySDR.git   
    mkdir build   
    cd build   
    cmake ..   
    make -j4   
    sudo make install   
    sudo ldconfig #needed on debian systems   

Ok now you need to install the Soapy driver your SDR, if you are using an Airspy, Google it, sorry, cant help.   
If you are using an SDRPlay device, here is how to install their API/driver (this is for a Pi (ARM) use your CPU file from them if on x86)   

    wget https://www.sdrplay.com/software/SDRplay_RSP_API-ARM-3.09.1.run   
    chmod 755 ./SDRplay_RSP_API-ARM-3.09.1.run  
    ./SDRplay_RSP_API-ARM-3.09.1.run  
    git clone https://github.com/pothosware/SoapySDRPlay  
    cd SoapySDRPlay/  
    mkdir build  
    cd build  
    cmake ..  
    make install  
You can test and see if it finds your SoapySDR with `SoapySDR --find`   
Also `SoapySDR --info` is helpful at times  

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

## Auto Scan Script   

This - like a lot of stuff in the avgeek world it seems - is very contentious.... So its not a must do thing...   
In short, in the early dumphfdl days we ran one set of frequencies at daytime and one at night (HF propagation follows the sun - roughly). That manual switching got old real quick and so was quickly automated to switch between banks of ground station frequencies. Then we started to dig into the bands and global locations and people asked constantly what two banks they should use for their location... So this auto scan script came into play. Was massively crowed sourced and edited and here we are.   
We now have a script that will allow dumphfdl to run on a Pi4 and auto tune 5 banks of frequencies every hour.   
In short, it listens to each bank for a default of 2 minutes (but can be adjusted), counts (scores) how many messages of each type it hears and then at the end of the 10 minutes parks itself on the highest scoring bank for the remaining 50 minutes then does the scanning and scoring again.    
Why is that contentious then? Sounds perfect right? Well, avgeeks know best and if that is not how you want to run your station, then don't run the script or edit it to suit your needs. No hard feelings - honest.   
   
### Auto scan warning   
If you are going to edit things, do so carefully.  
The five groups have been very carefully chosen to not overload the Pi 4. If you are running on something beefier, then you can open things up.   
You can of course just comment out an entire group and not scan it.   
    
Ok, here is the script:    
[https://github.com/wiedehopf/hfdlscript/blob/main/hfdl.sh](https://github.com/wiedehopf/hfdlscript/blob/main/hfdl.sh)  
Read the comments at the start.   
Tweak the feeds as you need.   
If your pi user is not 'pi', then change the pathing in the file to suit your username.  
Do note that you can just add more --output feeds, so you can feed your own VRS and your mates for example.   
You can also feed the ACARS to airframes.io (please and thanks) and your own local Node-RED for logging and live dashboards for example. Also each feed can be different, so JSON or text is Ok.

## VRS   
If you want to feed your dumphfdl positions to your local VRS you can.   
DO NOT FEED to a global feed or to any of the ADSB sites. Its not the same as ADSB!!!  
Just configure a location or use your current local one.   
Add a basestation feed.   
I prefer to add a port and use 'client' (not the 'server' that is in the example) in the dumphfdl config.   
Tick the 'is SatCom' so the aircraft hang around (hfdl like satcom only report now and then, if you don't plot longer, the aircraft drop off the map very quick - you can adjust the dwell time in the VRS settings under Jaero timeout.)  



<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>