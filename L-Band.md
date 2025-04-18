# How to build an L-Band ground station.   
   
Navigation: [home](README.md)  

Tip: Right click images and open in new tab for full resolution.    
      
The easiest way to get started with satcom ACARS is to build an L-Band setup.   
The clasic AERO ACARS L-Band data can be found around 1.5GHz and the signal footprint from each Inmarsat is broad enough that you do not require any antenna tracking. Simply point it at the middle of the satellite orbit and you can start receiving the signal and decoding ACARS messages.   
To see what Inmarsat satellite(s) are over your location, review the [Inmarsat](Inmarsat.md) page.  
   
Here is the big picture of what we are going to review:   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandoverview.jpg" height="580">   
   
The full signal path will be covered on another page, but the most import thing to know about L-Band is that you are picking up the ACARS messages *from* the airline dispatch or ground support staff *to* the aircraft.   
The way I describe it to friends and family is L-Band is *from land*. C-Band is *from Cockpit*. This means that if you are interested in listening to audio, you will only hear the voice of the dispatch operator and then silence while the flight crew are talking, you will *not* hear a full duplex conversation, just the ground side only.   

I take pains to explain this now before we get stated so that you understand what sort of messages you can expect to see from your efforts.    
Here is a typical sort of message you might see:   
`AES:4249EA GES:50 2 .VQ-BLQ ! RA G
QUHDQASRU~1
DEAR CREW,
PLEASE REQUEST ROUTE AND
DESCENT WIND SEPERATELY,
AND REPORT BACK WILL YOU
SUCCESSFULLY RECIEVE IT?
YES/NO
THANK YOU
`  
You can clearly see that this is a message from ground crew talking to the aircraft.   
But, don't be disappointed, there are a LOT of very interesting messages that come from ground staff and get sent up to the flight crew. Here is a hint, this is a CPDLC message to the same aircraft:   

`AES:4249EA GES:50 2 .VQ-BLQ ! H1 C
#MD/AA GDXE1XA.AT1.VQ-BLQ6192D0E622C960EC18
FANS-1/A CPDLC MESSAGE:
CPDLC UPLINK MESSAGE:
HEADER:
MSG ID: 3
MSG REF: 9
TIMESTAMP: 13:03:38
MESSAGE DATA:
CRUISE CLIMB TO [ALTITUDE]
FLIGHT LEVEL: 330`  
   
Here you can see the ground request that the aircraft climb to FL330.   
   
If your interest is military aircraft, L-Band has a ton of good information for you too.   
Here is an interesting ground staff message to the flight crew:   
`TC AES:3B75A8 GES:D0 2 .F-UJCH ! AA R
/OAKODYA.AT1.F-UJCH2545FAEA4AA1CF9D1A4D29A82A59A11504F8C819A08D263C8A9169208326
943A506354415E4D49082CCFAA0290
FANS-1/A CPDLC MESSAGE:
CPDLC UPLINK MESSAGE:
HEADER:
MSG ID: 10
TIMESTAMP: 17:31:43
MESSAGE DATA:
[FREETEXT]
CONFIRM TYPE OF 3 FIGHTER AIRCRAFT WITH YOU`   
    
This is from a French dispatch operator to a tanker that was towing 3 Rafael fighter aircraft around Tahiti.   
Since L-Band is from the ground to the aircraft, you will also see 'commands' given to flight crews for course changes, or even future flights, so you will know about a flight plan before it is flown. Here is one such example:  
   
`-06-21UTCAES:AE07EAGES:022.50107A!H1C-#MDWXR/ID50107A,RCH240,AJZF102SD173/MR3,11/MTKHMN,1610,TAFKHMN221610ZVRB06KT9999FEW240QNH3016INST26C-AUTORESPONSEBASEDONAVAILABLEDATA-CONTACTC2AGENCYFORADDITIONALINFO9FAD`  
Here we see RCH240 being instructed to fly to KHMN.   
    
There is more, but I will save it for 'Understanding Military ACARS Messages' page (when I get to writing it).   
     
## Building or buying the hardware ##   
Some people build, some people buy their antennas. With L-Band, you can do either.    
    
Here is a selection of L-Band antennas that I have used at some point in time:   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/PXL_20210418_192625210.jpg" height="580">      

At the front we have the RTL-SDR v2 patch. Next is the V3 patch (The v1 patch is what we call 'the blue pancake' its a simple printed circuit board patch antenna. DO NOT buy it), then a prototype of the 3D printed helix and then a second prototype.    
   
## Buy
The most popular buy option is the RTL-SDR v3 patch antenna. 
The other options are smaller antennas which are strongly not recommended! (Small size = low price = low performance ie very low signal). Some (including myself) have even tried and tested modified GPS antennas. Generally these are too small and do not have enough gain to be of real value. You might get up and running with a few scratchy signals on some of the stronger 600/1200 data channels, but you will soon be disappointed. In short, any of the small hockey puck sized patch antennas are to be avoided no matter how attractive the low price.   
   
If you do go ahead with the v3 patch antenna (and if the patch is your 'only' option for the installation you have in mind - then the v3 is the only one worth considering) be sure and replace the ultra thin and very lossy coax it comes with. More than one report of the coax simply not working out of the box is floating around on the Internet - thats how poor quality that coax is. There are many sellers / sources for quality coax with SMA connectors on each end. Remember, L-Band is around 1.5GHz, the higher the frequency, the more signal loss in the coax.
Also note that the v3 patch antenna has a built in LNA that requires Bias T to power it up. Do NOT run a second LNA in front of this antenna as it will block the DC and you will not get a signal from the antenna. (Yes, the antenna has a USB power option, you need to drill a hole in the case to use that power option).   
   
If your interest is listening to voice calls, you are going to need a pretty good antenna, the v3 patch antenna is marginal, more gain is required for good consistent decodes of the audio. Just keep in mind that the more gain an antenna has, the more directional it becomes. You may get to the point where your L-Band antenna has so much gain that the satellite orbit takes it off your antenna sweet spot and you need to track it or move each time you want to decode some voice messages. Note that this can even happen with a poorly installed patch antenna, here is an example: 
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/patchorbit.png" height="320"> 
   
Note how the message rate drops to zero when the satellite is at the top if its orbit. In this case, the patch mount should be tilted down a little so that the signal/message rate is consistent with aircraft movements. (Overnight, in the early mornings, aircraft movements die down, but your message rate should never go to zero like it does here in the graph).  
Another reason for these dropouts could be an obstruction between you and the satellite, for example a house or tree. If you recall from the [Inmarsat](Inmarsat.md) page the satellite orbit over ~24 hours is a '8', both up and down and side to side.   
    
Another aspect to consider is your long term interest in L-Band ACARS. If you just want to set something up and use it for an hour or so then pull it down, something like the V3 patch antenna might be Ok.   
If you just want to listen to one downlink channel a time, then your antenna configuration does not change much, but your software setup becomes a LOT simpler.  
If you only have an indoor antenna option, then more antenna gain is something you really need to consider.   
  
My goal was to setup a system that had 24 x 7 x 365 coverage and catch every downlink message possible from every data channel on the satellite.   
   
## Build     
My current preferred and highly recommended antenna for L-Band is a 3D printed 7 turn Helix.  
Here is a close up of the antenna while connected to a NanoVNA.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/nanovna.png" height="580">  
    
The hard work of getting the spacing is taken care of by the 3D printed white framework.   
You can download the file from thingverse here: <https://www.thingiverse.com/thing:4980180>  
Take care to download and print the correct type, there are 11 to chose from.   
Since I am **not** shooting into a dish, I need right-hand circular polarization. I also really like the version with the extra leg support at the top of the three legs, so I use file: <https://cdn.thingiverse.com/assets/d0/70/24/9c/3a/1542R_7T_0.11S_4.7D_10-90M_ACARS.stl>   
    
# BOM (Bill of Materials)
1 x 8 inch pizza pan. <https://www.amazon.com/gp/product/B08N4VQ9BM/>  
(Note, you can go larger, but no smaller on the reflector. Does not need to be stainless, but they last longer - and are harder to drill).   
1 x 2m soft copper 4mm tube. <https://www.amazon.com/gp/product/B07FXMY5DJ>    
(You will have a little left over, but 2m is the right length. You can go a little smaller diameter, but no bigger. Tube is easier to work with than solid copper wire).   
1 x Male SMA bulk head connector. <https://www.amazon.com/gp/product/B06Y5ZMNSJ/>   
Assorted stainless nuts, bolts, screws. (<https://www.amazon.com/gp/product/B06X1FNS96> <https://www.amazon.com/gp/product/B00B3RIH5E> <https://www.amazon.com/gp/product/B07D1L38HD> <https://www.amazon.com/gp/product/B01B1OD6MW/> )   
    
Order the 4mm copper tube off Amazon and the base is a stainless steel 8 inch pizza pan also from Amazon. The hardware is stainless steel from Home Depot or Amazon (2 large nuts and bolts for the 3D framework, two small nuts and bolts for the SMA bulkhead ). The antenna connector is a SMA male bulkhead connector from Amazon.   
Note, the 8 inch pizza pan is the smallest you should go. The reflector is an important part of the antenna performance. You can go bigger to no benefit, but no smaller.    

## Helix Build Tips   
      
The key to building the antenna is to pre-form the copper on a cylinder that is very close to the final size.   
       
One big tip is to NOT straighten the copper tube from how its loosely coiled as shipped. Very carefully feed the inner edge out the bottom of the packaged coil as it came and keep the coil going in a new RHCP open loose coil.   
Once you have it as an open coil in the right direction, THEN preform it on your cylinder.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/helixininch.png" height="320">   
    
And I know the real world uses mm, so here it is (since I also know people don't want to read or convert units.....)    
    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/helixinmm.png" height="320">    
    
Even my wife understood that I needed something the size of the 3D print and the exact tube brand to form the coper on did not matter at all, so yeah, just find a tube the size of the holes on the 3D print and pre-form the coper to that size.    
When you do that, its very low friction to just wind the coper onto the formwork, there is very little stress or effort and your print wont break.

Once you preform the copper to the right size, you can then wind it on the framework very smoothly.   
Just work it up the 3D framework slowly, inching it from the top, middle and bottom to keep the tension even all the way up the formwork.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandpreformcopper.png" height="460">  
    
For the feed, you don't have to, but I used a small round file to get the coper end nice and snug to the SMA post before I heat the copper first, then solder the SMA center pin.    

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/helixfeeddetail.png" height="460">
    
A touch of heat and solder and its very solid.
     
Trim the turns to roughly 7 and a bit turns (close to 8) and then drill the two large holes for the 3D frame in the reflector, then mark and drill the bulkhead connector mount near the left hand side support - you go near the left side of the frame so you can run the first 2/3rds of the copper parallel to the base, this improves the match and lowers the SWR. Solder the copper pipe to the connector and you are done building the antenna.  

Once built, trim the total length to get the VNA dip on frequency and move the first 2/3rds of a turn close to the reflector to get the SWR nice and low and you are done.   \
If you don't have a VNA, just trim the top turn to exactly 7 turns, ie, on the left side of the support that the SMA is on and the helix will be really close and still work better than the RTLSDR Patch antenna.    


   <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/7turnhelixantennas.jpg" height="460">
   
## LNA Tips   
       
While the helix can work Okish on its own, it really shines with a Nooelec L-Band low noise amplifier (LNA) mounted directly behind it. (If you are mounting the helix indoors or under a roof, you will need to use an LNA, no question).     
I buy my LNAs from Amazon. You can use Bias-T from the SDR dongle to power the amplifier or a micro USB power lead if your SDR device does not offer Bias-T as an option. Keep in mind that not all SDR Bias-Ts are equal. For example, I found out (the hard way) that the RSP1a Bias-T is not powerful enough to run the Nooelec + LNA, but the RTLSDRv3 runs it just fine. (As does the Nooelec SmarTee SDR).   
Here is the link to Amazon USA for the L-Band LNA that I really like and highly recommend. <https://www.amazon.com/gp/product/B07K1NMC23>   
Nooelec have a really helpful [page on their SAWbird LNA range](https://support.nooelec.com/hc/en-us/articles/360011133694-SAWbird-LNA-Filters), take some time to read it before making your purchase. Here is a tip, Inmarsat is pretty quiet on the 10500 and voice channels. You may need the extra gain of the + LNA version. Also note that the + draws an extra 150mA. This is a LOT of extra bias-T current. So for example, if you are using an RSP1a SDR, its Bias-T can only supply 50mA, so the base SAWbird LNA is (should be - might be) fine at 30mA draw, but the higher gain + version at 180mA will not work. So just keep in mind your entire signal path... your antenna, coax quality and length. (Of course, once again, to really press this home, you can and should just use a physical Bias-T and not have to worry about any of this).   
   
To give a feel for how the three antennas work, here are the three waterfalls centered around the 10500 channels.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98wasov1patch.png" height="320"> 


<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98wasov2patch.PNG" height="320">   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98wasocopperhelix.png" height="320">   
    
No antenna is going to work its best indoors, but if its your only option, then more gain will help.

Also keep in mind that if plan to mount this helix outside (and I strongly suggest you do) it will need to be weather proofed. Here are some photos of some customer solutions....   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixglueinpot.png" height="320">   
The silicon did not hold as well as they hoped, so they ended up screwing the base to the sides of the pot:    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixscrewinpot.png" height="320">   
Very low tech final resting place here, but its looking straight at the satellite and gives great around the clock decoding message rate:   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixondish.png" height="320">   
Here is another flowerpot solution, this one is a little more stealth (HOA rules):   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixpotfence.png" height="320">    
Lastly, here is how the LNA is mounted in both cases - just tuck it up out of the weather:    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixpotback.png" height="320">    
If you are indoors, you have more options:    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/lbandhelixtripod.png" height="320">   
Here is a great shot from a helix owner - looks like the ultimate L-Band antenna shoot out.....  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/antennaFarm.jpg" height="320">   
   
   From left to right. We have the ever popular RTLSDR v2 patch, the out of stock Othernet patch, long boom yagi (18 dBi and a length of 1,67 meters) and a 7 turn helix.  
   The results are interesting. Keep in mind these are just 'desktop' measurements as you see in the photo. I like them because they are real world, but should not be taken as hard and fast numbers: (Your install mileage may vary).   
  


| Antenna        | Jaero 600 dBuV  | Jaero 1200 dBuV  | Jaero 10500 dBuV        | Jaero 8400 dBuV  | Voice Decode  |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Helix      | 61.1 | 54.1 | 46.3  | 46.2 | yes |
| Yagi      | 62.4 | 61.5 | 50  | 48.1 | yes |
| Othernet | 53.2 | 54.7 | 39.5 | 35.8  |  no |
| v2 Patch | 56.2 | 58.4 | 46.2 | 48 | occasionally |

The gentleman that owns all the antennas kindly provided the numbers and used the same SDR and software to run the test for a few minutes on each antenna.   
It clearly shows that a big high gain antenna like the yagi is king of the L-Band, but keep in mind that it has such a narrow beam width that you will probably need to 'track' the satellite to some extent to keep the signal peaked. Also don't forget that the yagi is not circular polarized so is losing some gain there as well.  
It also shows that the data channels are not all equal. The 10500 and 8400 voice channels are the weakest. (And arguably the most interesting - despite the fact that I personally don't find one sided conversations interesting.)  
   
## Dream Antenna    
If I could have a dream L-band antenna, it might go something like this:    
In no order, my thoughts / wish-list:   
1. Inmarsat only (Don't want to try and use it for Iridium as well like the rtlsdr v2 patch - ie an L-Band antenna that does everything not very well).   
2. Filtered. SAW or otherwise. L-Band is busy/noisy. Want to keep as much out as we can.   
3. ~14Mhz bandwidth.   
4. 1537Mhz to 1550Mhz (roughly)   
5. RHCP.   
6. 30 to 50 deg beamwidth. (No less than 25 deg so no tracking is required).   
7. 10+db gain. (Real gain, not after the LNA fake numbers).   
8. 1 wavelength reflector (if required - ie if it ends up being a helix, but not locking the antenna into a given RHCP type of driven element).   
9. Full water proof / snow proof / sun proof.   
10. Tripod screw mounting (at the least). ie No suction cup option - ie a beefy antenna that works better than a light weight patch.   
11. Two power options. Bias-T and external volts. (External could be USBC or DC socket).   
12. Wide range bias T power voltage. 3 to 15 vDC. The 3v min is important as many SDRs only output 3.5v-3.8v DC under load.   
13. No LED. ie Don't make a xmas tree, and keep the power draw under ~50 to 100ma so most SDRs can drive it.   
14. No supplied coax.   
15. SMA female connector only.   
16. Passive antenna option considered. (We can run our own LNA and thus Bias-T power no longer an issue. More affordable).   
17. Different part number of a stubby LHCP antenna to fully illuminate a ~80cm or bigger dish. (Same LNA/pwer/connector etc).   
    
        
## Which SDR?   
In regard to SDRs, I like the silver v3 RTL-SDR for L-Band, but in this case, because of the requirement to use Bias-T to power the LNA, I might also use the Nooelect SmarTee SDR as it has Bias-T always on without needing to run the v3 software bat file to turn it on. The performance of the two SDRs seems to be identical. With that said, I have had some issue using the SmarTee with [SDRReceiver](SDRReceiver.md) that I am still working through. Also note that I have tested the RSP1a on L-Band and the more expensive SDR showed no benefit at all over the cheaper RTLSDR v3. This is mostly due to the fact of using the LNA, a more sensitive SDR does not perform any better since the system noise is not limited by the SDR, its set by the LNA noise figure. In short, use the cheaper SDR on L-Band and the other on HF where the difference in performance between the two is dramatic.   
Don't bother with the RTLSDR v4. Its snake oil and is a waste of money on anything but HF.   
        
## Mounting       
How you mount the antenna is up to you. A few people have put them under a flowerpot and mounted them outside and used a bracket that is pointing at their satellite. 
Some have attached them to camera tripods and used them inside their apartment's. In this case, you do not need to weatherproof the antenna, but it comes at a signal strength drop. Also experiment with positioning, a **window may not offer the best signal**. The reason for this is that a lot of windows have a Low-E coating. The metal coating really knocks back the L-Band signal. Often putting the antenna pointing out a wall or roof next to the window gives a better signal. No really. Trust me on this.      
Bottom line, the antenna and LNA are *NOT* water proof and you must put it under cover.   
## Coax   
Be sure and run some quality coax. The longer the length required to get from the antenna to the SDR, the more you should spend on the coax. 1.5GHz is rather lossy, more so than the 1090MHz from an ADSB antenna that you might be used to. (And even more so than the VHF ACARS frequency of around 130MHz). If in doubt, LMR-400 is the coax to use.   
   
   Ok, so you have the antenna mounted and pointed roughly in the [right direction](Inmarsat.md).        
     
## Software setup and tweaks    
With the antenna mounted and the coax run, we can focus on the software side of things.   
I am going to proceed as if you are going to set up and monitor all data channels around the clock and you are going to feed your data to your local Node-RED for message filtering (ie just Military aircraft) and reporting / alerting.   

In sort you need to run Jaero, thats the only software package that can decode the AERO data. You can run it on Windows or Linux.  
You also need to run some SDR dongle sofware, on either Windows or Linux there are lots of options.    
Each has their own page from my [Home](README.md) page.

Last thing to do.... What frequencies are in use for the satellite you can see/hear?     

## Inmarsat L-Band Frequencies and Data Rates ##  
Please NOTE!!! As of Jan 15th 2024, the following screenshots are out of date/old/inaccurate - They are close, but not perfect.   
Please use the frequency list!! They are very accurate.   
Use the screenshots get an idea of what things should _look_ like, but USE the frequency LIST, not the frequencies on the screenshots.   
The tables of frequencies/modes are accurate and should be primary, but the screenshots are helpful to show what you should be looking for when you first get running.  
     
# ACARS Frequency Lists for all Inmarsats   
Provisional Inmarsat frequency list prepared in February 2024 by David L. Wilson and Sergi.vdl2   
Huge thanks to these two guys for collecting and checking every single one of these frequencies!    
   
### 4A4F4 25-East   
Frequency...Region......Use..................Use......Hex Oct..Provider......GEO Location......Beam    
1545,1200	EMEA	25E	Aero-L(600)    	   P-Chan	90	220	ARINC & SITA     
1545,1250	EMEA	25E	Aero-L(1200)   	   P-Chan	90	220	ARINC & SITA     
1545,1300	EMEA	25E	Aero-L(600) 	      P-Chan	90	220	ARINC & SITA     
1546,0125	EMEA	25E	Aero-H+ (10500)	   P-Chan	90	220	ARINC & SITA     
1546,0275	EMEA	25E	Aero-H+ (10500)	   P-Chan	90	220	ARINC & SITA       
1546,1425   25E   EMEA  Aero voice(8400)AMBE C-Chan   90 220   ARINC & SITA Fucino, IT Global beam  
1546,1475   25E   EMEA  Aero voice(8400)AMBE C-Chan   90 220   ARINC & SITA Fucino, IT Global beam  
1546,1525   25E   EMEA  Aero voice(8400)AMBE C-Chan   90 220   ARINC & SITA Fucino, IT Global beam   
1546,1825   25E   EMEA  Aero voice(8400)AMBE C-Chan   90 220   ARINC & SITA Fucino, IT Global beam   
1546,1875   25E   EMEA  Aero voice(8400)AMBE C-Chan   90 220   ARINC & SITA Fucino, IT Global beam   
1546,1925   25E   EMEA  Aero voice(8400)AMBE C-Chan   90 220   ARINC & SITA Fucino, IT Global beam   
     
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/alphasatLband.PNG" height="400">       

### 3F5 54W  
Frequency...Region......Use..................Use......Hex Oct..Provider......GEO Location......Beam     
1545,0250	AORE	54W	Aero-L(600)	         P-Chan	44	104	ARINC   
1545,0300	AORE	54W	Aero-L(600)	         P-Chan	43	103	SITA   
1545,0350	AORE	54W	Aero-L(600)	         P-Chan	44	104	ARINC   
1545,0400	AORE	54W	Aero-L(600)	         P-Chan	43	103	SITA   
1546,0550	AORE	54W	Aero-H+ (10500)	   P-Chan	44	104	ARINC   
1546,0700	AORE	54W	Aero-H+ (10500)	   P-Chan	43	103	SITA   
1541,5050   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-5 N-America   
1541,5100   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-5 N-America   
1541,5150   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-5 N-America   
1541,5200   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-5 N-America   
1541,5250   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-5 N-America   
1541,5300   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-5 N-America   
1541,5350   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-5 N-America   
1541,5400   54W AORE    Aero voice(8400)AMB  C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-5 N-America   
1542,9750   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Global beam   
1542,9800   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Global beam   
1542,9850   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Global beam   
1543,4025   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-4 Mexico   
1543,4075   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-4 Mexico   
1543,4125   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-4 Mexico   
1543,4175   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-4 Mexico   
1543,4225   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-4 Mexico   
1543,4275   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-4 Mexico   
1543,4325   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-4 Mexico   
1543,4375   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-4 Mexico   
1546,8225   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-6 Europe   
1546,8275   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-6 Europe   
1546,8325   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-6 Europe   
1546,8375   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-6 Europe   
1546,8425   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-6 Europe   
1546,8475   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-6 Europe   
1546,8525   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-6 Europe   
1546,8575   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-6 Europe   
1547,4125   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-1 Brazil   
1547,4175   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-1 Brazil   
1547,4225   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-1 Brazil   
1547,4275   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-1 Brazil   
1547,4325   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-1 Brazil   
1547,4375   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-1 Brazil   
1547,4425   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-1 Brazil   
1547,4475   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-1 Brazil   
1549,7800   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-3 S-America   
1549,7850   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-3 S-America   
1549,7900   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-3 S-America   
1549,7950   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-3 S-America   
1550,4125   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-7 Africa   
1550,4175   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-7 Africa   
1550,4225   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-7 Africa   
1550,4275   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-7 Africa   
1550,4325   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-7 Africa   
1550,4375   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-7 Africa   
1550,4425   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-7 Africa   
1550,4475   54W AORE    Aero voice(8400)AMBE C-Chan   43/44 103/104 SITA/ARINC Burum, NL Spot beam-7 Africa   
 
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/54wL-Band.png" height="380">  

### 4F3 98W  
Frequency...Region......Use..................Use......Hex Oct..Provider......GEO Location......Beam         
1545,0500	AORW	98W	Aero-L(600)	      P-Chan	05	005	SITA   
1545,0600	AMER	98W	Aero-L(600)	      P-Chan	D0	320	ARINC & SITA   
1545,0650	AMER	98W	Aero-L(600)	      P-Chan	D0	320	ARINC & SITA   
1545,0750	AMER	98W	Aero-L(1200)	   P-Chan	D0	320	ARINC & SITA   
1545,0800	AORW	98W	Aero-L(600)	      P-Chan	05	005	SITA   
1545,0850	AMER	98W	Aero-L(600)	      P-Chan	D0	320	ARINC & SITA   
1545,0900	AORW	98W	Aero-L(600)	      P-Chan	05	005	SITA   
1545,1000	AORW	98W	Aero-L(600)	      P-Chan	02	002	ARINC   
1545,1700	AORW	98W	Aero-L(600)	      P-Chan	02	002	ARINC   
1545,1750	AORW	98W	Aero-L(600)	      P-Chan	02	002	ARINC   
1546,0050	AMER	98W	Aero-H+ (10500)	P-Chan	D0	320	ARINC & SITA   
1546,0200	AMER	98W	Aero-H+ (10500)	P-Chan	D0	320	ARINC & SITA   
1546,0625	AORW	98W	Aero-H+ (10500)	P-Chan	02	002	ARINC   
1546,0775	AORW	98W	Aero-H+ (10500)	P-Chan	05	005	SITA       
1542,9375   AMER 98W    Aero voice(8400)AMBE C-Chan D0 320 ARINC & SITA Paumalu, HI Global beam   
1542,9425   AMER 98W    Aero voice(8400)AMBE C-Chan D0 320 ARINC & SITA Paumalu, HI Global beam   
1542,9475   AMER 98W    Aero voice(8400)AMBE C-Chan D0 320 ARINC & SITA Paumalu, HI Global beam   
1542,9525   AMER 98W    Aero voice(8400)AMBE C-Chan D0 320 ARINC & SITA Paumalu, HI Global beam   
1542,9575   AMER 98W    Aero voice(8400)AMBE C-Chan D0 320 ARINC & SITA Paumalu, HI Global beam   
1542,9775   AORW 98W    Aero voice(8400)AMBE C-Chan 02/05 002/005 ARINC/SITA Laurentides, CA Global beam   
1542,9825   AORW 98W    Aero voice(8400)AMBE C-Chan 02/05 002/005 ARINC/SITA Laurentides, CA Global beam   
1542,9875   AORW 98W    Aero voice(8400)AMBE C-Chan 02/05 002/005 ARINC/SITA Laurentides, CA Global beam   
1542,9925   AORW 98W    Aero voice(8400)AMBE C-Chan 02/05 002/005 ARINC/SITA Laurentides, CA Global beam   
  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98w_L-Band_rtlsdr_activepatch.PNG" height="380">  

### 4F1 143E  
Frequency...Region......Use..................Use......Hex Oct..Provider......GEO Location......Beam       
1545,0250	APAC	143,5E	Aero-L(600)	         P-Chan	50	120	ARINC & SITA   
1545,0300	APAC	143,5E	Aero-L(600)	         P-Chan	82	202	ARINC   
1545,0350	APAC	143,5E	Aero-L(600)	         P-Chan	82	202	ARINC   
1545,0400	APAC	143,5E	Aero-L(600)	         P-Chan	85	205	SITA   
1545,0450	APAC	143,5E	Aero-L(600)	         P-Chan	85	205	SITA   
1545,0550	APAC	143,5E	Aero-L(600)	         P-Chan	50	120	ARINC & SITA   
1545,0700	APAC	143,5E	Aero-L(1200)	      P-Chan	50	120	ARINC & SITA   
1545,0950	APAC	143,5E	Aero-L(600)	         P-Chan	85	205	SITA   
1545,1350	APAC	143,5E	Aero-L(600)	         P-Chan	50	120	ARINC & SITA   
1545,1400	APAC	143,5E	Aero-L(600)	         P-Chan	50	120	ARINC & SITA   
1545,1450	APAC	143,5E	Aero-L(600)	         P-Chan	50	120	ARINC & SITA   
1545,1500	APAC	143,5E	Aero-L(600)	         P-Chan	50	120	ARINC & SITA   
1545,1550	APAC	143,5E	Aero-L(600)	         P-Chan	85	205	SITA   
1545,1800	APAC	143,5E	Aero-L(600)	         P-Chan	82	202	ARINC   
1545,2100	APAC	143,5E	Aero-L(600)	         P-Chan	82	202	ARINC   
1546,0050	APAC	143,5E	Aero-H+ (10500)	   P-Chan	50	120	ARINC & SITA   
1546,0350	APAC	143,5E	Aero-H+ (10500)	   P-Chan	50	120	ARINC & SITA   
1546,0550	APAC	143,5E	Aero-H+ (10500)	   P-Chan	85	205	SITA   
1546,0700	APAC	143,5E	Aero-H+ (10500)	   P-Chan	82	202	ARINC   
1546,0850	APAC	143,5E	Aero-H+ (10500)	   P-Chan	50	120	ARINC & SITA   
1542,9350   143,5E APAC    Aero voice(8400)AMBE C-Chan   50 120   ARINC & SITA Paumalu, HI Global beam   
1542,9400   143,5E APAC    Aero voice(8400)AMBE C-Chan   50 120   ARINC & SITA Paumalu, HI Global beam   
1542,9450   143,5E APAC    Aero voice(8400)AMBE C-Chan   50 120   ARINC & SITA Paumalu, HI Global beam   
1542,9500   143,5E APAC    Aero voice(8400)AMBE C-Chan   50 120   ARINC & SITA Paumalu, HI Global beam   
1542,9550   143,5E APAC    Aero voice(8400)AMBE C-Chan   50 120   ARINC & SITA Paumalu, HI Global beam   
1542,9600   143,5E APAC    Aero voice(8400)AMBE C-Chan   50 120   ARINC & SITA Paumalu, HI Global beam   
1542,9650   143,5E APAC    Aero voice(8400)AMBE C-Chan   50 120   ARINC & SITA Paumalu, HI Global beam   
1542,9700   143,5E APAC    Aero voice(8400)AMBE C-Chan   50 120   ARINC & SITA Paumalu, HI Global beam   
1542,9750   143,5E APAC    Aero voice(8400)AMBE C-Chan   82/85 202/205 ARINC/SITA Perth, AU Global beam   
1542,9800   143,5E APAC    Aero voice(8400)AMBE C-Chan   82/85 202/205 ARINC/SITA Perth, AU Global beam   
1542,9850   143,5E APAC    Aero voice(8400)AMBE C-Chan   82/85 202/205 ARINC/SITA Perth, AU Global beam   
1542,9950   143,5E APAC    Aero voice(8400)AMBE C-Chan   82/85 202/205 ARINC/SITA Perth, AU Global beam       

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/143eL-Band.png" height="380"> 

### 6F1 83E (No screenshot for now)      
Update: Apr 2025   
1545076800 (600)   
1545081700 (600)   
1545086800 (600)   
1545156400 (600)   
1545161500 (600)   
1545181900 (600)    
1546036100 (10500)   
1546086000 (10500)   
1546101200 (10500)   
1546116700 (10500)    
    
Old list kept for historical reference only - do not use.   
Frequency...Region......Use..................Use......Hex Oct..Provider......GEO Location......Beam      
1545,0050   83,5E       Aero-L(600)       Psmc2    C1 301         ARINC Perth, AU         Global beam      
1545,1600   83,5E       Aero-L(600)       P-Chan   C5 305         SITA Perth, AU          Global beam      
1545,1650   83,5E       Aero-L(600)       P-Chan   C5 305         SITA Perth, AU          Global beam      
1545,1850   83,5E       Aero-L(600)       P-Chan   C5 305         SITA Perth, AU          Global beam      
1545,2150   83,5E       Aero-L(600)       P-Chan   C1 301         ARINC Perth, AU         Global beam      
1545,2200   83,5E       Aero-L(600)       P-Chan   C1 301         ARINC Perth, AU         Global beam   
1545,2250   83,5E       Aero-L(600)       P-Chan   C1 301         ARINC Perth, AU         Global beam   
1546,0425   83,5E       Aero-H+ (10500)   P-Chan   C1 301         ARINC Perth, AU         Global beam   
1546,0925   83,5E       Aero-H+ (10500)   P-Chan   C1 301         ARINC Perth, AU         Global beam   
1546,1075   83,5E       Aero-H+ (10500)   P-Chan   C5 305         SITA Perth, AU          Global beam   
1546,1225   83,5E       Aero-H+ (10500)   P-Chan   C5 305         SITA Perth, AU          Global beam     
1546,1575   83,5E       Aero voice(8400)AMBE C-Chan C1/C5 301/305 ARINC/SITA Perth, AU    Global beam      
1546,1625   83,5E       Aero voice(8400)AMBE C-Chan C1/C5 301/305 ARINC/SITA Perth, AU    Global beam      
1546,1675   83,5E       Aero voice(8400)AMBE C-Chan C1/C5 301/305 ARINC/SITA Perth, AU    Global beam      
1546,1725   83,5E       Aero voice(8400)AMBE C-Chan C1/C5 301/305 ARINC/SITA Perth, AU    Global beam      
1546,1775   83,5E       Aero voice(8400)AMBE C-Chan C1/C5 301/305 ARINC/SITA Perth, AU    Global beam       


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>