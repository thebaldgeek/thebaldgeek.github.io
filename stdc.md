# STD-C aka InmarsatC aka NCSC aka EGC aka Marine Messages.   
   
Navigation: [home](README.md)  

STDC provides a range of messages to ship crew. They are 'offical' messages rather than personal email or text messages.   
These messages can be decoded via a few different software packages, some Linux only, some Windows only, some cross platform.   
All these programs decode the same 1200 bps DBPSK Network Control Station Channel (NCSC).
The main frequencies are known as Enhanced Group Call (EGC), which allows official broadcast messages to be sent to selected groups of ship stations located anywhere within a satellite's coverage.   
The usual four Inmarsat geostationary satellites provide worldwide coverage for these types of broadcasts.    
You will find them on the following frequenices:   
   
98w. 4F3. AOR-W: 1537.70 MHz   
   
25e. 4AF4. IOR: 1537.10 MHz   
   
54w. 3F5. AOR-E: 1541.45 MHz   
   
143e. 4F1. POR: 1541.45 MHz   
    
Most people seem to be using the RTLSDR v3 patch antenna, but a ~7 turn RHCP helix with LNA would be better, or a 3-4 turn LHCP helix pointing at a dish would be better still.
The signal is easy to find as it is a continous carrier even when no messages are being sent.

Software options:
InmarsatDecoder (~$50USD) Windows.   
Teckmanoid (~$50USD) Crossplatform (Java required)   
Scytale-C (Free) Crossplatform with some work.    
SDR++ STD-C demodulator plug-in and QT Inmarsat-C Parser. (Free). Linux only   

