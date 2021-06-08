# Inmarsat - Finding 'your' sat.   
   
Navigation: [home](README.md)  

One of, if not, THE first thing you will need to do is find which of the 4 Inmarsat satellites covers your part of the planet. Or even more specifically, which of them is visible from your desired antenna location.    
There are two versions of the following diagram floating around on the Internet, be sure and consult the correct one (the one shown here). One is pre-migration, the other is post-migration. Inmarsat moved the orbits for better coverage and other technical reasons in 2018. 

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/inmarsatcoverage.png" height="580">   
   
   
Each satellite covers part of the planet with some overlap. Each satellite uses different frequencies from those satellites that overlap with the one next to it. We list the frequencies for L-Band further down on this page.   
Your choice will come down to what you can see, what local obstructions are between you and the satellite and if you are planing on receiving L-Band or C-Band aero data or both.  
    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/inmarsattable.png" height="580">   
   

You will see these Hex and Octal codes in the Jaero output, more of them latter, but this table will help you see what areas are covered by each satellite.  
    
As mentioned, you might find (unless you live in Asia Pacific where you only have one satellite visible no matter where you live) that you can see from the diagram that you have two satellite options. Keep in mind that the L-Band beam width is rather broad and can be received and decoded even when near the edge of the coverage as per the map. C-Band is a lot more narrow beam and you will find receiving and decoding a LOT harder (if not impossible) when at the edge of the coverage shown in the diagram. (For example, I am in Southern California and after several attempts still can not get decodable C-Band signal from 54W (the red in the diagram) but get solid decodes from L-Band).   
    
As mentioned, local obstructions will play a role in what your options are.   
I used an Android app to show a virtual reality view of where the satellite is located in the sky. I HIGHLY recommend you download the app and see what your options are.  
There are many such apps and I would think that there would some options in the Apple store, but don't have an Apple device so cant call any out.    
Here is the Android one I used: https://play.google.com/store/apps/details?id=ftl.satellitedishpointer.sdp   
Here are the two satellites above my house. Firstly, 98W, the main sat for my region.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98worbitvr.png" height="580">  
    
As you can see, it is well above my house and in the clear sky for its entire orbit.    
You need to keep in mind that the satellite will move +3 and -3 degrees either side of the equator, so be sure and visualize some movement around a 23 hour 58 minute cycle. In other words, even though the Inmarsats are called geostationary, they are not 'fixed' in the sky. Allow some margin for movement.    
     
Here is my 54W outlook.    
    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/54wloworbit.png" height="580">   
     
With this satellite you can start to see why I pointed out the +-3 deg movement. From this location that slow oscillation will take the satellite very close to below my horizon.   
From the roof of my house however, I get full coverage of the L-Band over the whole orbit with no signal fade.   
    
Perhaps it would help to see the orbit on a graph:   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98worbitgraph.png" height="280">   

The red line is the +-3 Deg orbit Latitude shift around the equator. The green line is the slow wobble over Longitude (Yes, I have the scale incorrectly labeled in this graph when I took the screenshot). We will talk a lot more about both of these drifts when we get to the section about C-Band reception as you need to track your dish to account for this orbit wobble.   

Here is yet another way to visualize the drift in the satellite orbit:   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98worbitheatmap.png" height="580"> 

This is heatmap of Inmarsat 98W orbit taken over 2-3 days.   
   

**A note about window mounted L-Band antennas.** We have found in helping many people get up and running with L-Band reception that many double and single glazed windows have a 'Low E coating'. It is a very thin (transparent) metal film on the glass that helps with insulation from cold and heat. It is very very effective in blocking RF signal. More often than not people may find they get a better signal looking through a wall or roof than looking through a window. Please keep that in mind when using the AR sat finder app and seeing where to place your antenna.  
   
The type of antenna also will have some impact on your continuous reception. If you just want to setup now and then to pick up a little data for an hour or so, then this will not be a major issue, but if you wish to leave the antenna in place and track aircraft messages around the clock (ie, over the whole orbit of the satellite) then here are some tips:   
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/25elbandv2patchdropouts.png" height="280"> 
   
Here is a classic issue that comes up often with the RTLSDR V2 (and V1 and blue PCB patch) Patch antennas. They have marginal beam width and so you can often lose data at the top or bottom (or both) of the orbit.   
We will cover how to plot your data rate on a graph like this on another page, but it is a critical part of setting up, tuning and running a quality ground station.   
In this case you can try tilting the antenna mount up a bit at a time until you have good data rates over the whole orbit, or you can swap out the patch antenna for a helix antenna.
Here are some of the L-Band antennas we have tested:

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98waso.jpg" height="580">   
   
   From front to back, we have the v1 patch, the v2 patch, a wire wound 7 turn helix and lastly a 4mm copper pipe 7 turn helix (my preferred antenna for L-Band).  
   
## Inmarsat L-Band Frequencies and Data Rates ##  

### 4A4F4 25-East
1545.1150 GES:90 600  
1545.1200 GES:90 600  
1545.1250 GES:90 1200  
1545.1300 GES:90 600  
1545.1600 GES:C5 600  
1545.1650 GES:C5 600  
1545.1850 GES:C5 600  
1545.1900 GES:C5 600  
1545.2150 GES:C1 600  
1545.2200 GES:C1 600  
1545.2250 GES:C1 600  
1546.0130 GES:90 10500  
1546.0270 GES:90 10500  
1546.0430 GES:C1 10500  
1546.0920 GES:C1 10500  
1546.1080 GES:C5 10500  
1546.1200 GES:C5 10500  

### 3F5 54W  
1545.0300 GES:43 600  
1545.0350 GES:44 1200      
1545.0400 GES:43 600  
1545.0450 GES:44 1200    
1545.0950 GES:44 600  
1545.1000 GES:02 600  
1545.1350 GES:44 600  
1545.1400 GES:43 1200  
1545.1790 GES:43 600  
1546.0550 GES:44 10500  
1546.0700 GES:43 10500  
1546.0850 GES:44 10500  

### 4F3 98W  
1545.0500 GES:05 600  
1545.0600 GES:D0 600  
1545.0650 GES:D0 600  
1545.0750 GES:D0 1200  
1545.0800 GES:05 600  
1545.0850 GES:D0 600  
1545.0900 GES:05 600  
1545.1000 GES:02 600  
1545.1700 GES:02 600  
1545.1750 GES:02 600  
1546.0050 GES:D0 10500  
1546.0200 GES:D0 10500  
1546.0630 GES:02 10500  
1546.0780 GES:05 10500      
  
### 4F1 143E  
1545.025 GES:50 600   
1545.030 GES:82 600  
1545.035 GES:82 600   
1545.040 GES:85 600   
1545.045 GES:85 600   
1545.055 GES:50 600   
1545.070 GES:50 1200    
1545.095 GES:85 600   
1545.135 GES:50 600   
1545.140 GES:50 600   
1545.145 GES:50 600   
1545.150 GES:50 600   
1545.155 GES:85 600   
1545.180 GES:82 600   
1545.210 GES:82 600   
1546.005 GES:50 10500   
1546.035 GES:50 10500   
1546.055 GES:85 10500   
1546.070 GES:82 10500   
1546.085 GES:50 10500   

