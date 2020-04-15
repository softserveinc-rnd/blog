# Review of Occupancy Detection Methods

The implementation of smart cities, smart buildings, and other smart strategies are impossible without information about humans’ presence and their quantity inside. Such kind of human sensing was named occupancy detection. Occupancy detection requires the presence of variable sensors on the body, some kinds of terminals (Wi-Fi, Bluetooth, so) in the human pocket or ambient sensors (environmental) in the smart environment and sophisticated AI and ML algorithms to analyze the measurements results. The usage of variable sensors and terminals technically is the most natural solution, but it also requires some level of discipline. It is the right approach for organizations with strong regulations or corporate culture but very ineffective in other cases. On the other hand, such a solution automatically identifies users as well, which lowers the level of privacy. So, below different ambient solutions that could be embedded into the environment are described.  

## Video Cameras

Most buildings entrance, territories near it and some critical infrastructure are covered by video cameras and office guards are familiar with such popular devices. Such infrastructure could be widened and used for occupancy detection. 

For example, Analog Devices has developed a low cost, low power embedded computer vision platform, named  Blackfin®, that could be used for occupancy detection. 

https://www.analog.com/en/design-center/landing-pages/002/apm/vision-based-occupancy-sensing-solutions.html# 


| Pros. | Cons. | Use |
| -------- |--------- |-------------- |
| The most popular solution because of <p> *recent enormous progress in image/video processing and computer vision, <p> *as well as lowering of prices on HD cameras.  | | |
| | | |

<table>
	<thead>
		<tr>
			<td>Pros.</td>
			<td>Cons.</td>
			<td>Use</td>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

## IR Cameras (pyrometers)

Usage of IR Cameras instead of RGB ones allows fixing some privacy issues. It is hard to identify people on the IR video stream and use it as compromising materials, even is the video is stolen. 

Sensor construction, recommendations of placement were described in work [18] 

## PIR Sensors

That type of sensors is commonly used for occupancy detection in alarms and light control systems. They are sensitive only to changes of the infrared radiation (human motion, for example). 

## Array of IR sensors

Placing several IR sensors in the room allow us to capture its temperature pattern and detect changes due to the quantity of people's presence and their activity.   In work [3], authors placed IR sensors at the doorways for counting the number of people inside rooms. 

## Break-beam sensors 

If the IR sensor is a passive solution, break beam sensor is an active one. It consists of a pair of devices - a transmitter of the IR beam and its receiver.  If someone passes near the sensor pair, it breaks the IR beam, and the sensor detects that event. 

http://www.sdinternational.nl/downloads/leaflets/People%20Counter%20-%20Display.pdf 

## Ultrasonic sensors 

Ultrasonic sensors use simple radar idea – ultrasonic transmitter generates ultrasonic chirps that are reflected from human bodies. The microphone receives a reflected signal, and after signal analysis, people can be detected and counted. Schematic system design is shown in the picture below, taken from [5], which describes the implementation of one such system.  

| | Maximun capacity | Average error | Error/Max Capacity (%) |
| ------------------------------------------------------------------------------------------ |
| Small room | 8 | 0.61 | 7.6 |
| Medium room | 30 | 1.6 | 5.3 |
| Large room | 150 | 2.6 | 1.7 |

## UWB radars 

UWB radars emit radio waves and analyze the reflected signal. Modern DSP and ML techniques are used for signal analysis. Became very popular because of usage in self-driving cars. 

Novelda develops UWB sensors for human presence detection in indoor applications and smart building systems. As an example could be mentioned X4M300 sensor. See documentation in [6] and demonstration on video [7]. The similar solution also proposes an Italian company ARIA sensing [8] 

## Wi-Fi

Technically, Wi-Fi sensing is the implementation of UWB radar technology. The main advantage is that Wi-Fi infrastructure is already present in modern buildings and offices and could be reused for occupancy detection. 

Moreover, Wi-Fi sensing could be realized in both the terminal and non-terminal way. The RF signal transmitted by the user's Wi-Fi terminal (smartphone or any gadget in pocket) is analyzed in the first option. The second implementation doesn't rely on user terminals but requires the presence of at least two Wi-Fi devices (e.g. a notebook and a Wi-Fi router). One device is used as a signal transmitter, the second – as a receiver. Early Wi-Fi sensing implementations were based on RSSI measurements when the last implementations on CSI and could use AoA and ToF methods on several signal frequencies. Authors of work [9] claim that Wi-Fi is already successfully used for detection, recognition, and estimation tasks, providing examples of usage.

## Microphone

The microphone captures the noise produced by people and their activities in the room, conversations, etc. After signal analysis, it is possible to estimate the number of people in the room. Placing an array of directed microphones also allows tracking the position of a noise source. Speech recognition, speech segregation, and noise detection/classification techniques are useful for solving such a task.  

Project Ubicoustics is the best jaw-dropping example of microphone usage. Additional information available on the project page [11], video presentation can be found here [12]. 

## Capacitance sensors

Modern painting materials can convert the whole wall or even room into a capacitance sensor or electromagnetic noise detector. It allows detecting peoples near the wall. 

Project Wall++ is the best demonstration of possibilities and capacitance of sensors. Additional information in article [12] and video demonstration [13] 

## CO2 sensors 

A person releases a certain amount of carbon dioxide while breathing which allows to use CO2 sensors for occupancy detection. This approach was analyzed in work [14] and it was noticed that CO2 data had to undergo some processing to find the most meaningful way to bring valuable information. In work [15] it was shown that CO2 sensors need some time to predict the number of people in the room correctly, and more sophisticated algorithms (controllers) give better estimation results. The figure below (taken from work [15]) demonstrates measured CO2 concentration in time when a different number of people are present in the room and ventilation flow rate was set to 3 air changes per hour (ACH).   

## Smart meters

Home's pattern of electricity usage generally changes when occupants are present due to their interaction with electrical loads. An example of such an approach is described in [16] 

## Pressure sensors

Covering the floor by pressure sensors is also the right solution for occupancy detection. It is enough to have several sensors near the doors for people counting solutions when people's location solutions require covering all floor by sensors tiles. The usage of sensors pairs allows detecting moving direction as well as in case of break beam pair of sensors.  Descriptions of proposed solutions were found only in works about person identification by walking style.  

## Turnstile counters

Turnstiles are popular solution for people access control for stadiums, amusement parks, mass transit stations, office lobbies, airports, ski resorts, factories, power plants, etc. But they can be also placed near the room entrance or entrance to specific building area and used for people counting.  

## Summary

Overall, there are plenty of approaches that can be used for occupancy detection/people counting. Each of them has its advantages and drawbacks, and  though being useful in certain cases appears to be  ineffective in others. Attribute driven approach may be helpful while choosing the most suitable solution.  Weighting the efforts / resources needed for implementation and the desired results vs the obtained will allow to find the most valuable solution.  

## References

[1] Room occupancy estimation through wifi, UWB, and light sensors mounted on doorways. Mohammadmoradi H., Yin S.,  Gnawali O. Proceedings of the 2017 International Conference on Smart Digital Environment - ICSDE '17. City: New York, New York, USA. Publisher: ACM Press, 2017 pp: 27-34. DOI:  10.1145/3128128.3128133. ISBN: 9781450352819 

[2] https://www.analog.com/en/design-center/landing-pages/002/apm/vision-based-occupancy-sensing-solutions.html 

[3] Measuring People-Flow through Doorways Using Easy-to-Install IR Array Sensors.  Mohammadmoradi H., Munir S., Gnawali O., Shelton C. 2017 13th International Conference on Distributed Computing in Sensor Systems (DCOSS). Publisher: IEEE, 2017 pp: 35-43. DOI: 10.1109/DCOSS.2017.26. ISBN:  978-1-5386-3991-7 

[4] http://www.sdinternational.nl/downloads/leaflets/People%20Counter%20-%20Display.pdf 

[5] Occupancy estimation using ultrasonic chirps.  Shih O., Rowe A. ACM/IEEE 6th International Conference on Cyber-Physical Systems, ICCPS 2015. Publisher: Association for Computing Machinery, Inc., 2015 pp: 149-158. 

[6] X4M300 presence sensor site and desription: https://www.xethru.com/x4m300-presence-sensor.html. 

[7] X4M300 presence sensor video demonstration: https://www.youtube.com/watch?v=UpMULKydVT4&feature=youtu.be 

[8] LT102 UWB radar module information from ARIA sensing http://ariasensing.com/products/lt102-uwb-radar-module/ 

[9]  WiFi Sensing with Channel State Information. Ma Y., Zhou G., Wang S. ACM Computing Surveys, 2019 vol: 52 (3) pp: 1-36. DOI: 10.1145/3310194, ISSN: 03600300 

[10] Project Ubicoustics page   http://www.gierad.com/projects/ubicoustics/ 

[11] Video demonstration of Ubicoustics project https://www.youtube.com/watch?time_continue=211&v=N5ZaBeB07u4 

[12] Zhang Y.,  Yang C.,  Hudson S., Harrison C., Sample A. Wall++: Room-Scale Interactive and Context-Aware Sensing.     Proceedings of the 2018 CHI Conference on Human Factors in Computing Systems - CHI '18. City: New York, New York, USA. Publisher: ACM Press, 2018 pp: 1-15.  DOI:10.1145/3173574.3173847. ISBN: 9781450356206 Free copy of publication  https://yangzhang.dev/research/Wall/Wall.pdf 

[13] Video demonstration of Wall++ project https://www.youtube.com/watch?v=175LB2OiMHs&feature=youtu.be 

[14] A Non-Intrusive Approach for Indoor Occupancy Detection in Smart Environments. Abade B., Perez Abreu D., Curado M. Sensors (Basel, Switzerland), 2018 vol: 18 (11). DOI: 10.3390/s18113953, ISSN:   1424-8220, PMID: 30445696 

[15] CO2 sensors for occupancy estimations: Potential in building automation applications. Gruber M., Trüschel A.,  Dalenbäck J. Energy and Buildings, 2014 vol: 84 pp: 548-556. 

[16]  Non-Intrusive Occupancy Monitoring using Smart Meters.  Chen D., Barker S., Subbaswamy A., Irwin D., Shenoy P. Proceedings of the 5th ACM Workshop on Embedded Systems For Energy-Efficient Buildings - BuildSys'13. City: New York, New York, USA. Publisher: ACM Press, 2013 pp: 1-8. DOI:  10.1145/2528282.2528294. ISBN:9781450324311 

[17] https://en.wikipedia.org/wiki/Turnstile 

[18] Mikkilineni A., Dong J., Kuruganti T., Fugate D.  A novel occupancy detection solution using low-power IR-FPA based wireless occupancy sensor. Energy and Buildings 2019 vol: 192 pp: 63-74 

 



