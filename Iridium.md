# Iridium ACARS and SBD Decoding.   
   
Navigation: [home](README.md)  

There is a good amount of ACARS messages being sent via the Iridium satellite constellation. 4 stations scattered around mainland USA are seeing around 3000 messages a day.  
In Feb 2022 we just started looking at it for the first time, so all this is very new, but here are some tips to get you started. If you want to get technical, [this doc](https://www.icao.int/safety/acp/inactive%20working%20groups%20library/acp-wg-m-iridium-3/ird-swg03-wp05-draft%20iridium%20ams(r)s%20tech%20manual%20-%20021506.pdf) is a good read.    
### Antenna   
I started out using the RTLSDR v2 patch antenna since its only meh at Inmarsat and so I had an unused one kicking around. While not the best antenna for Iridium (its directional and has a SAW filter in the LNA), its not too bad and given it's price and availability, if its all you can get, then give it a go.  
I jumped on eBay and picked up an iridium dome antenna and will report back on how it goes once we get some air time with it.   
Do note that there are very few _active_ iridium antennas since transmitting up to the satellites is very common, so if you want to go with an amplified antenna, you will need to take a look at building your own ground station. Perhaps more on this in the future if we find real value in the data.   
### LNA   
There are a few wide band amplifiers that cover 1.6Ghz, but the Nooelec Iridium LNA has amazing performance. Well worth the money and Bias-T hassels to drive this amplifier. 
### SDR   
I like the RTLSDR v3 for this sort of thing. Its very affordable and very quick and clean to get running. The problem with the RTLSDR is that it only covers around 2Mhz bandwidth and that is only covers a very small number of the Iridium data channels.  
4 of us have tried getting the RSP1a up and running and all 4 have failed, we will get to the bottom of that in due course, in the mean time I am using the Airspy Mini (at only 3Mhz bandwidth, looks like the Raspberry Pi can not drive it at its full 6Mhz bandwidth) and am getting good numbers, about 4x the data from the RTLSDR. Once we get the RSP1a working, I will update this page with the instructions. Note that Texas is using an Airspy R2 at around 8Mhz bandwidth and has the best message rate of the 4 stations so far.   

To be clear. You require a 10Mhz bandwidth SDR and computer to drive it to get all the data channels on Iridium.   
  
Note that if you end up using a Nooelect LNA, the more expensive RSP1a can not drive it, so you will need a physical Bias-T power injector.
### MUCCC - iridium-toolkit and gr-iridium    
The repo can be found on the [Chaos Computer Club München](https://github.com/muccc) GitHub.    
You will need to either build gr-iridium from source or use [DragonOS](DragonOS). Just to add some 'fun' into the mix, the DragonOS_Pi64 and the x86 Dragon_Focal use different versions of gr-iridium with the Pi being the newer version. Not sure what the differences are or if they matter for ACARS reception/decoding.   
Note that none of the Iridium tools need a gui, so you can run it all via a shell on a headless Pi with no issues. I did my testing on a Pi4 2gb. You will quickly max out the CPU long before the memory on the Pi, so 2gig or 4 gig of RAM does not matter.   

It is very important that you run the latest iridium-toolkit. It is under active development and the version on DragonOS does _not_ include the ACARS decoder. To get the latest, run the following 3 commands from your home directory.   
```cd ~```   
```wget https://github.com/muccc/iridium-toolkit/archive/refs/heads/master.zip```   
```unzip master.zip```   

With those three commands you are ready to start.   

For now you are going to open a few terminals, we are working on an script to run it, but for now, this is the best way to get going.....    
Here is the big picture, we are going to make two python files (acars.py and map.py) each with a different port number, one to feed me your ACARS the other to feed me your sats.json file to plot your coverage [on the Iridium map](http://thebaldgeek.net:7777/map.html).
# Lots of terminals
## Terminal One   
Run the extractor:    
```iridium-extractor -D 4 --multi-frame /usr/src/gr-iridium/examples/rtl-sdr.conf | python3 -u ~/iridium-toolkit-master/iridium-parser.py -o zmq```  
Of course, if you not using an RTLSDR look in the /examples/ directory and find your SDR and tweak that file to best set it up.   
You are going to get a line of data per second:   
```1645669280 | i: 3267/s | i_avg: 142/s | q_max: 1267 | i_ok:   0% | o: 2001/s | ok:   0% | ok:  13/s | ok_avg:   7% | ok:       8971 | ok_avg:  10/s | d: 33001```  

You want to see 60% to 100% in the `ok:` part. Lower number means more bad packets and you need to fix your antenna, coax, LNA or gain in the .conf file.   
## Terminal Two
Type `nano acars.py`, then copy/paste [in this text](https://github.com/microp11/iridiumlive/blob/master/udp-for-il.py) from the iridiumlive github. Change the IP address to my site `thebaldgeek.net` and change the port number from 15007 to the port I give you. Then save and exit nano. If you want to send me your map coverage, do this command ```cp acars.py map.py``` then ```nano map.py``` and change the port number for the one I give you.   
Next run this command:   
```python3 -u ~/iridium-toolkit-master/reassembler.py -m acars zmq: | python3 /home/ubuntu/acars.py```  
Do note that nothing will show in this terminal until you pickup your first ACARS message. Depending on how much Iridium aircraft there are in your area, it could take a moment or a few minutes, then a single number will show up, you will see a number for every message. The number is the size of the ACARS message once its decoded.  
## Terminal Three    
Now, we need to get the map running: (This is optional, but cool to see)   
```cd ~/iridium-toolkit-master/html```      
```nano example.sh```    
On the second bottom line, add a 3 at the end of the python and change the IP address for your Pi (your pi might not be 192.168.1.122), so it should read ```python3 -m http.server --bind 192.168.1.22 8888```     
Save and exit nano    
  
In the terminal run the example file: `./example.sh`  
At this point, you can visit your Pi's IP address from any browser on your  network and look for the map, so in my case `http://192.168.1.122:8888/map.html`  
Let that run. You should see the sats and beams update around once a minute.

## Terminal Four   
Almost there: make a copy of the python UDP script `cp ~/acars.py ~/map.py`   
Now edit that new file: `nano ~/map.py` and change the port number to the one I give you.   
Next run this command: 
```pip install https://github.com/joh/when-changed/archive/master.zip```   
This will install a python script that will look for changes to a file. 
Now go to where it was installed:  
```cd /home/ubuntu/.local/bin```   
Now run the file watch which will send me your sats.json once a minute and your coverage will be added to the master map on my site:

```./when-changed ~/iridium-toolkit-master/html/sats.json cat ~/iridium-toolkit-master/html/sats.json |  python3 ~/map.py```

So, to wrap this up... you need 4 terminal (PuTTY or what ever) sessions:    
1. ```iridium-extractor -D 4 --multi-frame /usr/src/gr-iridium/examples/rtl-sdr.conf | python3 -u ~/iridium-toolkit-master/iridium-parser.py -o zmq```  
2. ```python3 -u ~/iridium-toolkit-master/reassembler.py -m acars zmq: | python3 /home/ubuntu/acars.py```   
3. `./example.sh`   
4. ```./when-changed ~/iridium-toolkit-master/html/sats.json cat ~/iridium-toolkit-master/html/sats.json |  python3 ~/map.py```

---

Simplex Frequency Allocation   

| Channel Number | Center Frequency(MHz) | Allocation |   

| :-: | :------: | :------------: |  
| 1 | 1626.020833 | Guard Channel |   
| 2 | 1626.062500 | Guard Channel |   
| 3 | 1626.104167 | Quaternary Messaging |   
| 4 | 1626.145833 | Tertiary Messaging |   
| 5 | 1626.187500 | Guard Channel |   
| 6 | 1626.229167 | Guard Channel |   
| 7 | 1626.270833 | Ring Alert |   
| 8 | 1626.312500 | Guard Channel |   
| 9 | 1626.354167 | Guard Channel |   
| 10 | 1626.395833 | Secondary Messaging |   
| 11 | 1626.437500 | Primary Messaging |   
| 12 | 1626.479167 | Guard Channel |   

Duplex Channel Band   

| Sub-band | Lower Edge (MHz) | Upper Edge (MHz) |

| :-: | :--: | :--: |   
| 1 | 1616.000000 | 1616.333333 |   
| 2 | 1616.333333 | 1616.666667 |   
| 3 | 1616.666667 | 1617.000000 |   
| 4 | 1617.000000 | 1617.333333 |   
| 5 | 1617.333333 | 1617.666667 |   
| 6 | 1617.666667 | 1618.000000 |   
| 7 | 1618.000000 | 1618.333333 |   
| 8 | 1618.333333 | 1618.666667 |   
| 9 | 1618.666667 | 1619.000000 |   
| 10 | 1619.000000 | 1619.333333 |   
| 11 | 1619.333333 | 1619.666667 |   
| 12 | 1619.666667 | 1620.000000 |   
| 13 | 1620.000000 | 1620.333333 |   
| 14 | 1620.333333 | 1620.666667 |   
| 15 | 1620.666667 | 1621.000000 |   
| 16 | 1621.000000 | 1621.333333 |   
| 17 | 1621.333333 | 1621.666667 |   
| 18 | 1621.666667 | 1622.000000 |   
| 19 | 1622.000000 | 1622.333333 |   
| 20 | 1622.333333 | 1622.666667 |   
| 21 | 1622.666667 | 1623.000000 |   
| 22 | 1623.000000 | 1623.333333 |   
| 23 | 1623.333333 | 1623.666667 |   
| 24 | 1623.666667 | 1624.000000 |   
| 25 | 1624.000000 | 1624.333333 |   
| 26 | 1624.333333 | 1624.666667 |   
| 27 | 1624.666667 | 1625.000000 |   
| 28 | 1625.000000 | 1625.333333 |   
| 29 | 1625.333333 | 1625.666667 |   
| 30 | 1625.666667 | 1626.000000 |   

Stop reading here, the notes below are wrong and are just for history.   

------------------------------

## Pipe and tee   
We are going to pipe the data into Node-RED via UDP.   
To do this, we need a way to get the stdout data into a UDP stream, we will [use the iridiumlive python code](https://github.com/microp11/iridiumlive/blob/master/udp-for-il.py) to do that.   
Pull the code down from the github and save it in a file (or just cut paste it into a nano editor).   
Change the IP address in the code to match your Node-RED computer and pick a different port, but note the number.   
I strongly suggest putting the port number in the file name you save as you may end up using a few of these files to move data around (I have three).    
My files are `iudp55667.py` and `iudp66778.py` Obviously, the port number is the same in the python code as the file name and the same number is used in the Node-RED UDP in node.   
You will need to chmod the files to make them executable.  
We can dump everything at once into Node-RED, but its a firehose, so lets just get ACARS going for a start.    
```
iridium-extractor -D 4 --multi-frame rtl-sdr.conf | python3 -u ./iridium-parser.py -p | python3 -u ./reassembler.py -m acars | python3 /home/ubuntu/iudp55667.py
```
You can see we are piping the data from each application to the next. The -u tells python to unbuffer the data. Note you may or may not have to call out 'python3' depending on what versions of python you have installed on your Pi, I have both v2 and v3, so need to call out which to use (you must use v3 for the iridium-toolkit).    
Now on the Node-RED end, you can put your UDP in node and a debug node and after a few minutes you should see your first Iridium ACARS message pop up.   
If you want to see short burst data messages, in the command above, swap `-m acars` for `-m sbd` You will see more sbd messages than ACARS, so that might be a good sanity check.   
 
What if you want both on different streams? Use a `tee`.    
```
iridium-extractor -D 4 --multi-frame rtl-sdr.conf | python3 -u ./iridium-parser.py | tee >(python3 -u ./reassembler.py -m acars | python3 /home/ubuntu/iudp55667.py) | python3 -u ./reassembler.py -m sbd | python3 /home/ubuntu/iudp66778.py
```
Now add a second UDP in node and a second debug in the Node-RED editor and you will have ACARS on port 55667 and sbd on port 66778.    

How about three feeds. One to IridiumLive, one to ACARS and one to sbd....     
```
sudo iridium-extractor -D 4 --multi-frame ~/iridium-toolkit-master/rtl-sdr.conf | tee >(python3 -u /usr/src/iridium-toolkit/iridium-parser.py -p /dev/stdin /dev/stdout | python3 /home/ubuntu/u15007.py) | python3 -u /usr/src/iridium-toolkit/iridium-parser.py -p |  tee >(python3 -u ~/iridium-toolkit-master/reassembler.py -m acars | python3 /home/ubuntu/u9998.py) |  python3 -u ~/iridium-toolkit-master/reassembler.py -m sbd | python3 /home/ubuntu/u29998.py
```

If you get sick of seeing the status message scrolling up the page in the terminal, you can send it to null like this:    
```
iridium-extractor -D 4 --multi-frame rtl-sdr.conf 2>/dev/null | python3 -u ./iridium-parser.py | tee >(python3 -u ./reassembler.py -m acars | python3 /home/ubuntu/iudp55667.py) | python3 -u ./reassembler.py -m sbd | python3 /home/ubuntu/iudp66778.py
```
Now you just get the UDP count of real messages.   

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>