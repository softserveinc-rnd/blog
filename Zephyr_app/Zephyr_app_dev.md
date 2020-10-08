
# **Zephyr RTOS: Application development**

### Introduction

The previous blog considered general issues related to Zephyr RTOS. This part moves further and deals with the application development process in more detail.

Being the ***Linux Foundation*** project, Zephyr naturally inherits its best development features and tools:

- established infrastructure for existing platforms compilation with simple extension tools

- powerful drivers development tool based on device tree structure approach

- flexible and orthogonal configuration

- easy IDE and Python integration, a powerful command-line interface (CLI)

- POSIX compatible API

It is also worth mentioning that:

- Since Zephyr supports a very large number of boards, it naturally uses _Cmake_ software building tool which is intrinsically cross-platform and compiler independent

- Zephyr uses its own CLI called _west._ This meta-tool provides a multiple repository management system, that makes configuration simpler and apart from its own built-in commands it also allows adding custom commands. This makes _west_ quite flexible and powerful. West is used for building, flashing and debugging applications. However, it is not obligatory for Zephyr development

- Zephyr extensively uses Python 3 and its package manager for installing and running scripts used to compile, build, and run applications.

 ### Getting started

Zephyr OS has such wonderful documentation for all systems [[Ref]](https://docs.zephyrproject.org/latest/getting_started/installation_linux.html), so it is hard to recommend something better.

### Application development. Standard boards

Zephyr's base directory hosts the system's source code, its kernel configuration options, and its build definitions. It can reside anywhere, but, in fact, location is controlled by `west update` command where [target directory] for Zephyr's own code is specified. Execute `source <path_to_zephyrproject_dir>/zephyr/zephyr-env.sh` command to set all variables and prepare your environment for working with the system.

Zephyr's application folder `app` has to contain at least the following files: `CmakeLists.txt`, `prj.conf`, `Kconfig`, `src/\*.c`.
- **CmakeLists.txt** file specifies the minimum CMake version required as well as the location of application source code files. It also links the application directory with Zephyr's CMake build system. This link provides features supported by Zephyr's build system, such as board-specific kernel configuration files etc.
- **prj.conf** is one out of two principal kernel and application configuration files (the other is Kconfig file). In this file, various configuration options tailoring kernel for a specific application to be defined.
- **Kconfig** file also contains configuration information, but of a different type than `prj.conf` does. The other difference between them is that there exists a deep hierarchy of Kconfig files spread over different Zephyr's kernel levels.
- **Application source code files.** Source code files should be placed in the `src` directory. Code can be written in C, Assembly and C++ languages. Support for the latter is not complete for now, but it is intensively being developed.

Eventually, running the command ``` west build -b [board\_name] ``` from the application directory `app` will result in a binary image being built and placed in automatically created `build/zephyr` folder.

### Build control

Zephyr build system is very flexible. For this purpose, it uses many variables.

The most important variables are `ZEPHYR_BASE`, `BOARD` and `DTC_OVERLAY_FILE`. They can be supplied to the build system in different ways, namely, either as parameters to `west` command or as the environmental variable, or as a proper statement in `CMakeLists.txt` file.

As the name implies, the `BOARD` variable specifies the board name for the build system. Earlier it has been shown how it can be specified as an argument to the `west` command.

`DTC_OVERLAY_FILE` variable is used to redefine or extend the board setting while building for the custom board.

### Build phases

The Zephyr build process consists of two main stages:

- configuration - driven by CMake
- build - driven by Make (or Ninja)

##### Configuration stage

Configuration stage is rather complicated involving many files throughout the Zephyr hierarchy. As the basic input, it takes device tree sources (`\*.dtsi` files) specified for each board supported by Zephyr, as well as `CmakeLists.txt`, `Kconfig` and `prj.conf` files. For example, the CMake begins with processing the `CmakeLists.txt` file in the application directory, which refers to the `CmakeLists.txt` file in the Zephyr top-level directory, which in turn refers to `CmakeLists.txt` files throughout the build tree (directly and indirectly). Header files for the build stage are an expected output of the configuration stage. _devicetree\_unfixed.h_ and _devicetree\_fixups.h_ are intermediate files of interest containing basic configuration information. Final output configuration files are _autoconf.h, .config, devicetree.h_ as well as _Makefile_. So, header files are generated automatically as a result of the configuration stage. The figure below provides the described configuration workflow in detail (find the source and more detail at [zephyrproject.org](https://docs.zephyrproject.org/latest/guides/build/index.html)):

![Arch](build-config-phase_2.svg)

##### Build stage

Compilation process, in its turn, can also be subdivided into two stages.

At the **first** and **principal** stage, the source files from various subsystems are included into the build, dependent on configuration setting made at the previous stage. They are compiled into archives with reference to header files in the tree. Header files generated during the configuration phase are included as well. Binary `Zephyr \_prebuilt.elf` is generated at this stage.

Final binary image `zephyr.elf` is generated at the **second** stage, which is needed because the binary from the previous stage is incomplete in some configurations, containing empty placeholder sections that must be filled in. Dedicated Python script runs to gather missed information and eventually final binary is built. Details can be found at [zephyrproject.org](https://docs.zephyrproject.org/latest/guides/build/index.html).

Optionally, at the post-processing stage, an `.elf file may be converted to the `.bin` or `.hex` formats.

### Application development. Custom boards

The process becomes more complicated while developing an application for a custom board. The device tree structure describing the board hardware is already predefined for the popular boards and thus is well described. This is definitely not a case for a custom board. Fortunately, the majority of custom boards are based upon one of the known MPUs. This fact essentially simplifies the development process. For this purpose, Zephyr introduced a notion of device tree overlays. Let's consider how it works for the custom hardware with the environmental sensors on board.

##### Enabling known sensor

Zephyr has implemented drivers for the vast majority of sensors. If the custom hardware has a sensor on a board, then Zephyr build system must be properly configured to include sensor functionality in the final binary image. Let's show this for the `nrf52840 pca10056` board from Nordic Semiconductor with MEMS nano pressure sensor `lps22hb` from STM on board.

So, the device tree structure for the `nrf52840` does not contain `lps22hb`. To have `lps22hb` working with `nrf52840`, we have to include sensor into configuration files. This requires the following steps:

1. In the `prj.conf` file (in application directory `app/`) add the following:
```
CONFIG\_SENSOR=y
CONFIG\_LPS22HB=y
```

2. In the same application folder, create the overlay file `nrf52840\pca10056.overlay` with the following content:
```
&i2c0 {
	compatible = "nordic,nrf-twi";
	status = "okay";
	sda-pin = <26>;
	scl-pin = <25>;
	clock-frequency = <I2C\_BITRATE\_FAST\>
	...
	lps22hb-press@5c {
		compatible = "st,lps22hb-press";
		reg = <0x5c>;
		label = "LPS22HB"
	};
	...
};
```
`overlay` file has the same structure as `dtsi` file, so its information just extends or redefines the basic device tree information.

In our example, i2c setting is redefined since the custom `i2c` pin configuration is used instead of the default one. Second, the sensor information is provided, in particular, its id.

Including sensor configuration in `prj.conf` file and creating the `overlay` file is all that is needed to enable the sensor for the custom board in Zephyr. All the rest, e.g. generating the properly updated header files, is done by Zephyr itself.

##### Adding a new sensor

If the sensor driver is not implemented in Zephyr all the job done by Zephyr in case of the known sensor should now be performed manually by the developer. Let's go through all these steps for **ICM-20948** motion tracking device from TDK.

Several files must be added or modified throughout the Zephyr hierarchy.

- Create `icm20948/` folder in `../zephyr/drivers/sensor/` directory. In the `Kconfig` file place at least the following:
```
config ICM20948
	bool "ICM20948 motion tracking sensor"
	depends on (I2C && HAS\_DTS\_I2C)
	help
		Enable driver for ICM20948.
```
- In the `CMakeLists.txt` file add all `ICM-20948` related source files, e.g.:
```
zephyr\_library()
zephyr\_library\_sources\_ifdef(CONFIG\_ICM20948 deviceIcm20948.c)
```

- In the same `icm20948/` folder add proper source files
- In the folder `../zephyr/dts/bindings/sensor/` create a `tdk,icm20948.yaml` file and fill it with the following code:
```
title: TDK motion tracking sensor
description:
	This is a representation of the TDK motion tracking sensor
compatible: "tdk,icm20948"
include: i2c-device.yaml
```
- In the `../zephyr/drivers/sensor` folder to the file `CmakeLists.txt` add the line:
```
add\_subdirectory\_ifdef(CONFIG\_ICM20948 icm20948)
```
- In the `../zephyr/drivers/sensor/` folder add to the file `Kconfig` the line:
```
source "drivers/sensor/icm20948/Kconfig"
```
All the above-mentioned steps enable **ICM-20948** sensor driver and make it possible to be used like all the other sensors, including Zephyr's sensor API.

Zephyr philosophy considers sensors as part of the hardware. As a result, like all basic hardware, Zephyr wants sensors to be initialized during the preliminary step, in any case at some time point prior to the start of the application's main function. Thus, when the main part of application starts, the sensors are ready for usage (if properly set up and initialize), and the developer only has to obtain the sensor handle by unique sensor's name and use sensors API functions to manipulate sensor's data.

## Conclusion

In this blog, we observed the process of Zephyr application development. Specific case applying the environmental sensors was considered. Probably, at first glance, it is not easy to work with Zephyr. Using SDK and toolchain developed just for certain SoC or MPU is usually more straightforward. Within such approaches, moving to another board presents a need in getting familiar with new SDK and new toolchain. Using Zephyr makes a process of migrating from one board to another smooth and flexible. Anyway, Zephyr is positively worth paying extra attention to it.
