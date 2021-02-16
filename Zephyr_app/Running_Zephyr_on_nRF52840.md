#Running *Zephyr* on *nRF52840* board using `west` and *Eclipse* on Linux Ubuntu

##Connecting and flashing

By default `west` attempts to flash the software to *nRF52840*  with `nrfjprog`. In order to use the *JLink* connection following steps may be needed. Note that links and versions mentioned here are valid for 15-02-2021.

Instead of simple `west flash` a JLink runner must be specified by `west flash -r jlink` or `west flash --runner jlink`. In this case it may appear that the system does not know `jlink`.

From the page <https://www.segger.com/downloads/jlink/#J-LinkSoftwareAndDocumentationPack> download either 32-bit <https://www.segger.com/downloads/jlink/JLink_Linux_i386.deb> or 64-bit <https://www.segger.com/downloads/jlink/JLink_Linux_x86_64.deb> software, depending on what your system accepts. Save the file, do not attempt to run it straight from the browser. Install the package manually, be careful that it did not get "read only" attribute as it would make the installer reject it. The easiest way to install is to right-click it in the *File Browser*. 

With these steps completed your `west` should recognize the connected *nRF52840* and flash it successfully.

##Running the debugger

###Preparing the debugger itself

Since ordinary `gdb` does not fully work in this environment install `gdb-multiarch` with `sudo apt-get install gdb-multiarch`.

###Configuring debugger environment

To run the debugger from inside the *Eclipse* you need to set up the debug configuration. One of ways to get to it is through *Eclipse* menu `File` -> `Debug Configurations...`. There, you should take care on tab *Main* to select correct ELF file because in *Zephyr* environment there may be many of them.  
Next, in the *Debugger* tab and *J-Link GDB Server Setup* panel make sure that *Actual executable:* field shows `JLinkGDBServerCLExe` with the path appropriate for your *Eclipse* to find it. Note that this field is not editable, it only parses the contents of above field *Executable path:*.  
In the field *Device name:* enter `nRF52840_xxAA`. In case you use different board use neighbouring link *Supported device names* which sends you to <https://www.segger.com/products/debug-probes/j-link/technology/cpus-and-devices/overview-of-supported-cpus-and-devices/>. Note that this is not the actual list but you must take one more step from that page to <https://www.segger.com/downloads/supported-devices.php>. You will find there appropriate board code to enter.  
Scroll down and still in *Debugger* tab find panel *GDB Client Setup*. There fill the field *Executable name:* so that next field *Actual executable:* shows `gdb-multiarch` with appropriate path for your *Eclipse* to find it.  
The debugging congifuration is set and you can use it. Other parameters (which are many) can be left default or adjusted for your needs.

##Reading the *Zephyr* console output

`printk()` function in Zephyr environment lets you output to the board console. The console may be routed with *RTT* through the *JLink* debugger to your *Linux*. *RTT* stands for *Real-Time Tracing*.  

###Configuring the console to use *JLink* connection

You need to configure the *Zephyr* build system to use the *RTT*. In order to do that make sure that your `prj.conf` file contains following section:
    CONFIG_HAS_SEGGER_RTT=y
    CONFIG_USE_SEGGER_RTT=y
    CONFIG_RTT_CONSOLE=y  
You may also need to disable other routings for the *Zephyr* console with:
    CONFIG_UART_CONSOLE=n  
Rebuild the code and it will be using *RTT*.

###Accessing the *RTT* output

To see the output of *RTT* console you can use command line `JLinkRTTLogger` or GUI `JLinkRTTViewer`. Their default configurations are mostly sufficient. You may need to set *RTT Channel name or index:* to `0` instead of default `1`. For `JLinkRTTLogger` set *Output file:* to `/dev/stdout` if you want instant output.
