# Decoding ADSC, ADSB, ACARS, VDL2, Iridium, HF-DL and other aircraft type messages.

Navigation: [Inmarsat](Inmarsat.md) : [L-Band](L-Band.md) : [C-Band](C-Band.md) :  [VHF-ACARS/VDL2](vhf-acars.md) :  [dumpHFDL](dumpHFDL.md) : [Iridium](Iridium.md) : [STDC](stdc.md) : [Jaero](jaero.md) : [SDRReceiver](SDRReceiver.md) : [Radiosonde](radiosonde.md) : [DragonOS](DragonOS.md) : [autoTLE](autoTLE.md) : [OpenSkyAPI](OpenSkyAPI.md) : [VRS](vrs.md) : [MQTT](mqtt.md) : [Raspberry Pi](raspberrypi.md) : [Telegram Bot](telegram.md) : [UAV-Drone](UAV-Drone.md) : [Squawk](Squawk.md) 

# The main ACARS website

You can search and live view a lot of satcom ACARS feeds (and some HFDL / VHF VDL ones as well) on the site:-    
    
[tbg.airframes.io](https://tbg.airframes.io/)   
       
Please note that the website is a dumpster fire. (ie, full of bugs and glitches).   
No, tbg can't 'just give me the old site back'. Since March 22nd 2024 there is no 'old site' in existence.        
And yes, thebaldgeek is more painfully aware than you can ever know that the site looks horrible on _your_ mobile and PC screen sizes.    
    
Map with ADSC and ACARS plotted together:    
[tbgmap.airframes.io](https://tbgmap.airframes.io/)   
Tips for using the map - and you REALLY REALLY should read them - can be found here:   
[tbg map notes](https://tbg.airframes.io/dashboard/map)
    
  
# What even is ACARS??    
Get a solid intro by [reading this overview of ACARS](https://www.pentestpartners.com/security-blog/introduction-to-acars/). Its one of the best introductions of ACARS from signal to data I have ever come across.    
   
There are many osint folks and avgeeks that combine the usual ADSB/C data (aircraft pixels on a map) _with_ ACARS to really amplify both sources of data. The sum really is MUCH greater than the parts.   
   
Think of it this way:    
ADSB/C is the where.    
ACARS is the why it is where it is.

## About these GitHub pages  
This GitHub 'website' is just a tbg brain dump and rough help notes to assist others in getting the hardware and software together to receive and decode ACARS messages from the main modes/frequencies.    
Its not perfect, its not up to date, its not finished, its not polished, it never will be..... in time, these pages will fade as more helpful docs are written over at [docs.airframes.io](https://docs.airframes.io/)   

###  READ THIS!

My motto is 'fail fast, fail often'. I am NOT a programer. Do NOT use the site. Do not read these GitHub pages. But please do continue to complain about both of them.  
The best way to put this is: `I don't know what I'm doing, but at least I know that I don't know what I'm doing.`  


### Support    

I am happy to help those that try and help themselves.... In other words, if you don't read these pages and ask questions that are clearly answered here, then tbg responses will be limited. (Usually screenshots from this Github of what you did not read).     
   
If you have some ideas about improving the data readablity or decoding of ACARS for the site, here is my starting point - "A problem well stated is a problem half-solved. Charles Kettering - Inventer".   
In other words, the better you can describe your suggestion, the better chance you have of seeing it show up on the site.    
      

### Contact  
If you are on X, best way to get hold of thebaldgeek is to DM him over there. (Both X and DM's are open and public).   
If your not on X, you can try the [website chat](https://tbg.airframes.io/dashboard/chat) to connect with tbg and chat about ACARS.  
    
thebaldgeek is most active on [X / Twitter](https://twitter.com/thebaldgeek).       
The best way to keep updated with the goings on of all things ACARS really is via X.     
   
### Other resources   

Do note that I don't Tweet actual OSINT information... My site/tweets/role is to provide raw OSINT data. Ive found that most people that do osint often don't know where/how the raw data they use comes from, my goal is to help people understand how RF (radio frequency) signals can be converted into useful data for people to analyze and thus deepen the intel derived.   
    
If you have 15 minutes to look at some old real world examples of ACARS data, look back through the [Reddit ACARS](https://www.reddit.com/r/ACARS/) sub.   
    
Not as active, but tbg is also on <a rel="me" href="https://ioc.exchange/@thebaldgeek">Mastodon</a>   
Even less active, but also on [BlueSky](https://staging.bsky.app/profile/thebaldgeek.bsky.social)   

If you want more of a traditional forums, then airframesio has that as well, join the [airframes community](https://community.airframes.io/)   
The whole ACARS team is very active on the [airframes discord](https://discord.com/invite/airframes)  
    
For even more searchable ACARS data (over 2 Billion ACARS messages stretching back a few years) and information on how to feed the different ACARS modes, please support [airframes.io](https://app.airframes.io/about)   
You can also follow them on Twitter [AirframesIO](https://twitter.com/AirframesIO)   
   
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>