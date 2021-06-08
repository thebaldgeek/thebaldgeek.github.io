# Inmarsat - Finding 'your' sat.   
   
Navigation: [home](README.md)  

One of, if not, THE first thing you will need to do is find which of the 4 Inmarsat satellites covers your port of the planet. Or even more specifically, which of them is visible from your desired antenna location.    
There are two versions of the following diagram floating around on the Internet, be sure and consult the correct one (the one shown here). One is pre-migration, the other is post-migration. Inmarsat moved the orbits for better coverage and other technical reasons. 

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/inmarsatcoverage.png" height="580">   
   
   
As you can see, each satellite covers the main part of the planet with some overlap. Each satellite uses different frequencies from those satellites that overlap with the one next to it.   
Your choice will come down to what you can see, what local obstructions are between you and the satellite and if you are planing on receiving L-Band or C-Band aero data or both.  
    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/inmarsattable.png" height="580">   
   

You will see these Hex and Octal codes in the Jaero output, more of them latter, but this table will help you see what areas are covered by each satellite.  
    
As mentioned, you might find (unless you live in Asia Pacific where you really only have one satellite visible no matter where you live) that you can see from the diagram that you have two options. Keep in mind that L-Band is rather and can be received and decoded when near the edge of the coverage as per the map. C-Band is a lot more narrow and you find receiving and decoding a LOT harder (if not impossible) when at the edge of the coverage shown in the diagram. (For example, I am in Southern California and after several attempts still can not get decodable C-Band signal from 54W (the red in the diagram) but get solid decodes from L-Band).   
    
As mentioned, local obstructions will play a role in what your options are.   
I used an Android app to show a virtual reality view of where the satellite is located in the sky. I HIGHLY recommend you download the app and see what your options are.  
There are many such apps and I would think that there are some options in the Apple store, but don't have an Apple device so cant call any out.    
Here is the Android one I used: https://play.google.com/store/apps/details?id=ftl.satellitedishpointer.sdp   
Here are the two satellites above my house. Firstly, 98W, the main sat for my region.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98worbitvr.png" height="580">  
    
As you can see, it is well above my house.    
You need to keep in mind that the satellite will move +3 and -3 degrees either side of the equator, so be sure and visualize some movement around a 23 hour 58 minute cycle. In other words, even though the Inmarsats are called geostationary, they are not 'fixed' in the sky. Allow some margin for movement.    
     
Here is my 54W outlook.    
    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/54wloworbit.png" height="580">   
     
With this satellite you can start to see why I pointed out the +-3 deg movement. From this location that slow oscillation will take the satellite very close to below my horizon.   
From the roof of my house however, I get full coverage of the L-Band over the whole orbit with no signal fade.   
    
Perhaps it would help to see the orbit on a graph:   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/98worbitgraph.png" height="280">   

The red line is the +-3 Deg orbit Latitude shift around the equator. The green line is the slow wobble over Longitude (Yes, I have the scale incorrectly labeled in this graph when I took the screenshot). We will talk a lot more about both of these drifts when we get to the section about C-Band reception as you need to move the dish to account for this orbit wobble.