
DOS Flash Utility
=================


HOW TO USE: 

Download rufus or unetbootin to make a FreeDOS bootable USB. Copy the contents of this specific directory to the root of your new FreeDOS USB, boot from the external USB by pressing F9, and then once you change your directory to C:\, just type: 

dosflash 

and follow the steps which will guide you to update your firmware



DOSFlash.exe - Use locally or with a Preboot eXecution Environment (PXE) 
               management application (e.g. Altiris eXpress) to update or
               restore the System BIOS. 


NOTE:  A BIOS update may be done using these utilities from a USB hard drive
or a USB flash media device.  Copy all the files in this folder to a DOS 
bootable medium.  Make sure that the device you want to boot from is connected
to the computer to be upgraded and power cycle the computer.  When the system 
boots to the USB device, the BIOS update may then be performed.  
See DOSFlash.txt for syntax.


Files included in this folder:

BIOS image binary file (ex: L01_0270.bin)
DOSFlash.exe
DOSFlash.txt
FlshUefi.cpu
MD5.txt    
SHA256.txt
README.TXT (this file)

Copyright (c) 2011-2016 HP Development Company, L.P.
