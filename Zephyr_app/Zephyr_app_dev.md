
# **Zephyr RTOS: Application development**

 ***Introduction***

The previous blog considered general issues related to Zephyr RTOS. This part moves further and deals with application development process in more detail.

Being the Linux Foundation project Zephyr naturally inherits its best development features and tools:

- established infrastructure for existing platforms compilation with simple extension tools

- powerful drivers development tool based on device tree structure approach

- flexible and orthogonal configuration

- easy IDE and Python integration, powerful command line tool

- POSIX compatible API

It is also worth mentioning that:

- Since Zephyr supports very large number of boards it naturally uses _cmake_ software building tool which is intrinsically cross-platform and compiler independent

- Zephyr uses its own command line tool called _west._ This meta-tool provides a multiple repository management system, makes configuration simpler and apart from its own built-in commands it also allows adding custom commands. This makes _west_ quite flexible and powerful. West is used for building, flashing and debugging applications. However, it is not obligatory for Zephyr development

- Zephyr extensively uses Python 3 and its package manager for installing and running scripts used to compile, build, and run applications.

 ***Getting started***

To start application development the following steps must be performed:

- Install _cmake_ version 3.13.1 or higher

- Install _west_

- Run _west init_ [target directory] command

- Switch to [target directory] and run _west update_

The last two commands result in the latest Zephyr OS repository in the target directory. To complete the setup process Zephyr&#39;s Software Development Kit (SDK) must be downloaded and installed. Proper environmental variables must be set and scripts run. When building with the help of Zephyr toolchain the following environmental variables are to be set as:

- export ZEPHYR\_TOOLCHAIN\_VARIANT=zephyr
- export ZEPHYR\_SDK\_INSTALL\_DIR **=** [zephyr sdk location]

Zephyr has a rich set of examples demonstrating how various peripheries, drivers, etc function.

After all the above steps are performed, building the sample application for the specific board will be the following:

_west build -b [board\_name] [sample code directory]_

_Eest_ can be also used to flash the recently built sample application binary on specific board.

While it is quite easy and straightforward to build, flash and run the sample Zephyr application, it may turn out to be more challenging to get through these stages for the custom application, especially for the custom boards.

## **Application development. Standard boards**

Zephyr&#39;s base directory hosts Zephyr&#39;s own source code, its kernel configuration options, and its build definitions. It can reside anywhere, but, in fact, location is controlled by _west update_ command where [target directory] for Zephyr&#39;s own code is specified. For application to know this location as well as other setting parameters the _zephyr-env.sh_ script residing in root Zephyr&#39;s directory must run prior to application building.

Zephyr&#39;s application folder ( **app** ) has to contain at least the following files: CmakeLists.txt, prj.conf, Kconfig, src/\*.c.
``` ```
``` ``` 
``` ```
``` ```
``` ```
``` ```
``` ```
- **CmakeLists.txt.** This file specifies the minimum CMake version required as well as the location of application source code files. It also links the application directory with Zephyr&#39;s CMake build system. This link provides features supported by Zephyr&#39;s build system, such as board-specific kernel configuration files, etc.
- **prj.conf**. This is one out of two principal kernel and application configuration files (the other is Kconfig file). In this file various configuration options tailoring kernel for specific application are to be defined.
- **Kconfig**. This file also contains configuration information but of different type than **prj.conf** does. The other difference between them is that there exists a deep hierarchy of Kconfig files spread over different Zephyr&#39;s kernel levels.
- **Application source code files.** Source code files should be placed in the _src_ directory. Code can be written in C, Assembly and C++ language. Support for the latter is not complete for now, but it is intensively being developed.

Eventually, running the command

_west build -b [board\_name] ._

from application directory **app** will result in binary image being built and placed in automatically created **build/zephyr** folder.

### **Build control**

Zephyr build system is very flexible. For this purpose it uses many variables.

The most used variables are ZEPHYR_BASE, BOARD , and DTC_OVERLAY_FILE. They can be supplied to the build system in different ways, namely, as either parameters to _west_ command or as the environmental variable, or as a proper statement in CMakeLists.txt file.

As the name implies, BOARD variable specifies the board name for the build system. Earlier we showed how it can be specified as an argument to west command.

DTC_OVERLAY_FILE variable is used to redefine or extend the board setting while building for the custom board.

### **Build phases**

The Zephyr build process consists of two main stages:

- configuration - driven by CMake
- build - driven by Make (or Ninja)

***Configuration stage***

Configuration stage is rather complicated involving many files throughout the Zephyr hierarchy. As the basic input it takes device tree sources (\*.dtsi files) specified for each board supported by Zephyr, as well as `CmakeLists.txt, Kconfig and prj.conf files. `For example, _CMake_ begins by processing the `CmakeLists.txt` file in the application directory, which refers to the `CmakeLists.txt` file in the Zephyr top-level directory, which in turn refers to `CmakeLists.txt` files throughout the build tree (directly and indirectly). Header files for the build stage are an expected output of the configuration stage. _devicetree\_unfixed.h_ and _devicetree\_fixups.h_ are intermediate files of interestcontaining basic configuration information. Final output configuration files are _autoconf.h, .config, devicetree.h_ as wellas _Makefile._ So,header files are generated automatically as a result of configuration stage.The figure below provides the described configuration workflow in detail (find the source and more detail at [zephyrproject.org](https://docs.zephyrproject.org/latest/guides/build/index.html)):

![Arch](build-config-phase_2.svg)

***Build stage***

Compilation process, in its turn, can be also subdivided into two stages.

At the **first** and **principal** stage, the source files from various subsystems are included into build, dependent on configuration setting made at the previous stage. They are compiled into archives with reference to header files in the tree. Header files generated during the configuration phase are included as well. Binary **zephyr\_prebuilt.elf** is generated at this stage.

Final binary image **zephyr.elf** is generated at the **second** stage, which is needed because the binary from the previous stage is incomplete in some configurations, containing empty placeholder sections that must be filled in. Dedicated Python script runs to gather missed information and eventually final binary is built. Details can be found at [zephyrproject.org](https://docs.zephyrproject.org/latest/guides/build/index.html).

Optionally, at post-processing stage an _elf_ file may be converted to _bin_ or _hex_ formats.

## **Application development. Custom boards**

The process becomes a little bit complicated while developing application for a custom board. The device tree structure describing the board hardware is already predefined for the popular boards and thus is well described. This is definitely not a case for a custom board. Fortunately, the majority of custom boards are based upon one of the known MPUs. This fact essentially simplifies the development process. For this purpose, Zephyr introduced a notion of device tree overlays. Let&#39;s consider how it works for the custom hardware with the environmental sensors on board.

***Enabling known sensor*** 

Zephyr has implemented drivers for the vast majority of sensors. If the custom hardware has a sensor on board then Zephyr build system must be properly configured to include sensor functionality in the final binary image. Let&#39;s show this for _nrf52840 pca10056_ from Nordic Semiconductor with MEMS nano pressure sensor lps22hb from STM on board.

So, the device tree structure for _nrf52840_ does not contain _lps22hb_. To have _lps22hb_ working with _nrf52840_ we have to include sensor into configuration files. This requires the following steps:

1. In the **prj.conf** file (in application directory **app)** add the lines:

...

CONFIG\_SENSOR=y

CONFIG\_LPS22HB=y

...

1. In the same application folder create the overlay file _nrf52840\_pca10056__.overlay_ with the following content:

&amp;i2c0 {

compatible = &quot;nordic,nrf-twi&quot;;

status = &quot;okay&quot;;

sda-pin = \&lt;26\&gt;;

scl-pin = \&lt;25\&gt;;

clock-frequency = \&lt;I2C\_BITRATE\_FAST\&gt;;

...

lps22hb-press@5c {

compatible = &quot;st,lps22hb-press&quot;;

reg = \&lt;0x5c\&gt;;

label = &quot;LPS22HB&quot;;

};

...

};

_overlay_ file has the same structure as _dtsi_ file so its information just extends or redefines the basic device tree information.

In our example, i2c setting are redefined since the custom i2c pin configuration is used instead of the default one. Second, the sensor information is provided, in particular, its id.

Including sensor configuration in _prj.conf_ file and creating the overlay file is all that is needed to enable the sensor for the custom board in Zephyr. All the rest, e.g. generating the properly updated header files, is done by Zephyr itself.

***Adding new sensor***

If the sensor driver is not implemented in Zephyr all the job done by Zephyr in case of known sensor should now be performed manually by the developer. Let&#39;s go through all these steps for **ICM-20948** motion tracking device from TDK.

Several files must be added or modified throughout Zephyr hierarchy.

- Create **icm20948** folder in **../zephyr/drivers/sensor/** directory. In **Kconfig** file place at least the following:place at least the following:

_config ICM20948_

_bool &quot;ICM20948 motion tracking sensor&quot;_

_depends on (I2C &amp;&amp; HAS\_DTS\_I2C)_

_help_

_Enable driver for ICM20948._

- In **CMakeLists.txt** file add all **ICM-20948** related source files , e.g.:

_zephyr\_library()_

_zephyr\_library\_sources\_ifdef(CONFIG\_ICM20948 deviceIcm20948.c)_

- In the same **icm20948** folder add proper source files

- In the folder **../zephyr/dts/bindings/sensor** create **tdk,icm20948.yaml** file and fill it with the following code:

_title: TDK motion tracking sensor_

_description:_

_This is a representation of the TDK motion tracking sensor_

_compatible: &quot;tdk,icm20948&quot;_

_include: i2c-device.yaml_

- In the **../zephyr/drivers/sensor** folder edit **CmakeLists.txt** fileby adding the code line:

_add\_subdirectory\_ifdef(CONFIG\_ICM20948 icm20948)_

- In the **../zephyr/drivers/sensor** folder edit file **Kconfig** by adding the code line:

_source &quot;drivers/sensor/icm20948/Kconfig&quot;_

All the above mentioned steps enable ICM-20948 sensor driver and make it possible to be used like all the other sensors, including Zephyr&#39;s sensor API.

Zephyr philosophy considers sensors as part of hardware. As a result, like all basic hardware, Zephyr wants sensors to be initialized during the preliminary step, in any case at some time point prior to start of the application&#39;s main function. Thus, when the main part of application starts the sensors, d, are ready for use (if properly setup and initialize) and what is needed by developer is to obtain the sensor handle by unique sensor name and to use sensors API functions to manipulate with sensor data.

## **Conclusion**

In this blog we learned about the process of Zephyr application development. Specific case applying the environmental sensors was considered. Probably at the first glance it is not easy to work with Zephyr. Using SDK and toolchain developed just for certain SoC or MPU is usually more straightforward. Within such an approach, moving to another board presents a need in getting familiar with new SDK and new toolchain. Using Zephyr makes a process of migrating from one board to another smooth and flexible. Anyway, Zephyr is definitely worth of paying extra attention to it.
