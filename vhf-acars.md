# Aircraft Communication Addressing and Reporting System. #    
   
Navigation: [home](README.md)  
 
ACARS is the messaging system that allows aircraft talk to and from the ground staff / systems.   

There are two main ACARS modes on VHF.    
ACARS between 129 Mhz and 131 Mhz    
VDL2 between 136.6 Mhz and 136.9 Mhz    
Roughly you can think of ACARS as slightly older analog and VDL2 as digital.    
    
The two different modes are in use to different amounts all over the world, its imposable for us (yet - the data will soon be there for us to say with more confidence) to tell you which to pick for your location. I suggest that you  install both packages, run both for a week and compare numbers for your location. Perhaps, like me in California, both have high message rates and you will end up running a few SDR dongles. (I run 3 in the one Pi 3).   
The other 'fun' part here is that if the full spread of ACARS frequencies are in use in your location, it will be too wide for a single RTLSDR bandwidth, so if they are and you want to catch all the data (please and thank-you), then you will need to run two dongles, a lower set of frequencies on one and the higher set on the other.   
So, a full setup might consist of 2 x ACARS SDR and 1 x VDL2 SDR.
    
## Hardware BOM (Bill of materials)  
* 1 x Antenna. There are some options here. Some have used an old ham 2m antenna, others a 'scanner' antenna. Ovoid a discone, they are very low gain. If you want the best, then the [PDP ACARS](https://dpdproductions.com/collections/aviation-base-mobile-antennas/products/acars-vertical-outdoor-base-antenna) antenna is the one to get. Here is an example of what NOT to buy. This airband antenna is BROKEN! [Amazon](https://www.amazon.com/dp/B07XNKX18D?ref_=cm_sw_r_ud_dp_QW7K7EJXCSYNG1BKXQTY) Note that you can NOT use your existing ADSB one, the frequencies are not even close.  
* 1 x coax cable, length for your installation. The good thing here is the frequency of ACARS is much lower than ADSB, so the coax loss is much lower. 
A good starter is [RG-8x](https://www.amazon.com/s?k=rg-8x&crid=3QO4RHETIF7KL&sprefix=rg-%2Caps%2C212&ref=nb_sb_ss_ts-doa-p_7_3), a bit more harder to work with is [RG-213](https://www.amazon.com/s?k=rg-213&crid=2LGFNZMSJ9TVW&sprefix=rg-213%2Caps%2C126&ref=nb_sb_noss_1). ADSBExchange sell a range of coax cable types and lengths [Store](https://store.adsbexchange.com/collections/all)     
 Since its receive only, you can use good quality 75 ohm cable if you like [Amazon](https://www.amazon.com/s?k=75+ohm+outdoor+coax+cable&ref=nb_sb_noss)    
* 1 x SMA splitter. You will need to split your antenna into 2 (or 3) SDRs if you plan to run both ACARS and VDL. [Amazon](https://www.amazon.com/Bingfu-Antenna-Splitter-Cellular-Amplifier/dp/B07STYNB6V/) This will get you started, if you need to split further, just look for the right combo of SMA male/female.    
* 1 or 2 or 3 x SDR. [RTLSDRv3](https://www.amazon.com/RTL-SDR-Blog-RTL2832U-Software-Defined/dp/B0129EBDS2/) or you can go for the [Orange ADSBEx](https://store.adsbexchange.com/products/adsbexchange-com-orange-r860-rtl2832u-0-5-ppm-tcxo-sdr-w-amp). Do NOT use the blue dongles, they are filtered for ADSB and will not work on VHF-ACARS.   
 * 1 x Raspbery Pi. You can use your existing ADSB Pi (Check the CPU load first), or put in a new Pi.  
 * 1 x USB Powered Hub. If you end up using 3 ACARS dongles and your ADSB dongle (and perhaps a 978 dongle) on the same Pi, you will need to run a powered hub.  

Note, be very careful about running an LNA. ACARS is close to the FM band and you may overload the front of the SDR and make things worse. Look at your SDR waterfall software if you can to see what the RF interference in your area is like and see how well you are picking up the ACARS/VDL bursts. I personally have had both success and failure running the [GPIO filtered airband LNA](https://gpio.com/products/airband-filtered-low-noise-amplifier?variant=19591697301526). In one location it was great and made a worthy addition, in another it made the signal useless. It was an expensive test. Your milage may vary.  

## Software   
There is one supported decoder for ACARS and two decoders for VDL2. All of which only run on Linux. (There are some Windows options, Blackcat and MultiPSK, both are outside the scope of this page - neither of them can feed airframes.io).   
If you know and love docker, then there that option as well [SDR Enthusiasts](https://github.com/sdr-enthusiasts) is a good way to combine your ADSB data with your ACARS data in your location.

[acarsdec](https://github.com/TLeconte/acarsdec) is a multi-channel acars decoder with built-in rtl_sdr, airspy front end or sdrplay device.   
[vdlm2dec](https://github.com/TLeconte/vdlm2dec) can decode up to 8 frequencies simultaneously ( but in the same 2Mhz range ) It decodes ARINC-622 ATS applications (ADS-C, CPDLC) via libacars library.    
[dumpvdl2](https://github.com/szpajder/dumpvdl2) Has the following features: 
* RTLSDR (via rtl-sdr library)
* Mirics SDR (via libmirisdr-4)
* SDRPlay RSP (native support through official driver version 2 and 3)
* SoapySDR (via soapy-sdr project)
* prerecorded IQ data from a file
* Decodes multiple VDL2 channels simultaneously
* Automatically reassembles multiblock ACARS messages, MIAM file transfers, fragmented X.25, CLNP and COTP packets.
* Supports various outputs and output formats (see below)
* Enriches logged messages with ground station details read from a text file (MultiPSK format)
* Enriches logged messages with aircraft data read from Basestation SQLite database
* Supports message filtering by type or direction (uplink, downlink)
* Can store raw frames in a binary file for later decoding or archiving purposes.

[Airframes.io](https://app.airframes.io/about) supports feeds from all three, personally I like dumpvdl2 as it has a much richer output that I find very helpful (noise floor and signal data just to name two).    

## Building / Installing the Software  
If you just want to get going - and who doesnt... just go here and run the script you want....   
- https://app.airframes.io/about
- https://github.com/sdr-enthusiasts
- https://github.com/wiedehopf/adsb-wiki/wiki/acarsdec-install
- https://github.com/wiedehopf/adsb-wiki/wiki/vdlm2dec-install
- https://github.com/wiedehopf/adsb-wiki/wiki/dumpvdl2-install   
   
You can script the following commands, but I like to copy paste each one to ensure it runs without error.    
If you are installing on an existing ADSB setup, you can skip the first part since you already have the SDR drivers installed and working.  

No matter if you have an existing ADSB or clean install, the first step is to update your system and install the required packages. 
All the following need to be done as root, so lets become sudo....  
`sudo su`   

`apt-get update `   

`apt-get install -y cmake rtl-sdr git cmake libusb-1.0-0-dev libtool librtlsdr-dev build-essential libglib2.0-dev pkg-config librtlsdr-dev libxml2-dev libzmq3-dev python3-zmq zlib1g-dev libxml2-dev`    

`ldconfig`  

If you have SDR software installed all ready, skip this section.  
`cd /usr/src`  
`git clone git://git.osmocom.org/rtl-sdr.git`  
`cd rtl-sdr`  
`mkdir build`  
`cd build`  
`cmake ../ -DINSTALL_UDEV_RULES=ON -DDETACH_KERNEL_DRIVER=ON`  
`make -j3`  
`make install`  
`ldconfig`  
`cd /usr/src/rtl-sdr`  
`cp rtl-sdr.rules /etc/udev/rules.d/`  
  
Now we install the libacars package. This is needed to decode the rich ACARS messages like ARINC622.    
`cd /usr/src`  
`git clone --depth=1 https://github.com/szpajder/libacars`  
`cd libacars`  
`mkdir build`  
`cd build`  
`cmake ../`  
`make -j3`  
`make install`  
`ldconfig`  
   
Now lets install the acarsdec package.  
`cd /usr/src`  
`git clone --depth=1 https://github.com/TLeconte/acarsdec.git`  
`cd acarsdec`  
`mkdir build`  
`cd build`  
`cmake .. -Drtl=ON`  
`make -j3`  
`make install`  

Now lets install the dumpvdl2 package.  
`cd /usr/src`  
`git clone --depth=1 https://github.com/szpajder/dumpvdl2.git`  
`cd dumpvdl2`  
`mkdir build`  
`cd build`  
`cmake ../`  
`make -j3`  
`make install`  
`cd ..`  
`cp etc/dumpvdl2.service /etc/systemd/system/`  
`cp etc/dumpvdl2 /etc/default/`  
`systemctl daemon-reload`  
   
Lastly, reboot and plug in your ACARS SDR dongle(s).  
`reboot now`  

Here is an example command to listen on a few VDL frequencies (check out [airframes.io/about](https://app.airframes.io/about) for a good list of VDL2 frequencies to listen on in your part of the world.   
   
`dumpvdl2 --rtlsdr -0 --gain 42 136725000 136775000 136800000 136975000`
    
Once you are happy with the output you can then setup dumpvdl2 to launch in the background and when the Pi boots:   
   
`sudo nano /etc/default/dumpvdl2`  
In that file, uncomment the DUMPVDL2_OPTIONS= and put your options from the test you just ran in to the file, save and exit it - it will look something like this:  
  
`DUMPVDL2_OPTIONS="--rtlsdr -0 --gain 42 --correction 7 --output decoded:text:udp:address=yourWebSite.com,port=112233 136725000 136775000 136800000 136975000"`   
   
Here is an example command line that will filter out empty system pings and handshakes:       
`dumpvdl2 --msg-filter all,-avlc_s,-acars_nodata,-gsif,-x25_control,-idrp_keepalive,-esis --rtlsdr 2 --gain 40 --correction -1 --output decoded:text:file:path=vdl.log,rotate=hourly 136650000 136975000 136800000`   
   
Here is an example command to listen on a few ACARS fequenices:   
`acarsdec -v -o 4 -g 280 -r 0 131.550 131.525 131.725 131.825 130.025 130.425 130.450 131.125`   
   
Once you have your mode up and decoding to the terminal, then you can feed the data to airframes.io and claim your feeder (and climb the soon coming leaderboard).   
   
   Stop reading!   

 ------------  

Both vdlm2dec and dumpvdl2 can work with Node-RED. In fact they are very similar to install and use. They both output their data in JSON but only dumpvdl2 has a decoded text option.   
Part of the problem with both of them is that neither author lists all the options of the JSON keys their programs can produce in their docs, this makes it hard for me to write a Node-RED flow that can intelligently deal with unknown keys as they come across the wire. I'm sure if you dug into their code they would probably have an array somewhere in a file that lists all the possible key pairs that their program could show in an given message. I'm also sure that if you knew how to program there is probably a well known method to deal with random key pairs in your code.   

Note that vdlm2dec requires its command line frequencies to be in Mhz while dumpvdl requires them to be in Hz.   



**Feeding VDL2 data to Node-RED**    
Both programs (well, all three if you count the ACARS decoder) will take a command line option to stream the decoded message via UDP. I simply point that stream to my hostname:port and have a UDP in node listening on that port.   

I hope to add a Node-RED ACARS example flow to this page 'soon'.    

## dumpvdl ##   
Here is a partial flow will display some of the main text values that come in on a decoded text stream from dumpvdl.  
    
    [{"id":"27278a8d.356866","type":"udp in","z":"5e5fdc91.d8f9d4","name":"Uk","iface":"","port":"112233","ipv":"udp4","multicast":"false","group":"","datatype":"utf8","x":2040,"y":1380,"wires":[["85112668.5314d8","63e7b7fa.3dbca8","ae622b78.e1ec48","ae6e4362.9c512","a4d431d5.84261"]]},{"id":"85112668.5314d8","type":"msg-speed","z":"5e5fdc91.d8f9d4","name":"","frequency":"min","estimation":false,"ignore":false,"x":2210,"y":1380,"wires":[["dd053c0a.85401"],["b01b47b.d90c2b8","9a9f2355.0e9eb"]]},{"id":"b01b47b.d90c2b8","type":"switch","z":"5e5fdc91.d8f9d4","name":"frequency counter","property":"payload","propertyType":"msg","rules":[{"t":"cont","v":"136.725","vt":"str"},{"t":"cont","v":"136.775","vt":"str"},{"t":"cont","v":"136.800","vt":"str"},{"t":"cont","v":"136.975","vt":"str"},{"t":"else"}],"checkall":"false","repair":false,"outputs":5,"x":2450,"y":1340,"wires":[["7e35bf77.81579"],["bddb221b.8cf9d"],["fa937852.523268"],["4ca4ddca.ab0714"],[]]},{"id":"7e35bf77.81579","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1260,"wires":[["ebf306d.eeed3f8"]],"l":false},{"id":"bddb221b.8cf9d","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1300,"wires":[["dd625424.044428"]],"l":false},{"id":"63e7b7fa.3dbca8","type":"debug","z":"5e5fdc91.d8f9d4","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":2210,"y":1460,"wires":[]},{"id":"fa937852.523268","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1340,"wires":[["b09868e3.aa1528"]],"l":false},{"id":"4ca4ddca.ab0714","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1380,"wires":[["927bfee8.ebf32"]],"l":false},{"id":"dd053c0a.85401","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":2,"width":1,"height":1,"name":"","label":"msg per min: ","format":"{{msg.payload}}","layout":"row-left","x":2458,"y":1227,"wires":[]},{"id":"927bfee8.ebf32","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":7,"width":2,"height":1,"name":"","label":"136.975 = ","format":"{{msg.payload}}","layout":"row-left","x":2810,"y":1380,"wires":[]},{"id":"b09868e3.aa1528","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":5,"width":2,"height":1,"name":"","label":"136.800 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1340,"wires":[]},{"id":"ebf306d.eeed3f8","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":1,"width":2,"height":1,"name":"","label":"136.725 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1260,"wires":[]},{"id":"dd625424.044428","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":3,"width":2,"height":1,"name":"","label":"136.775 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1300,"wires":[]},{"id":"9a9f2355.0e9eb","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1420,"wires":[["8772957f.b74d78"]],"l":false},{"id":"8772957f.b74d78","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":4,"width":1,"height":1,"name":"","label":"Total: ","format":"{{msg.payload}}","layout":"row-left","x":2790,"y":1420,"wires":[]},{"id":"a38ae90b.462a58","type":"ui_group","name":"UK","tab":"733f36e1.cf5db8","order":7,"disp":true,"width":3,"collapse":false},{"id":"733f36e1.cf5db8","type":"ui_tab","name":"VHF-VDL2","icon":"flight","order":7,"disabled":false,"hidden":false}]  



- - - - 
## vdlm2dec ##  
Even though I don't use it since I cant handle the random JSON keys, here is a partial flow that displays some of the main key value pairs for vdlm2dec via JSON.    
    
    [{"id":"27278a8d.356866","type":"udp in","z":"5e5fdc91.d8f9d4","name":"Uk","iface":"","port":"112233","ipv":"udp4","multicast":"false","group":"","datatype":"utf8","x":2030,"y":1380,"wires":[["85112668.5314d8","4c65059e.1c8c4c"]]},{"id":"85112668.5314d8","type":"msg-speed","z":"5e5fdc91.d8f9d4","name":"","frequency":"min","estimation":false,"ignore":false,"x":2210,"y":1380,"wires":[["dd053c0a.85401"],["b01b47b.d90c2b8","9a9f2355.0e9eb"]]},{"id":"b01b47b.d90c2b8","type":"switch","z":"5e5fdc91.d8f9d4","name":"frequency counter","property":"payload","propertyType":"msg","rules":[{"t":"cont","v":"136.650","vt":"num"},{"t":"cont","v":"136.725","vt":"num"},{"t":"cont","v":"136.775","vt":"num"},{"t":"cont","v":"136.800","vt":"num"},{"t":"cont","v":"136.825","vt":"num"},{"t":"cont","v":"136.875","vt":"num"},{"t":"cont","v":"136.975","vt":"num"},{"t":"else"}],"checkall":"false","repair":false,"outputs":8,"x":2450,"y":1340,"wires":[["ce4baf35.883c4"],["7e35bf77.81579"],["bddb221b.8cf9d"],["fa937852.523268"],["19528aa2.bd25f5"],["3ccff35e.aac23c"],["4ca4ddca.ab0714"],[]]},{"id":"ce4baf35.883c4","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1220,"wires":[["534ea04c.ea31"]],"l":false},{"id":"7e35bf77.81579","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1260,"wires":[["ebf306d.eeed3f8"]],"l":false},{"id":"bddb221b.8cf9d","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1300,"wires":[["dd625424.044428"]],"l":false},{"id":"63e7b7fa.3dbca8","type":"debug","z":"5e5fdc91.d8f9d4","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":2150,"y":1540,"wires":[]},{"id":"fa937852.523268","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1340,"wires":[["b09868e3.aa1528"]],"l":false},{"id":"19528aa2.bd25f5","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1380,"wires":[["df38d989.ddb808"]],"l":false},{"id":"3ccff35e.aac23c","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1420,"wires":[["53a473c3.ca150c"]],"l":false},{"id":"4ca4ddca.ab0714","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1460,"wires":[["927bfee8.ebf32"]],"l":false},{"id":"dd053c0a.85401","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":17,"width":1,"height":1,"name":"","label":"msg per min: ","format":"{{msg.payload}}","layout":"row-left","x":2458,"y":1227,"wires":[]},{"id":"927bfee8.ebf32","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":19,"width":2,"height":1,"name":"","label":"136.975 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1460,"wires":[]},{"id":"534ea04c.ea31","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":1,"width":2,"height":1,"name":"","label":"136.650 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1220,"wires":[]},{"id":"b09868e3.aa1528","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":2,"width":2,"height":1,"name":"","label":"136.800 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1340,"wires":[]},{"id":"ebf306d.eeed3f8","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":7,"width":2,"height":1,"name":"","label":"136.725 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1260,"wires":[]},{"id":"dd625424.044428","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":13,"width":2,"height":1,"name":"","label":"136.775 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1300,"wires":[]},{"id":"df38d989.ddb808","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":8,"width":2,"height":1,"name":"","label":"136.825 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1380,"wires":[]},{"id":"53a473c3.ca150c","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":14,"width":2,"height":1,"name":"","label":"136.875 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1420,"wires":[]},{"id":"4c65059e.1c8c4c","type":"json","z":"5e5fdc91.d8f9d4","name":"","property":"payload","action":"","pretty":false,"x":2190,"y":1480,"wires":[["63e7b7fa.3dbca8","f8d13f15.5590c","527949ed.e9eb68","b6253ede.f08e3","102aaa94.c920d5","eda5e162.ec41c","6efac09a.a2f69"]]},{"id":"f8d13f15.5590c","type":"function","z":"5e5fdc91.d8f9d4","name":"icao","func":"msg.icaoString = msg.payload.icao.toString(16);\nmsg.gsid = msg.payload.toaddr.toString(16);\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","libs":[],"x":2410,"y":1460,"wires":[["62c4d94f.b25828","7d3510bb.8054b"]]},{"id":"62c4d94f.b25828","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":4,"width":1,"height":1,"name":"","label":"ICAO: ","format":"{{msg.icaoString}}","layout":"row-left","x":2550,"y":1460,"wires":[]},{"id":"7d3510bb.8054b","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":10,"width":1,"height":1,"name":"","label":"GS ID: ","format":"{{msg.gsid}}","layout":"row-left","x":2544,"y":1497,"wires":[]},{"id":"527949ed.e9eb68","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":5,"width":2,"height":1,"name":"","label":"Tail: ","format":"{{msg.payload.tail}}","layout":"row-left","x":2550,"y":1540,"wires":[]},{"id":"b6253ede.f08e3","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":11,"width":2,"height":1,"name":"","label":"Flight: ","format":"{{msg.payload.flight}}","layout":"row-left","x":2550,"y":1580,"wires":[]},{"id":"102aaa94.c920d5","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":16,"width":6,"height":1,"name":"","label":"Data: ","format":"{{msg.payload.data}}","layout":"row-left","x":2550,"y":1620,"wires":[]},{"id":"eda5e162.ec41c","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":21,"width":6,"height":1,"name":"","label":"Text: ","format":"{{msg.payload.text}}","layout":"row-left","x":2550,"y":1660,"wires":[]},{"id":"6efac09a.a2f69","type":"function","z":"5e5fdc91.d8f9d4","name":"","func":"msg.ts = new Date(msg.payload.timestamp * 1000);\nmsg.ts = msg.ts.toISOString().slice(msg.ts.length,-5);\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","libs":[],"x":2435,"y":1700,"wires":[["76d49f7b.2597e"]],"l":false},{"id":"76d49f7b.2597e","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":6,"width":3,"height":1,"name":"","label":"Last msg: ","format":"{{msg.ts}}","layout":"row-left","x":2560,"y":1700,"wires":[]},{"id":"9a9f2355.0e9eb","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2435,"y":1740,"wires":[["8772957f.b74d78"]],"l":false},{"id":"8772957f.b74d78","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":18,"width":1,"height":1,"name":"","label":"Total: ","format":"{{msg.payload}}","layout":"row-left","x":2550,"y":1740,"wires":[]},{"id":"a38ae90b.462a58","type":"ui_group","name":"UK","tab":"733f36e1.cf5db8","order":7,"disp":true,"width":11,"collapse":false},{"id":"733f36e1.cf5db8","type":"ui_tab","name":"VHF-VDL2","icon":"flight","order":7,"disabled":false,"hidden":false}]


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>