# STD-C aka InmarsatC aka NCSC aka EGC aka Marine Messages.   
   
Navigation: [home](README.md)  

STDC provides a range of messages to ships. These channel contain 'official' messages rather than personal email or text messages.   
These messages can be decoded via a few different software packages, some Linux only, some Windows only, some cross platform.   
All these programs decode the same 1200 bps DBPSK Network Control Station Channel (NCSC).   
The main frequencies are known as Enhanced Group Call (EGC), which allows official broadcast messages to be sent to ships located anywhere within a satellite's coverage.   
The usual four Inmarsat geostationary satellites provide worldwide coverage for these types of broadcasts.    
   
You will find them on the following frequencies:   
   
98w. 4F3. AOR-W: 1537.70 MHz   
   
25e. 4AF4. IOR: 1537.10 MHz   
   
54w. 3F5. AOR-E: 1541.45 MHz   
   
143e. 4F1. POR: 1541.45 MHz   
    
Most people seem to be using the RTLSDR v3 patch antenna but a ~7 turn RHCP helix with LNA would be better, or a 3-4 turn LHCP helix pointing at a small dish also works. The signal is very strong and robust, so you don't need huge amounts of gain.   
The SDR need be nothing more expensive than the usual RTLSDR V3 silver dongle.    
Use some quality coax (not the needle thin RTLSDR junk that comes with the patch antenna - throw it out and get some better quality coax). and you should have a very solid decode rate consisting of about 100+ messages per day.   
The signal is easy to find as it is a continuos carrier even when no messages are being sent.   
For the Linux decoders, usually a Raspberry Pi 4 is capable of decoding the stream. Most require either a GUI or a GUI SDR (with waterfall) software, so a desktop environment is required (DragonOS_Pi64 is highly recommended).   
   
Software options:   
    
satdump. (Free) Linux or Windows. Low CPU use with CLI option. Rock solid performance with JSON output via UDP makes this app the clear top choice.   
InmarsatDecoder (~$50USD) Windows.   
Teckmanoid (~$50USD) Crossplatform (Java required)   
Scytale-C (Free) Crossplatform with some work.    
SDR++ STD-C demodulator plug-in and QT Inmarsat-C Parser. (Free). Linux only   
stdcdec Command line. Linux. (Free)
    
It should be noted that none of these software packages other than satdump share their decoded messages very gracefully. I have had to use Node-RED and do some ugly workarounds to get the messages moved from the decoders to a web dashboard.   
This may not be an issue in your use case, but bears mentioning as the real power of receiving any of these satcom message streams is being able to filter and alert on messages of interest. 
Lastly, after months of logging the 4-5 'private' message channels on three of the satellites I can safely say the message contents just don't warrent the CPU cycles. Its mostly 'The fish are over here' in different launguages.   
All 4 satellite feeds are avliable on the main site, just click the menu and its the last page at the bototm.    
    
## Satdump tips    
Get satdump for your system [from their github.](https://github.com/SatDump/SatDump)    
Once built or installed, to get STDC data out via UDP stream, you need to edit the `Inmarsat.json` pipeline.   
The file is in the `pipelines` directory in the satdump folder.   
Open `Inmarsat.json` in your editor of choice.   
Scroll down the file a little, your looking for the `inmarsat_stdc_parser` section.   
I suggest you set `save_files` to false other wise you will forget and fill your hard drive - trust me on this one....      
On the `udp_sinks` set the `test` sink `IP` address to where you want your decoded data to go and the port number to match your sink.   
In my case, its a local 192.168 address of the PC running Node-RED and the port that the UDP in node is listening on.    
Save the file.    
    
I usually run the GUI once to get the offset. (I don't know any other way of getting it).   
Once you have the offset of the STDC signal, you can run the CLI version of satdump by something like this:    
### Windows   
`.\satdump.exe live inmarsat_stdc_c \tmp\ inmarsat_stdc_c --source rtlsdr --samplerate 250e3 --frequency 1537.73e6 --gain 37 --freq_shift 30475`   
### Linux   
``./satdump live inmarsat_std_c /tmp/satdump_out inmarsat_std_c --source rtlsdr --samplerate 250e3 --frequency 1541.49e6 --gain 32 --freq_shift 39143`   
   
Note how the frequency is not as per the list above, you want to move the STDC carrier away from the SDR center spike.   
Thus needing the offset from the gui and putting that number in as the --freq_shift on the CLI.