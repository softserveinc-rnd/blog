# Non-Contact Heart Rate Measurement Methods

## Executive summary

Heart rate is a very informative characteristic of the human body. It could be used to monitor human health, training process, emotions, lie detection e.t.c.as well as for person identification. Classical methods of heart rate measurement require the usage of the electrocardiograph and mounting at least 3 contact electrodes. Smartwatches and wristbands are not so vast and annoying for user devices and use photoplethysmography to measure heart rate. However, in that case, the user also should wear measuring device and knowledge of that could change the results of measurements. From another point of view what can be done if we can’t put measuring device on the user? In the current article, we analyzed dozens of non-contact heart rate measurement approaches and found that the most popular and useful during the last years were radio waves radars and optical methods. Details are provided below.  


## Usage of IMU for Heart Rate Measurement 

Instead of measuring electrical or optical signals, a 9-axis Inertial Measurement Unit (IMU) was used to detect the mechanical vibration of the chest caused by the heart movement. The acquired signal is called the ballistocardiogram (BCG). BCG waveform is more observable in the output of the gyroscope than the output of the accelerometer. An algorithm was developed to estimate the heart rate from the gyroscope-acquired BCG [1], [2].  


## Non-Contact Capacitive Based Electrodes 

Heart rate signal is acquired through the capacitive non-contact active electrodes. The electrodes are placed on the user’s chest, over a vest. Signals are captured and conditioned by an analog frontend where ECG and respiration rate (RR) is separated by utilizing a differential separation filter. The system uses Bluetooth v4.0 or Bluetooth low energy (BLE) for wireless communication between the wearable device and the remote server [3]. 

## Usage of Radio Waves for Heart Rate Measurement 

Both radar echo and Doppler effect are usually used to compute the heart rate.  There is a difference depending on the part of the body reflecting the radio waves, used frequency range, and type of radar system. Echo from the chest as well as from other parts of the body - head for example [7] is measured [8]. Some methods use ultra-high frequencies (about 79 GHz) [7] as well as sub gigahertz band (915 MHz) [11]. Widely used radar systems for such applications are a continuous wave (CW), ultra-wideband (UWB), frequency modulated continuous wave (FMCW) and stepped frequency continuous wave (SFCW) systems [5-11].  

Netmit laboratory at MIT uses a radio transmitter that generates FMCW signal that sweeps from 5.46 GHz to 7.25 GHz every 2.5 milliseconds, transmitting sub-mW power for breath and heart rate measurement [4].  

Novell approaches use near field coherent sensing (NCS), built on coherent RFID (radio frequency identification) architecture. It allows measuring the heart rate of small conscious animals, which even have a different heart structure [12]. 

## Ultrasonic Measurements

Chest displacement due to breath and heartbeats are measured using ultrasonic waves. A method is close to the described above measurements with the usage of radio waves. The main difference lies in the used wave frequencies, and the phase distance measuring method used [13].     

## Optical methods 

All the optical methods of heart rate measurements are based on the fact that the skin color changes due to blood circulation. Measurements can be done in the visible [14] or infrared spectrum range [15]. When a visible light range is used, the method is sensitive to external illumination and its pulsations caused by the usage of AC, gas-discharge and LED lamps. Also, both approaches are sensitive to body motions. 

Also, during the recent years the laser beams have been used to measure the chest displacements applying the same principles as in radio wave and ultrasonic radars [16]. Pentagon even claims that they used such methodology for distant people identification [17].    

## References 

1. Estimation of heart rate from a chest-worn inertial measurement unit. Jia W., Li Y., Bai Y., Mao Z., Sun M., Zhao Q. 4th International Symposium on Bioelectronics and Bioinformatics, ISBB 2015. Publisher: Institute of Electrical and Electronics Engineers Inc. 2015 pp: 148-151 

2. Combining actigraph link and petpace collar data to measure activity, proximity, and physiological responses in freely moving dogs in a natural environment. Ortmeyer H.,Robey L., McDonald T., Animals. 2018 vol: 8 (12) 

3. Wireless capacitive-based ECG sensing for feature extraction and mobile health monitoring. Wannenburg J., Malekian R., Hancke G., IEEE Sensors Journal, 2018 vol: 18 (14) pp: 6023-6032 

4. Smart Homes that Monitor Breathing and Heart Rate. Adib F., Mao H., Kabelac Z., Katabi D., Miller R. Proceedings of the 33rd Annual ACM Conference on Human Factors in Computing Systems - CHI '15. City: New York, New York, USA. Publisher: ACM Press. 2015 pp: 837-846 

5. Novel methods for noncontact heart rate measurement: A feasibility study. Kranjec J., Begus S., Drnovsek J., Gersak G. IEEE Transactions on Instrumentation and Measurement. 2014 vol: 63 (4) pp: 838-847 

6. Detection of Breathing and Heart Rates in UWB Radar Sensor Data Using FVPIEF-Based Two-Layer EEMD. Shyu K., Chiu L., Lee P., Tung T., Yang S. IEEE Sensors Journal. 2019 vol: 19 (2) pp: 774-784 

7. Measurement of instantaneous heart rate using radar echoes from the human head. Sakamoto T., Muragaki M., Tamura K., Okumura S., Sato T., Mizutani K., Inoue K., Fukuda T., Sakai H. Electronics Letters. 2018 vol: 54 (14) pp: 864-866 

8. A Stochastic Gradient Approach for Robust Heartbeat Detection with Doppler Radar Using Time-Window-Variation Technique. Ye C., Toyoda K., Ohtsuki T. IEEE Transactions on Biomedical Engineering. 2018 

9. Research on Non-Contact Monitoring System for Human Physiological Signal and Body Movement. Liang Q., Xu L., Bao N., Qi L., Shi J., Yang Y., Yao Y. Biosensors. 2019 vol: 9 (2) pp: 58. 

10. An Electromagnetic Model of Human Vital Signs Detection and Its Experimental Validation. Nahar S., Phan T., Quaiyum F., Ren L., Fathy A., Kilic O. IEEE Journal on Emerging and Selected Topics in Circuits and Systems. 2018 vol: 8 (2) pp: 338-349. 

11. 915-MHz Continuous-Wave Doppler Radar Sensor for Detection of Vital Signs. Park J., Jeong Y., Lee G., Oh J., Yang J. Electronics. 2019 vol: 8 (5) pp: 561 

12. No-touch measurements of vital signs in small conscious animals. Hui X., Kan E. Science Advances. 2019 vol: 5 (2) pp: eaau0169 

13. A method for the non-contact measurement of two-dimensional displacement of chest surface by breathing and heartbeat using an airborne ultrasound. Hayashi T., Hirata S., Hachiya H., Japanese Journal of Applied Physics. 2019 vol: 58 (SG) pp: SGGB10 

14. Real Time Heart Rate Monitoring from Facial RGB Color Video Using Webcam Embedded Sensor. Rahman H., Ahmed M., Begum S., Funk P. The 29th Annual Workshop of the Swedish Artificial Intelligence Society (SAIS 2016), At Malmö 

15. Non-contact photoplethysmogram and instantaneous heart rate estimation from infrared face video. Martinez N., Bertran M., Sapiro G., Wu H., 2019 

16. Non-contact monitoring of heart beat using optical laser diode vibrocardiography. Capelli G., Bollati C., Giuliani G. 2011 International Workshop on Biophotonics, BIOPHOTONICS 2011. 

17. MIT Technology Review. The Pentagon has a laser that can identify people from a distance—by their heartbeat. [URL](  https://www.technologyreview.com/s/613891/the-pentagon-has-a-laser-that-can-identify-people-from-a-distanceby-their-heartbeat/ )
