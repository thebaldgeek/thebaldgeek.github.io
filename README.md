# Decoding ADSC, ADSB, ACARS, VDL2, Iridium, HF-DL and other aircraft type messages.

Navigation: [Inmarsat](Inmarsat.md) : [L-Band](L-Band.md) : [C-Band](C-Band.md) :  [VHF-ACARS/VDL2](vhf-acars.md) :  [dumpHFDL](dumpHFDL.md) : [Iridium](Iridium.md) : [STDC](stdc.md) : [Jaero](jaero.md) : [SDRReceiver](SDRReceiver.md) : [Radiosonde](radiosonde.md) : [DragonOS](DragonOS.md) : [autoTLE](autoTLE.md) : [OpenSkyAPI](OpenSkyAPI.md) : [VRS](vrs.md) : [MQTT](mqtt.md) : [Raspberry Pi](raspberrypi.md) : [Telegram Bot](telegram.md) : [UAV-Drone](UAV-Drone.md) : [Squawk](Squawk.md) : [Interesting Flights](notable_flights.md) : [wardrive](wardrive.md)

# The main ACARS website

You can search and live view a lot of satcom ACARS feeds (and some HFDL / VHF VDL ones as well) on the site:-    
    
[tbg.airframes.io](https://tbg.airframes.io/)   
The closest thing there is to a 'users guide' for the site is [here](https://community.airframes.io/t/website-overview-tbg-airframes-io/159)   
       
Please note that the website is a dumpster fire. (ie, full of bugs and glitches).   
    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/dumpstaFire.png" height="320">    
   
Honestly, that's part of its quirky appeal. Jokes aside, tbg is not a programmer, he is the wrong guy to be doing this, but here we are...   
If you want a more solid ACARS website, check out [airframes.io](https://airframes.io), they are the real deal over there.   
If you are looking for ACARS hardware, hit up their [shop](https://shop.airframes.io/)    
The way we think of the two websites is that tbg.airframes is the scrappy ally cat that makes all the mistakes, ACARS on the bleeding edge.    
Airframes.io is the powerful puma, ACARS done right.   
The sites are not really 'connected' beyond they both are ACARS centric and run by good mates.    
thebaldgeek is gratefully hosted by airframes. It is CRITICAL that if you setup an ACARS station that you feed airframes.io first and foremost.         
    


Map with ADSC and ACARS aircraft:    
[tbgmap.airframes.io](https://tbgmap.airframes.io/)   
Tips for using the map - and you REALLY REALLY should read them - can be found here:   
[tbg map notes](https://tbg.airframes.io/dashboard/map)
    
Map with military aircraft and their ACARS messages:   
[tbgacarshub.airframes.io](https://tbgacarshub.airframes.io/adsb)   
Note: The position plots and ACARS messages are synchronized over time in your web browser. When you click the link, just chill for about 30 min while it does it thing.  
Since the map syncs in real time, the map won't work as intended on mobile devices, they drop the connection to save power too readily.   
      

# What even is ACARS??    
Get a solid intro by [reading this overview of ACARS](https://www.pentestpartners.com/security-blog/introduction-to-acars/). Its one of the best introductions of ACARS from signal to data thebaldgeek has ever come across.    
   
There are many osint folks and avgeeks that combine the usual ADSB/C data (aircraft pixels on a map) _with_ ACARS to really amplify both sources of data. The sum really is MUCH greater than the parts.   
   
Think of aircraft tracking this way:    
ADSB/C is the where.    
ACARS is the why.   

## About these GitHub pages  
This GitHub 'website' is just a tbg brain dump and rough help notes to assist others in getting the hardware and software together to receive and decode ACARS messages from the main modes and frequencies.    
Its not perfect, its not up to date, its not finished, its not polished, it never will be..... in time, these pages will fade as more helpful docs are written over at [docs.airframes.io](https://docs.airframes.io/)   

###  READ THIS!

tbg motto is 'fail fast, fail often'. thebaldgeek is NOT a programmer. Do NOT use the site. Do not read these GitHub pages.  
The best way to put this is: `I don't know what I'm doing, and its clear that I know that I don't know, but here we are.`  


### Support    

thebaldgeek is happy to help those that try and help themselves, conversely, low quality questions get cut/paste answers from these pages.        
   
If you have some ideas about improving ACARS readability or decoding of ACARS for the site, here is his starting point - "A problem well stated is a problem half-solved. Charles Kettering - Inventor".   
In other words, the better you can describe your suggestion, the better chance you have of seeing it show up on the site.    
tbg did not come up with any of the pages on the website, each of them are ideas clearly explained by avgeeks around the world.   
Its YOUR website, not thebaldgeeks!          

### Contact  
thebaldgeek is most active on [X / Twitter](https://twitter.com/thebaldgeek). DM's are open. Sorry, not sorry, its a fact, X is still the best avgeek platform hands down. Use lists for people you follow and its an amazing site for keeping updated with YOUR feed and nothing else. The interaction and aviation friendships there are second to none.          
If your not on X, you can try the [website chat](https://tbg.airframes.io/dashboard/chat) to connect with tbg and chat about ACARS.  
tbg also cross posts on [BlueSky](https://staging.bsky.app/profile/thebaldgeek.bsky.social). Lots of followers over there, but zero interaction - hence the cross posts for now.        
  
   
   
### Other resources   

Do note that tbg does not Tweet actual OSINT information... His site/tweets/role is to provide raw OSINT data. Hes found that most people that do osint often don't know where or how the raw data they use comes from, his goal is to help people understand how RF (radio frequency) signals can be converted into useful data for people to analyze and thus deepen the intel derived.   
    
tbg blogs about the main website, askes for input (anaon comments accepted), and goes into more depth on the sites workings: [k6thebaldgeek.blogspot](https://k6thebaldgeek.blogspot.com/)

Reddit is a tricky platform, but do take look through the posts on [Reddit ACARS](https://www.reddit.com/r/ACARS/) sub.   

If you want more of a traditional forums, then airframesio has that as well, join the [airframes community](https://community.airframes.io/)   
The ACARS team that matters is very active on the [airframes discord](https://discord.com/invite/airframes)  
The airframe team have an awesome blog: [blog.airframes](https://blog.airframes.io/)    
    
For even more searchable ACARS data (over 4 Billion ACARS messages stretching back a few years) and information on how to feed the different ACARS modes, please support [airframes.io](https://app.airframes.io/about)   
You can also follow them on Twitter [AirframesIO](https://twitter.com/AirframesIO)   
   
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>