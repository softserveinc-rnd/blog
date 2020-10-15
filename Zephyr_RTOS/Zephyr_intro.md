
# Zephyr RTOS 
### Introduction

The main question is why – why to develop yet another operating system for embedded devices? Indeed, what it is all for if Wikipedia counts around one hundred of embedded operating systems so that everybody can find one which fits specific application needs in the best way. In this short blog, we will attempt to clarify this issue as well as describe main features which distinguish Zephyr OS from other embedded OS.

IoT industry is rapidly developing. There is a long list of boards used as hardware for IoT devices. Sometimes there are cases when different boards are to be used within a single application, or a quick switch from one board to the other is demanded. Therefore, a need in a unified platform speeding up development under such circumstances is shaping. Creating such a platform was a driving force of Zephyr OS development. As it is stated at Zephyr official site [[Ref]](zephyrproject.org), Zephyr OS is intended to be open, collaborative environment to deliver an open-source RTOS, applicable in a wide diversity of use cases, and supporting as many as possible hardware devices, while giving possibilities for upstreaming code and participating in the future roadmap.

### Short history
Zephyr originated from the Virtuoso DSP operating system. Later, it was acquired by Wind River Systems in 2015 and renamed to Rocket OS, designed especially for resource-constrained embedded systems. In 2016, Rocket OS transformed into the Zephyr project managed by the Linux Foundation as open source. Since that time Zephyr project is sponsored and contributed mainly by Intel, Nordic Semiconductor, Linaro, Synopsys, Google, NXP, Tencent, Acer, Sony, STMicroelectronics, but also by many others.

Well, now when Linux Foundation manages Zephyr, the question arises, what is the need for Zephyr if Linux kernel itself can do the job well? Indeed, Linux is widely used for IoT applications. However, it requires at least a Cortex-A MCU (or equivalent) and is not the preferred choice for more resource-limited systems, such as Cortex-M [[Ref]](https://www.zephyrproject.org/zephyr-an-operating-system-for-iot).

While Linux vs Zephyr choice for resource-constrained systems is quite obvious, what about comparisons against the other embedded OS? As it was already stated earlier, there are many of them but let us consider just the most popular ones.

Probably the most popular embedded OS now is FreeRTOS [[Ref]](https://www.freertos.org/). It got even more support since being acquired by Amazon in 2017. Being just a bare operating system, it intrinsically lacks such things as device drivers, file systems, crypto modules, network stacks, middleware, and a bootloader. Therefore, they must be added from the other sources. It is an essential drawback in some use cases.

The other quite popular embedded OS is ARM’s Mbed OS. A specific feature of Mbed OS is that it is compiled on a remote server using the ARMCC C/C++ compiler. However, being provided by ARM, it does not support the other popular IoT platforms.

Apache Mynewt OS is another OS to mention in this context. Mynewt comes with a full implementation of the BLE stack and supports different boards which range, however, is somewhat limited.

Generally, the choice of an embedded OS heavily depends on the specific use case. Therefore, there is no single recipe or a single OS to be recommended. Discussion of the pros and cons of a different OS’s is out of the scope of this blog and focus is made on Zephyr specifics, and the author’s own experience acquired while working with this system.

### What makes Zephyr OS unique as compared to other OS?

1. **Supported boards**
	At the moment this blog is written several boards supported by Zephyr were around 170, much more than any another embedded OS has. Why is it important? Because it is very convenient. If due to some reasons decision is made to move to another hardware device the one thing to do (at least theoretically) is to inform Zephyr compiler for which board the code has to be compiled. Otherwise, without embedded OS supporting multiple boards, it is just the start of a painful process of getting familiar with board specifics, OS specifics, building toolchain, IDE etc. Thus, Zephyr essentially reduces time and efforts while moving to another board.
	
2. **Scalability**
	Zephyr is a highly configurable and modular OS that implements memory protection (even for platforms without an MMU/MPU). It uses Device Tree Support (DTS) only during compile time. Powerful configuration tool allows flexible inclusion of only those features which are needed in a specific application. Memory footprint can be as low as 8k.
	The other specific feature of Zephyr is that it has only one address space. It means that the application code and the kernel are combined in the same binary compilation. 
	
3. **Build toolchain**
	Being intrinsically cross-platform project, Zephyr naturally uses the CMake build system. It also extensively uses a command-line tool named ***west*** [[Ref]](https://docs.zephyrproject.org/latest/guides/west/index.html). West is used for building, flashing and debugging applications as well as Zephyr repository manager.
	In general, application configuration step is rather complicated in Zephyr. It extensively uses multi-level hierarchical configuration approach. [Here](https://docs.zephyrproject.org/latest/guides/build/index.html) is the link to the configuration build overview from the official Zephyr documentation page. It will be considered in more details in the next blog. For now, it’s worth stating that it includes Device Tree Compilation step resulting in the generation of application-specific header files – user need not writing header file manually.
	
4.  **Communication interfaces and device drivers**
	Zephyr support presently includes Bluetooth, Bluetooth LE 5.0, Ethernet, 802.15.4, Wi-Fi, IPv4/IPv6, 6LoWPAN, Thread, and NFC. 
	
5. **Sensor support**
	Expectedly, Zephyr has great sensors support with a high level of abstraction. The process goes smoothly during enabling sensor which is already supported by Zephyr. List of supported boards and sensors is very rich. However,  if a new sensor is to be enabled on a custom board, the process turns out to be a little complicated. An issue of implementing new sensor support on Zephyr will be addressed in detail in the next blog.
	
6. **Zephyr support and updates.**
	Zephyr OS has a great SDK and is very well documented. It is permanently developing project, and new releases are issued quite frequently. The scope of the project is very wide so that along with rather frequent updates, it is a separate task to track all changes and comments. Moreover, sometimes application development can be stuck for an indefinite. Authors personally experienced this when at some time started observing unexpected device resets. Hours were spent for debugging and naturally, reasons for the problem were first searched in application code. However, after a couple of weeks of debugging, the reason was localized to be in Bluetooth controller side part. Only at that moment decision was made to update Zephyr to the newest version. And voila – resets magically disappeared and the problem was solved.
	
### General conclusion
All in all, Zephyr OS is mighty and convenient instrument for embedded application development and is highly recommended for usage.	
In the next blog, an application development process using Zephyr OS will be described in more detail.
