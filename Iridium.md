# Iridium ACARS and SBD Decoding.   
   
Navigation: [home](README.md)  

There is a (small) amount of ACARS messages being sent via the Iridium satellite constellation.  
In Feb 2022 we just started looking at it for the first time, so all this is very new, but here is some tips to get you started.    
### Antenna   
I started out using the RTLSDR v2 patch antenna since its only meh at Inmarsat and so I had an unused one kicking around. Note that this really is **not** the right antenna for iridium at all. It has too much forward gain, iridium needs to be omnidirectional, and the v2 patch also has a SAW filter which kills the iridium signal at the 1.6 odd gigs it uses.    
I jumped on eBay and picked up an iridium dome antenna and will report back on how it goes once we get some air time with it.   
Do note that there are very few _active_ iridium antennas since transmitting up to the satellites is very common, so if you want to go with an LNA, you will need to take a look at building your own ground station. Perhaps more on this in the future if we find real value in the data.
### SDR   
I like the RTLSDR v3 for this sort of thing. Its also very quick and clean to get running. Also this is the sort of data that you need to get running and leave running indefinitely. Its a bit of a waste to tie up an expensive SDR. If I get time to test the RSP1a I will add those startup notes. Note that if you end up using an LNA, the more expensive RSP1a will not any any advantage over the cheaper v3.  
### MUCCC - iridium-toolkit and gr-iridium    
The repo can be found on the [Chaos Computer Club München](https://github.com/muccc) GitHub.    
You will need to either build gr-iridium from source or use [DragonOS](DragonOS). Just to add some 'fun' into the mix, the DragonOS_Pi64 and the x86 Dragon_Focal use different versions of gr-iridium with the Pi being the newer version. It matters if you want to use [iridiumlive](https://github.com/microp11/iridiumlive) (more on this program to come) but in short, the Pi version does not work with IridiumLive, but it is the better version to work with the  iridium-toolkit as it is a newer build.   
Note that none of the Iridium tools need a gui, so you can run it all via a shell on a headless Pi with no issues. I did my testing on a Pi4 2gb. If you get things going on a Pi 3, please let me know.  
On a fresh Buster Pi install (I like [dietpi](https://dietpi.com/)) - quick start - following [the build notes on iridiumlive](https://github.com/microp11/iridiumlive#quick-install-on-gr-iridium-and-iridium-toolkit-for-rapberry-pi)  seems to look good (I have not tested them, I'm using pre-built on DragonOS).

Unzip the master file and you are ready to start.   
Follow the guide on the [iridium-toolkit](https://github.com/muccc/iridium-toolkit) for a sanity check, ie writing to `output.bits` and `output.parsed` (Hint, remember to chmod them for user permissions).   
Once you are sure you are getting iridium data from the SDR, you can start moving the data into Node-RED.   
## Pipe and tee   
We are going to pipe the data into Node-RED.   
To do this, we need a way to get the stdout data into a UDP stream, we will [use the iridiumlive python code](https://github.com/microp11/iridiumlive/blob/master/udp-for-il.py) to do that.   
Pull the code down from the github and save it in a file (or just cut paste it into a nano editor).   
Change the IP address in the code to match your Node-RED computer and pick a different port, but note the number.   
I strongly suggest putting the port number in the file you save as you may end up using a few of these files to move data around (I have three).    
My files are `iudp55667.py` and `iudp66778.py` Obviously, the port number is the same in the python code as the file name and the same number is used in the Node-RED UDP in node.   
You will need to chmod the files to make then executable.  
We can dump everything at once into Node-RED, but its a firehose, so lets just get ACARS for a start.    
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

If you get sick of seeing the status message scrolling up the page in the terminal, you can send it to null like this:    
```
iridium-extractor -D 4 --multi-frame rtl-sdr.conf 2>/dev/null | python3 -u ./iridium-parser.py | tee >(python3 -u ./reassembler.py -m acars | python3 /home/ubuntu/iudp55667.py) | python3 -u ./reassembler.py -m sbd | python3 /home/ubuntu/iudp66778.py
```
Now you just get the UDP count of real messages.   
