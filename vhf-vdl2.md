# Flows to work with VHF VDL2.   
   
Navigation: [home](README.md)  

There are two main decoders that use an SDR and decode VDL2 data (I only ran either of these on a Raspberry Pi. If you are installing on Windows - good luck).    

Both vdlm2dec and dumpvdl2 can work with Node-RED. In fact they are very similar to install and use. They both output their data in JSON but only dumpvdl2 has a decoded text option.   
Part of the problem with both of them is that neither author lists all the options of the JSON keys their programs can produce in their docs, this makes it hard for me to write a Node-RED flow that can intelligently deal with unknown keys as they come across the wire. I'm sure if you dug into their code they would probably have an array somewhere in a file that lists all the possible key pairs that their program could show in an given message. I'm also sure that if you knew how to program there is probably a well known method to deal with random key pairs in your code.   

Note that vdlm2dec requires its command line frequencies to be in Mhz while dumpvdl requires them to be in Hz. 

**Feeding VDL2 data to Node-RED**    
Both programs (well, all three if you count the ACARS decoder) will take a command line option to stream the decoded message via UDP. I simply point that stream to my hostname:port and have a UDP in node listening on that port.     

## dumpvdl ##   
Here is a partial flow will display some of the main text values that come in on a decoded text stream from dumpvdl.  
    
    [{"id":"27278a8d.356866","type":"udp in","z":"5e5fdc91.d8f9d4","name":"Uk","iface":"","port":"112233","ipv":"udp4","multicast":"false","group":"","datatype":"utf8","x":2040,"y":1380,"wires":[["85112668.5314d8","63e7b7fa.3dbca8","ae622b78.e1ec48","ae6e4362.9c512","a4d431d5.84261"]]},{"id":"85112668.5314d8","type":"msg-speed","z":"5e5fdc91.d8f9d4","name":"","frequency":"min","estimation":false,"ignore":false,"x":2210,"y":1380,"wires":[["dd053c0a.85401"],["b01b47b.d90c2b8","9a9f2355.0e9eb"]]},{"id":"b01b47b.d90c2b8","type":"switch","z":"5e5fdc91.d8f9d4","name":"frequency counter","property":"payload","propertyType":"msg","rules":[{"t":"cont","v":"136.725","vt":"str"},{"t":"cont","v":"136.775","vt":"str"},{"t":"cont","v":"136.800","vt":"str"},{"t":"cont","v":"136.975","vt":"str"},{"t":"else"}],"checkall":"false","repair":false,"outputs":5,"x":2450,"y":1340,"wires":[["7e35bf77.81579"],["bddb221b.8cf9d"],["fa937852.523268"],["4ca4ddca.ab0714"],[]]},{"id":"7e35bf77.81579","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1260,"wires":[["ebf306d.eeed3f8"]],"l":false},{"id":"bddb221b.8cf9d","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1300,"wires":[["dd625424.044428"]],"l":false},{"id":"63e7b7fa.3dbca8","type":"debug","z":"5e5fdc91.d8f9d4","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":2210,"y":1460,"wires":[]},{"id":"fa937852.523268","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1340,"wires":[["b09868e3.aa1528"]],"l":false},{"id":"4ca4ddca.ab0714","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1380,"wires":[["927bfee8.ebf32"]],"l":false},{"id":"dd053c0a.85401","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":2,"width":1,"height":1,"name":"","label":"msg per min: ","format":"{{msg.payload}}","layout":"row-left","x":2458,"y":1227,"wires":[]},{"id":"927bfee8.ebf32","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":7,"width":2,"height":1,"name":"","label":"136.975 = ","format":"{{msg.payload}}","layout":"row-left","x":2810,"y":1380,"wires":[]},{"id":"b09868e3.aa1528","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":5,"width":2,"height":1,"name":"","label":"136.800 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1340,"wires":[]},{"id":"ebf306d.eeed3f8","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":1,"width":2,"height":1,"name":"","label":"136.725 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1260,"wires":[]},{"id":"dd625424.044428","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":3,"width":2,"height":1,"name":"","label":"136.775 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1300,"wires":[]},{"id":"9a9f2355.0e9eb","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1420,"wires":[["8772957f.b74d78"]],"l":false},{"id":"8772957f.b74d78","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":4,"width":1,"height":1,"name":"","label":"Total: ","format":"{{msg.payload}}","layout":"row-left","x":2790,"y":1420,"wires":[]},{"id":"a38ae90b.462a58","type":"ui_group","name":"UK","tab":"733f36e1.cf5db8","order":7,"disp":true,"width":3,"collapse":false},{"id":"733f36e1.cf5db8","type":"ui_tab","name":"VHF-VDL2","icon":"flight","order":7,"disabled":false,"hidden":false}]  

**Building dumpvdl**  
Here are some rough notes to build dumpvdl. This is a very bear bones build. We turn off pretty much all the options that dumpvdl supports. We simply want to move the decoded text from the station location to a central Node-RED.  

`sudo apt-get install build-essential cmake git libglib2.0-dev pkg-config`   
`cd`  
`git clone https://github.com/szpajder/libacars`  
`cd libacars`  
`mkdir build`  
`cd build`  
`cmake ../`  
`make`  
`sudo make install`  
`sudo ldconfig`  
`sudo apt-get install librtlsdr-dev`
`cd`  
`git clone git://git.osmocom.org/rtl-sdr.git`  
`cd rtl-sdr/`  
`mkdir build`  
`cmake ../`  
`make`  
`sudo make install`  
`sudo ldconfig`  
`sudo nano /etc/modprobe.d/blacklist.conf`  
Add the following line, save and exit the file: blacklist dvb_usb_rtl28xxu  
Reboot the Pi  
`cd`  
`git clone https://github.com/szpajder/dumpvdl2.git`  
`cd dumpvdl2`  
`mkdir build`  
`cmake -DMIRISDR=FALSE -DSDRPLAY=FALSE -DSOAPYSDR=FALSE -DSQLITE=FALSE -DETSY_STATSD=FALSE -DRAW_BINARY_FORMAT=FALSE -DZMQ=FALSE ../`  
`make`  
`sudo make install`  

Here is an example command to listen on a few frequencies (check out airframes.io/about for a good list of VDL2 frequencies to listen on in your part of the world) and stream the decded messages to a URL and port that your Node-RED should be listening on:   

`dumpvdl2 --rtlsdr -0 --gain 42 --correction 7 --output decoded:text:udp:address=yourWebSite.com,port=112233 136725000 136775000 136800000 136975000`
   
Once you are happy with the output and the input to Node-RED, you can then setup dumpvdl2 to launch in the background and when the Pi boots:  
  
`cd /home/pi/dumpvdl2`  
`sudo cp etc/dumpvdl2.service /etc/systemd/system/`  
`sudo cp etc/dumpvdl2 /etc/default/`  
`sudo nano /etc/default/dumpvdl2`  
In that file, uncomment the DUMPVDL2_OPTIONS= and put your options from the test you just ran in to the file, save and exit it - it will look something like this:  
  
`DUMPVDL2_OPTIONS="--rtlsdr -0 --gain 42 --correction 7 --output decoded:text:udp:address=yourWebSite.com,port=112233 136725000 136775000 136800000 136975000"`  
  
`sudo systemctl daemon-reload`  
`sudo systemctl start dumpvdl2`  
`systemctl status dumpvdl2`  
`systemctl enable dumpvdl2`  

- - - - 
## vdlm2dec ##  
Even though I don't use it since I cant handle the random JSON keys, here is a partial flow that displays some of the main key value pairs for vdlm2dec via JSON.    
    
    [{"id":"27278a8d.356866","type":"udp in","z":"5e5fdc91.d8f9d4","name":"Uk","iface":"","port":"112233","ipv":"udp4","multicast":"false","group":"","datatype":"utf8","x":2030,"y":1380,"wires":[["85112668.5314d8","4c65059e.1c8c4c"]]},{"id":"85112668.5314d8","type":"msg-speed","z":"5e5fdc91.d8f9d4","name":"","frequency":"min","estimation":false,"ignore":false,"x":2210,"y":1380,"wires":[["dd053c0a.85401"],["b01b47b.d90c2b8","9a9f2355.0e9eb"]]},{"id":"b01b47b.d90c2b8","type":"switch","z":"5e5fdc91.d8f9d4","name":"frequency counter","property":"payload","propertyType":"msg","rules":[{"t":"cont","v":"136.650","vt":"num"},{"t":"cont","v":"136.725","vt":"num"},{"t":"cont","v":"136.775","vt":"num"},{"t":"cont","v":"136.800","vt":"num"},{"t":"cont","v":"136.825","vt":"num"},{"t":"cont","v":"136.875","vt":"num"},{"t":"cont","v":"136.975","vt":"num"},{"t":"else"}],"checkall":"false","repair":false,"outputs":8,"x":2450,"y":1340,"wires":[["ce4baf35.883c4"],["7e35bf77.81579"],["bddb221b.8cf9d"],["fa937852.523268"],["19528aa2.bd25f5"],["3ccff35e.aac23c"],["4ca4ddca.ab0714"],[]]},{"id":"ce4baf35.883c4","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1220,"wires":[["534ea04c.ea31"]],"l":false},{"id":"7e35bf77.81579","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1260,"wires":[["ebf306d.eeed3f8"]],"l":false},{"id":"bddb221b.8cf9d","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1300,"wires":[["dd625424.044428"]],"l":false},{"id":"63e7b7fa.3dbca8","type":"debug","z":"5e5fdc91.d8f9d4","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":2150,"y":1540,"wires":[]},{"id":"fa937852.523268","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1340,"wires":[["b09868e3.aa1528"]],"l":false},{"id":"19528aa2.bd25f5","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1380,"wires":[["df38d989.ddb808"]],"l":false},{"id":"3ccff35e.aac23c","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1420,"wires":[["53a473c3.ca150c"]],"l":false},{"id":"4ca4ddca.ab0714","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2675,"y":1460,"wires":[["927bfee8.ebf32"]],"l":false},{"id":"dd053c0a.85401","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":17,"width":1,"height":1,"name":"","label":"msg per min: ","format":"{{msg.payload}}","layout":"row-left","x":2458,"y":1227,"wires":[]},{"id":"927bfee8.ebf32","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":19,"width":2,"height":1,"name":"","label":"136.975 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1460,"wires":[]},{"id":"534ea04c.ea31","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":1,"width":2,"height":1,"name":"","label":"136.650 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1220,"wires":[]},{"id":"b09868e3.aa1528","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":2,"width":2,"height":1,"name":"","label":"136.800 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1340,"wires":[]},{"id":"ebf306d.eeed3f8","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":7,"width":2,"height":1,"name":"","label":"136.725 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1260,"wires":[]},{"id":"dd625424.044428","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":13,"width":2,"height":1,"name":"","label":"136.775 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1300,"wires":[]},{"id":"df38d989.ddb808","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":8,"width":2,"height":1,"name":"","label":"136.825 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1380,"wires":[]},{"id":"53a473c3.ca150c","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":14,"width":2,"height":1,"name":"","label":"136.875 = ","format":"{{msg.payload}}","layout":"row-left","x":2800,"y":1420,"wires":[]},{"id":"4c65059e.1c8c4c","type":"json","z":"5e5fdc91.d8f9d4","name":"","property":"payload","action":"","pretty":false,"x":2190,"y":1480,"wires":[["63e7b7fa.3dbca8","f8d13f15.5590c","527949ed.e9eb68","b6253ede.f08e3","102aaa94.c920d5","eda5e162.ec41c","6efac09a.a2f69"]]},{"id":"f8d13f15.5590c","type":"function","z":"5e5fdc91.d8f9d4","name":"icao","func":"msg.icaoString = msg.payload.icao.toString(16);\nmsg.gsid = msg.payload.toaddr.toString(16);\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","libs":[],"x":2410,"y":1460,"wires":[["62c4d94f.b25828","7d3510bb.8054b"]]},{"id":"62c4d94f.b25828","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":4,"width":1,"height":1,"name":"","label":"ICAO: ","format":"{{msg.icaoString}}","layout":"row-left","x":2550,"y":1460,"wires":[]},{"id":"7d3510bb.8054b","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":10,"width":1,"height":1,"name":"","label":"GS ID: ","format":"{{msg.gsid}}","layout":"row-left","x":2544,"y":1497,"wires":[]},{"id":"527949ed.e9eb68","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":5,"width":2,"height":1,"name":"","label":"Tail: ","format":"{{msg.payload.tail}}","layout":"row-left","x":2550,"y":1540,"wires":[]},{"id":"b6253ede.f08e3","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":11,"width":2,"height":1,"name":"","label":"Flight: ","format":"{{msg.payload.flight}}","layout":"row-left","x":2550,"y":1580,"wires":[]},{"id":"102aaa94.c920d5","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":16,"width":6,"height":1,"name":"","label":"Data: ","format":"{{msg.payload.data}}","layout":"row-left","x":2550,"y":1620,"wires":[]},{"id":"eda5e162.ec41c","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":21,"width":6,"height":1,"name":"","label":"Text: ","format":"{{msg.payload.text}}","layout":"row-left","x":2550,"y":1660,"wires":[]},{"id":"6efac09a.a2f69","type":"function","z":"5e5fdc91.d8f9d4","name":"","func":"msg.ts = new Date(msg.payload.timestamp * 1000);\nmsg.ts = msg.ts.toISOString().slice(msg.ts.length,-5);\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","libs":[],"x":2435,"y":1700,"wires":[["76d49f7b.2597e"]],"l":false},{"id":"76d49f7b.2597e","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":6,"width":3,"height":1,"name":"","label":"Last msg: ","format":"{{msg.ts}}","layout":"row-left","x":2560,"y":1700,"wires":[]},{"id":"9a9f2355.0e9eb","type":"counter","z":"5e5fdc91.d8f9d4","inc":"1","name":"","x":2435,"y":1740,"wires":[["8772957f.b74d78"]],"l":false},{"id":"8772957f.b74d78","type":"ui_text","z":"5e5fdc91.d8f9d4","group":"a38ae90b.462a58","order":18,"width":1,"height":1,"name":"","label":"Total: ","format":"{{msg.payload}}","layout":"row-left","x":2550,"y":1740,"wires":[]},{"id":"a38ae90b.462a58","type":"ui_group","name":"UK","tab":"733f36e1.cf5db8","order":7,"disp":true,"width":11,"collapse":false},{"id":"733f36e1.cf5db8","type":"ui_tab","name":"VHF-VDL2","icon":"flight","order":7,"disabled":false,"hidden":false}]

 