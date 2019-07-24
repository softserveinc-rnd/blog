# Wireless Communication Between Devices 

## Executive summary

The radio waves are traditionally used to organize wireless communications  between the devices. However, last researches are concentrated on the wireless  optical, acoustic and ultrasonic communications, especially for the vehicle-to-vehicle communication on the roads and for the underwater communications.

A new kind of communication is proposed for the nontechnology applications – chemical communication.  

## Electromagnetic waves 

All wireless communication between the devices now is done by changing one or 
several parameters of the waves (magnitude, frequency of phase). Waves are 
divided on electromagnetic, mechanical and gravitational. First two kinds of waves 
are well studied and used for communication. The last kind of waves was predicted 
in Einstein's works. The first observation was made in 2016 and it still does not have
the practical usage.

### Radio communication 

Radio waves propagate well through air and space, can avoid obstacles due to 
diffraction phenomena. Waves with bigger length (or lower frequency) can avoid 
more significant obstacles. But waves with bigger length require bigger equipment 
and more energy for generation  

The ISM (Industrial, Scientific, and Medical) radio band is usually used for 
communication between devices because it does not require licensing. Initially, ISM 
band was used for non-communication purposes. Now it is widely used for the short-
range device to device communication. Band frequency details are provided in the 
table below.


<table>
    <thead>
        <tr>
            <th colspan=2>Frequency range</th>
            <th>Notes</th>
    	</tr>
    </thead>
    <tbody>
    	<tr>
    		<td>6.765 MHz </td>
    		<td>6.795 MHz </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>13.553 MHz </td>
    		<td>13.567 MHz </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>26.957 MHz </td>
    		<td>27.283 MHz  </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>40.66 MHz  </td>
    		<td>40.7MHz </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>433.05 MHz </td>
    		<td>434.79 MHz  </td>
    		<td>Used only in Europe   (Region 1) Used only in Europe   (Region 1)  </td>
    	</tr>
    	<tr>
    		<td>902 MHz  </td>
    		<td>928 MHz  </td>
    		<td>Used only In America (Region 2)  </td>
    	</tr>
    	<tr>
    		<td>6.765 MHz </td>
    		<td>6.795 MHz </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>2.4 GHz </td>
    		<td>2.5 GHz  </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>5.725 GHz </td>
    		<td>5.875 GHz </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>24 GHz </td>
    		<td>24.25 GHz</td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>61 GHz </td>
    		<td>61.5 GHz  </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>122 GHz </td>
    		<td>123 GHz  </td>
    		<td> </td>
    	</tr>
    	<tr>
    		<td>244 GHz </td>
    		<td>246 GHz  </td>
    		<td> </td>
    	</tr>
    </tbody>
</table>

The most popular standards for different kinds of network communication are shown in the figure below (taken from [3]). Protocol details are described in [1], [2], [3]. 

![Figure 1. Standards for wireless radio communication](img/wireless-tecnologies-range.png)

### Wireless Optical Communication

#### Infrared communication 

Infrared communication has several advantages over the radio communication.  Firstly,  it is security – infrared waves are not propagated through walls that makes it perfect for the indoor communication within a single room. Secondly, it is safety – infrared waves are not harmful to human. Thirdly,  – infrared receivers and transmitters are cheap now and allow to transmit data with 1Gbps rate.

This kind of communication also has several disadvantages. It is not suitable for the outdoor communication. Typical room additionally contains several sources of the infrared noise that complicates the communications.  

Possible variants of infrared communication organization are shown below (taken from [4]).   

![Figure 2. Variants of infrared commnunication](img/infrared-connunication-wariants.png)

#### Lazer communication and free space optical communications 

Lazer is suitable for communication between the Earth and the space satellites. Experiments in free space show that it can transfer data on several thousand kilometers and have the potential to bridge interplanetary distances of millions of kilometers, using the optical telescopes as beam expanders.

On the Earth, lazers are used for inter-building communications. Some kinds of lasers are also suitable for the underwater communications and measurements. Details are in [6],[7].

#### Visible light communication 

IIntensive development of visible light communication (VLC) systems started with the extensive commercial usage of the light-emitting diodes (LED). This technology allows creating of the full range of communication solutions: Ultra Short Range Communication, Short Range Communication, Medium Range Communication, as well as Long Range Communications   

Ultra Short Range VLC is used mainly for intra-  and inter - chip communications.

The most interesting application of the Short Range VLC solutions is the creation of a wireless body area network (WBAN). The main trigger here is the progress in Organic LED (OLED) technology that allow embedding of optical transceivers directly into the closing. Another application area – the interconnection of the devices around the workspace. The integrated phone camera (imaging sensor) is used as an optical detector to enable various M2M applications, including phone-to-phone, phone-to-TV, and phone-to-vending machine communication in the last researches. 

Medium Range VLC is used for LAN organization. LiFi will replace WiFi networks. In addition to the indoor deployment, LEDs are being widely used in the outdoor lighting, traffic signs, advertising displays, car headlights/taillights, etc. This allows for vehicle-to-vehicle communication and vehicle-to-infrastructure communication [8] as well as signaling and broadcasting safety-related information to vehicles on the road.     

On the other hand, the water is relatively transparent to light in the visible band of the spectrum (absorption takes its minimum value in the blue/green spectral range).This fact  paves the way for the underwater VLC which can achieve data speeds of hundreds of Mbps for the short ranges [9]

Long Range VLC is used for the high rate communication between the two fixed points over distances up to several kilometers. It is an efficient solution to bridge the gap between the end-user and the fiber optic infrastructure already in place, WLAN-to-WLAN connectivity in enterprise and campus environments, broadband access to remote or underserved areas, and wireless video surveillance/ monitoring. They are also useful as redundant links in the cases of disasters because they are easy-to-install and re-deployable. Further details are in [11]. 

##Mechanical waves 

### Acoustic communication 

Acoustic waves are used for the underwater communication [10], and cover the distance ranges up to several kilometers. However, this technology has minimal bandwidth available, low celerity, and large latencies. Data rates are limited to a few hundreds or thousands of kbps. 

Some researchers use acoustic waves for communication between the devices and smartphones, using smartphone microphone as a receiver [12].

### Ultrasonic communication 

Ultrasonic waves are traditionally used to measure the distance and thickness. But researches are building communications systems, based on their usage [13], [14]. The usage of new graphene diaphragms for transmitting/receiving ultrasonic signalscould stimulate the further progress in that field  [15]. 

Please also note, that people didn’t hear ultrasonic waves. But the high-intensity ultrasound could be destructive for human and even used as a weapon, sometimes lethal.

## Other methods 

### Molecular communication 

When devices are scaled down to the nanoscale level, the new communication means are needed for them. Researches are inspired by the observation of the biological systems, in which communication is typically done through the molecules.Feasibility studies show that such kind of communication has low energy consumption, low communication speed, and causes chemical reactions on the receiver’s side. The character of communications is stochastic. More details are in [16].

## References 

1. Sensor technologies: healthcare, wellness, and environmental applications. McGrath M., Scanaill C.. Publisher: ApressOpen, 2014. 

2. Embedded systems for smart appliances and energy management. Grimm C., Neumann P., Mahlknecht S. Publisher: Springer, 2013 pp: 148. 

3. A Study of Efficient Power Consumption Wireless Communication Techniques/ Modules for Internet of Things (IoT) Applications. Mahmoud M., Mohamad A., Mahmoud M., Mohamad A. Advances in Internet of Things, 2016 vol: 06 (02) pp: 19-29 

4. Wireless infrared communications. Kahn J., Barry J. Proceedings of the IEEE, 1997 vol: 85 (2) pp: 265-298. 

5. Infrared Communication - Introduction of IR and It's Functionality. Date Accessed: 2019-07-17. URLS: www.elprocus.com/communication-using-infrared-technology/ 

6. Optical wireless communications - An emerging technology. Uysal M., Nouri H. International Conference on Transparent Optical Networks. Publisher: IEEE Computer Society, 2014.

7. A review of operational laser communication systems. Goodwin F. Proceedings of the IEEE, 1970.  vol: 58 (10) pp: 1746-1752  

8. Performance analysis of a car-to-car visible light communication system. Luo P., Ghassemlooy Z., Minh H., Bentley E., Burton A., Tang X. Applied Optics, 2015 vol: 54 (7) pp: 1696 – 1706. 

9. Underwater optical wireless communication network. Arnon S. Optical Engineering, 2010 vol: 49 (1) pp: 015001 

10. Wiley encyclopedia of telecommunications. Proakis J. Publisher: John Wiley & Sons, 2003 

11. Survey on free space optical communication: A communication theory perspective. Khalighi M., Uysal M., IEEE Communications Surveys and Tutorials, 2014 vol: 16 (4) pp: 2231-2258 

12. Audio Networking: The Forgotten Wireless Technology. Madhavapeddy A., Scott D., Tse A., Sharp R. IEEE Pervasive Computing, 2005 vol: 4 (3) pp: 55-60 

13. Wireless Communication Using Ultrasound in Air with Parallel OOK Channels. Wright W., Wentao Jiang. Publisher: Institution of Engineering and Technology (IET), 2013 pp: 25-25

14. Ultrasonic Signals Are the Wild West of Wireless Tech. WIRED. Date Accessed: 2019-07-18. URLS www.wired.com/story/ultrasonic-signals-wild-west-of-wireless-tech/ 

15. Graphene electrostatic microphone and ultrasonic radio. Zhou Q., Zheng J., Onishi S., Crommie M., Zettl A. Proceedings of the National Academy of Sciences, 2015 vol: 112 (29) pp: 8942-8946 

16. Molecular Communication-IEEE Recommended Practice for Nanoscale and Molecular Communication Framework View project signal processing View project Molecular Communication. Suda T., Moore M., Nakano T., Hiyama S., Moritani Y., Suda T., Egashira R., Enomoto A., Moore M., Nakano T. 2008. 
