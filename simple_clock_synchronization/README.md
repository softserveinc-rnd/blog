#Implementation of simple time synchronization algorithm in a mesh network

##Principle
The synchronization is based on broadcasted time stamps. Each node both listens to other transmissions and sends own value of network time. Separate time slots are assigned for those operations.  
If received time stamp is older than own (i.e. the value is bigger), this value is accepted as network time. This way the first node in the network gives the time base. Notice, that it is not necessary for the first node to be constantly operational, because once synchronized, whole network knows and broadcasts this time.

##Hardware
Network nodes in the proof of concept network are built on Particle Xenon boards with a little help of nRF52840 board acting as additional node and a JLink.  

##Software
Implementation is based on a loop with timing segments producing cycles starting from listening phase and subsequenty a series of shorter transmission phases separeted by idle time. Both first and last transmission phases in a cycle that are neighbouring with listening phase are not separeted from it. That is, the system without delay transitions from transmitting to listening to transmitting.
###Time measuring
Time counter is a millisecond counter stored in a 64-bit integer. This ensures sufficient capacity. Time is derived from Zephyr system millisecond timer with additional offset to align it with network time. This offset is modified during time adjustment procedure.
###Timing
Timing is based on following parameters:
+ Period of advertising phase.
+ Length of advertising transmission (within this period).
+ Number of those periods within a cycle.
+ Length of listening phase - based on advertising phase with randomly added small amount of time.
Reason for the randomly added time is such that differentiating cycle lengths between nodes allows to shift the listening phase relatively to advertising phases of other nodes. This in turn secures the node against accidentally falling into constant unlucky time relation with peer that could make information exchange difficult. To avoid identical pseudorandom values in all nodes, the enthropy-based generator is selected instead of simpler time-based one.
###Communication
For communication advertising mechanism of GAP is used. Advertising and scanning time is manually controlled. Time adjustment is done immediately in a callback function upon reception of data packet.  
Currently Zephyr's Bluetooth driver does not allow for more sophisticated communication control. In further implementation it would be profitable to receive the notification when the required number of broadcasts is sent and instantly enter the sleep mode. Similar action would be taken when time synchronization is executed, although this is a more complex situation and needs further consideration.
###User interface
The software uses RTT terminal to communicate in a text form, however this is only available at devices connected to JLink. Visual status information is presented with RGB LED on the board. Colour of indication are following:
+ Black - idle
+ Green - scanning in progress, can change to
+ White - time adjustment was made, remains on till the end of scanning
+ Red - broadcasting in progress  
As a visualisation of the synchronization there is a flash of blue light on second LED of the board. Flashes are made based on network time count and when it is synchronized they all come simultaneously.
