# Approaches to Human Activity Recognition 

The implementation of IoT, smart cities, and smart buildings all require information about human movements, activities, and presence. Recently, varying types of human sensing have become a contemporary approach. One among them is Human Activity Recognition (HAR).  Here, we investigate new methods, based on scientific research, to HAR. 

## Sensor-based taxonomies

As presented by Lara and Labrador, Zhaojie Ju, et al., and others [1], [2] , [6], [16] different taxonomies for Human Activity Recognition, depending on usage of sensor types, are proposed by experts. The most relevant universal taxonomies are proposed in works by Ma Y. et al. and Andreas Bulling et al. [6], [16]. Both types are sensor-based.  

Three groups, called modalities, divide all sensors. The first group is wearable or body-worn sensors. These are worn by humans and capture body movements. Examples of such sensors include accelerometers, gyroscopes, and magnetometers embedded into bands, watches, smartphones, closes, and more body-type devices.  

The second group of modalities consists of the object sensors. These sensors are embedded into different objects, which are related to various human activities. RFID-based [7], accelerometers, integrated into a coffee cup, etc. are examples of such sensors.  

And, the third group are named ambient sensors. Often this group contains different sensors embedded into the humans environment. These types often include microphones [17], ultrasonic and UWB radars [18], Wi-Fi [16], Bluetooth, video [2], infrared and depth cameras [9], capacitance sensors [8],[19], and others, as presented by Bian S. et al. and Chen D et al..   

## The correct sensor for the required activity  

Wearable sensors are useful for the detection of daily living as well as fitness activities. More complex operations that include moving, manipulation, or interaction with particular objects in the environment, are better captured by the object sensors. However, for activities that require collaboration between humans, communication with different devices is better captured by the ambient sensors.   

Portions of wearable sensor research [4] are dedicated to the correct placement of the sensor on the human body. Researchers concluded that placing sensors on the dominant wrist, waist, or the dominant hip pocket receives the best results for the body movement capturing. On the other hand, object and ambient sensors should be integrated into environments in a non-invasive way to collect data naturally and not disturb humans. During the preprocessing, sensor signals are usually cut to form sliding windows. Moreover, the signals from different sensors, different sensor types, or even different sensor axes, are treated as separate channels. This approach could enhance the next signal classification step.    


## Sensor data processing 

The typical sensor processing flow contains data acquisition, signal processing and segmentation, feature extraction and selection, training and classification steps [5]. A detailed description of features used for activity classification, as well as classification algorithms, was made in this report [6]. All the signal features are divided into time-domain (mean, standard deviation, variance, interquartile range (IQR), mean absolute deviation (MAD), the correlation between axes, entropy, and kurtosis), frequency domain (Fourier Transform (FT) and Discrete Cosine Transform (DCT)). Additionally, the Principal Component Analysis (PCA), Linear Discriminant Analysis (LDA), Autoregressive Model (AR), and HAAR filters are used for feature selection and construction.   

Accuracy of different training and classification algorithms with existing working systems were evaluated by researchers [4], [6]. These vary from 70% to almost 98%. Researchers also noticed [5] that person-dependent algorithms provide better results than person-independent methods, just as the usage of accelerators is better than the usage of gyroscopes. 

## Deep learning techniques for recognition improvement 

The usage of machine learning (ML) and deep learning techniques is impossible without the existence of datasets dedicated to human action and activity recognition. Many of these examples are described here [3]. 

 Other publications, including those by Cook D et al., Yang J., et al., Ronao and Cho, Hammerla N. et al., Ordóñez F. and Roggen D., and Wang J. et al. [10] - [15] are dedicated to using different deep learning techniques directed to the improvement of the activity recognition. Survey [15] and work [14] contain recommendations for using RNN and LSTM architectures for short-term and CNN for long-term repetitive activities' recognition.  In those works, it was also recorded that CNN has possibilities to fuse sensor channels naturally. Applying CNN, it is possible to increase F1 scores by 15% fusing accelerometers and gyroscopes. An increase of 20% is seen when fusing accelerometers, gyroscopes, and magnetic sensors. These results demonstrate that the convolutional layers can extract features from sensor signals of different modalities without ad hoc preprocessing 

## In conclusion 

SoftServe experts recommend using wearable sensors for the activities which are related to human moving. Object sensors should be used when capturing human interaction with specific objects is needed. Ambient sensors are sufficient to capture both kinds of activities but may suffer from shadowing and blindness.  The use of ambient sensors for recognition activities in closed smart environments, as well as sensor fusion approaches to compensate for their technical debts, is the most advanced solution and proposal. Moreover, a modern approach to sensor fusion involves using convolutional neural networks to complete the tasks automatically during networks training. To learn more, contact SoftServe today. 

 ## References

[1] Vrigkas M., Nikou C., Kakadiaris I. A review of human activity recognition methods. Frontiers Robotics AI. Publisher: Frontiers Media S.A., 2015 vol: 2 (NOV) 

[2] Ke S., Thuc H., Lee Y., Hwang J., Yoo J., Choi K. A review on video-based human activity recognition. Computers. Publisher: MDPI AG, 2013 vol: 2 (2) pp: 88-131 

[3] Chaquet J. Carmona E. Fernández-Caballero A. A survey of video datasets for human action and activity recognition. Computer Vision and Image Understanding, 2013 vol: 117 (6) pp: 633-659 

[4] Attal F., Mohammed S., Dedabrishvili M., Chamroukhi F., Oukhellou L., Amirat Y. Physical human activity recognition using wearable sensors. Sensors (Switzerland). Publisher: MDPI AG, 2015 vol: 15 (12) pp: 31314-31338 

[5] Bulling A., Blanke U., Schiele B. A tutorial on human activity recognition using body-worn inertial sensors. ACM Computing Surveys, 2014 vol: 46 (3). 

[6] Lara Ó., Labrador M. A survey on human activity recognition using wearable sensors. IEEE Communications Surveys and Tutorials, 2013. 

[7] Luo X., Yang Q., Li P., Miyazaki T., Wang X. Grouping Strategy for RFID-based Activity Recognition in Smart Home. DOI: 10.1109/iThings/GreenCom/CPSCom/SmartData.2019.00038 

[8] Bian S., Rey V., Hevesi P., Lukowicz P. Passive capacitive based approach for full body gym workout recognition and counting. 2019 IEEE International Conference on Pervasive Computing and Communications, PerCom 2019. Publisher: Institute of Electrical and Electronics Engineers Inc.,2019 

[9] Aggarwal J., Xia L. Human activity recognition from 3D data: A review Pattern Recognition Letters. Publisher: Elsevier, 2014 vol: 48 pp: 70-80 

[10] Cook D., Feuz K., Krishnan N. Transfer learning for activity recognition: A survey. Knowledge and Information Systems. 2013 vol: 36 (3) pp: 537-556  

[11] Yang J., Nguyen M., San P., Li X., Krishnaswamy S. Deep convolutional neural networks on multichannel time series for human activity recognition. IJCAI International Joint Conference on Artificial Intelligence. Publisher: International Joint Conferences on Artificial Intelligence, 2015 vol: 2015-January pp: 3995-4001.  

[12]Ronao C., Cho S. Human activity recognition with smartphone sensors using deep learning neural networks. Expert Systems with Applications, 2016 vol: 59 pp: 235-244 

[13] Hammerla N., Halloran S., Plötz T. Deep, convolutional, and recurrent models for human activity recognition using wearables. IJCAI International Joint Conference on Artificial Intelligence. Publisher: International Joint Conferences on Artificial Intelligence, 2016 vol: 2016-January pp: 1533-1540 

[14] Ordóñez F., Roggen D. Deep convolutional and LSTM recurrent neural networks for multimodal wearable activity recognition. Sensors (Switzerland), 2016 vol: 16 (1) 

[15] Wang J., Chen Y., Hao S., Peng X., Hu L. Deep learning for sensor-based activity recognition: A survey. Pattern Recognition Letters, 2019 vol: 119 pp: 3-11. 

[16] WiFi Sensing with Channel State Information. Ma Y., Zhou G., Wang S. ACM Computing Surveys, 2019 vol: 52 (3) pp: 1-36. DOI: 10.1145/3310194, ISSN: 03600300 

[17] Ubicoustics project page http://www.gierad.com/projects/ubicoustics/ 

[18] UWB radar sensor site: https://www.xethru.com/x4m300-presence-sensor.html 

[19] Non-Intrusive Occupancy Monitoring using Smart Meters.  Chen D., Barker S., Subbaswamy A., Irwin D., Shenoy P. Proceedings of the 5th ACM Workshop on Embedded Systems For Energy-Efficient Buildings - BuildSys'13. City: New York, New York, USA. Publisher: ACM Press, 2013 pp: 1-8. DOI:  10.1145/2528282.2528294. ISBN:9781450324311 



