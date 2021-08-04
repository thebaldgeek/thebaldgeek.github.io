# How to use SDRReceiver to send data to Jaero.   
   
Navigation: [home](README.md)  

The old way to send data from your SDR software to Jaero was to use virtual audio cables (VAC). This was very fragile, CPU intensive, expensive (a licensed copy of VAC was required) and each SDR software package had its up and down's. Issues ranged from unpredictable lockups/crashes, PC hangs, high CPU use, memory leaks, convoluted graphical interfaces and a lot of unneeded features (bloat). It also made the option of running on Linux just about impossible. With satcom you just need the frequency to be sent to each Jaero the most efficient way possible with out needing constant monitoring and restarts. Most systems even run headless and you never need to look at the actual SDR software for months at at time.   
  
  In August 2021, a new SDR receiver and version of Jaero were released that solved all these issues.   
  ## Big Picture   
SDRReceiver uses an ini file to set its frequencies. It is not visual point-and-click software. You put the center frequency in the file, then sub VFO frequencies and name them, Jaero then picks up the data from the VFO names.  
There are two main parts to getting the whole system working, SDRReceiver and its ini file and starting Jaero with a batch file, setting up each Jaero with the correct port number and VFO name. You only have to configure everything once.
  ## Install SDRReceiver on Windows  
  Visit the github page and download the zip file.   
  <https://github.com/jeroenbeijer/SDRReceiver>  
  The download is on the right, click on the 'Releases', then on that page, at the bottom, click on 'Assets' and select the file with win_x86 in it.  
  This will download it on your PC, once there, extract it into a directory of your liking. You don't have to install it, so it will be run from the directory you extract it. I simply left it in my downloads folder.   
  ## Satellite ini file    
  Once you have downloaded and unzipped the receiver software, the next thing is to get your satellite ini file and copy or create it in the same directory as SDRReceiver.   
  At the time of me typing this, there are only a few ini files for the satellites. I hope that the community will share their files and we can have them all on this website to download.   
  For now, there are a few here: <https://github.com/jeroenbeijer/SDRReceiver/tree/master/sample_ini>   
  The main missing one is L-Band for 143E. If you have it, please let me know.    
  Download the .ini file into the same directory as your SDRReceiver unzipped into.   
  No, from Windows Explorer, hold down the left shift key and right mouse click to pull up the menu. From that pop up menu select either Open Command Prompt, or Open Power Shell Here. (depending on your version of Windows).   
  That will open a back or blue box, now start typing the command `SDR` and hit the tab key, this will auto complete the command to the .exe and then you just add `-s` and then name of your ini file.   
  The full command is thus `.\SDRReceiver.exe -s 54w.ini`   
  If you computer throws an error that it cant find the ini, then Windows might have saved it with a hidden .txt extension, so type this: `.\SDRReceiver.exe -s 54w.ini.txt`  
  It should work. If not, then you did not put the .ini file in the same directory as the SDRReceiver software.