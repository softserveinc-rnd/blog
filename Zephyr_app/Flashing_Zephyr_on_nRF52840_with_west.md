#Connecting *nRF52840* board to *Zephyr* using `west` on Linux Ubuntu

By default `west` attempts to flash the software to *nRF52840*  with `nrfjprog`. In order to use the *JLink* connection following steps may be needed. Note that links and versions mentioned here are valid for 15-02-2021.

Instead of simple `west flash` a JLink runner must be specified by `west flash -r jlink` or `west flash --runner jlink`. In this case it may appear that the system does not know `jlink`.

From the page <https://www.segger.com/downloads/jlink/#J-LinkSoftwareAndDocumentationPack> download either 32-bit <https://www.segger.com/downloads/jlink/JLink_Linux_i386.deb> or 64-bit <https://www.segger.com/downloads/jlink/JLink_Linux_x86_64.deb> software, depending on what your system accepts. In my case I had to install 32-bit version despite 64-bit system. For some reason 64-bit package was not acceptable, however installing 32-bit one caused some other complications.

With 32-bit version on 64-bit system there in turn appeared problem with libraries required by `jlink`. So if you encounter one you may need to do following installations to your system:  
* `sudo apt-get install libgtk2.0-0:i386 libidn11:i386 libglu1-mesa:i386`
* `sudo apt-get install libsm6:i386`
* `sudo apt-get install libudev1:i386`

Having all those steps completed your `west` should recognize the connected *nRF52840* and flash it successfully.
