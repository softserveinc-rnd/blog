# Calibration different camera systems (in progress)

## Executive summary
Camera calibration is one of the primary steps in capturing photos needed for various computer vision problems, such as 3D reconstruction or object detection. In the process of camera calibration we obtain parameters required for correct image reconstruction. Usually cameras come with parameters predefined by manufacturer. However, environment conditions such as humidity highly influence camera lens, which introduces distortions to images. The goal of camera calibration is to solve such issues.
Calibrating the camera means obtaining internal camera-specific parameters (intrinsics) and relations of this camera to other cameras (extrinsics). Intrinsics include lens focal length and optical centers. 

 Calibration pipeline consists of two major steps: 
1. Collecting photos of reference grids with some pattern (commonly chessboard) from more than 5 different perspectives
2. Applying algorithm, which obtains camera parameters

In our experiments we use [ZED stereo camera](https://www.stereolabs.com/zed/) .  We run our experiments for different patterns and calibration algorithms and compare our results  with default camera parameters on metrics namely absolute and relative errors, re-projection error.
## Single camera calibration
### 1. Image collection
#### Setup 1
 Our initial setup is as follows: 1) we fix printed 7x10 chessboard on the table and make it as smooth as possible 2) Under the vertical light we collect at least 15 photos from different views by moving the camera. We make photos in the way that chessboard takes more than 90% of the picture.
 ![ ](https://res.cloudinary.com/duewxx1op/image/upload/c_scale,w_300/v1583322194/chessboard_table_tyzufl.png  "Setup 1") 

#### Setup 2
In this setup instead of putting chessboard on a table we display it on the computer screen. Other conditions remain the same as in Experiment 1.

### 2. Calibration algorithm
For every image we find chessboard and its internal corners on the image (we use `cv2.findChessboardCorners()` for corner detection and `cv2.cornerSubPix()` to optimize results of previous function ). Then for obtaining camera parameters we apply algorithm from OpenCV library implemented in `cv2.calibrateCamera()` function. 

We observed that board and corner detection algorithms are highly sensitive to illumination level and shades. Therefore one should carefully select position of the camera to minimize unpleasant effects.

### 3. Results
For comparison we use mean re-projection error, which is a common metric for camera calibration. Re-projection errors provide a qualitative measure of accuracy. A re-projection error is the distance between a pattern keypoint detected in a calibration image, and a corresponding world point projected into the same image. Errors for every image are averaged to get final result. Usually RMSE distance is applied. However in our experiments we use L2 distance, because we get relatively small values.

We compare results obtained in both setups with parameters 1) predefined by ZED and 2) inferred with ZED calibration tool. Comparison results we show in Table . We observed that OpenCV calibration algorithm in both setups worked significantly better than ZED calibration tool. Note that ZED calibration was performed in the environment conditions (amount of light) not appropriate enough. However our setups share the same conditions. OpenCV calibration algorithm performed slightly better on Setup 2, which may be caused by several reasons. Firstly, chessboard on the screen is perfectly flat. Secondly, illumination of the board on screen is better. 

| Methods | Mean re-projection error (px)|
| ------------- |-------------|
| Setup 1      | 0.0598 |
| Setup 2      | 0.0379 |
| Factory      | 2.4097 |
| ZED calibrated      | 2.4636 |

Table . Comparison of calibration results

In Tables *-* we see how factory parameters and parameters inferred with ZED calibration differ from parameters obtained with OpenCV algorithm in both our Setups. As mean re-projection error is only slightly different in both factory-related methods errors in distortion intrinsics parameters are very similar.

| Intrinsics | Factory  |ZED calibrated  |
| ------------- |-------------| ---------|
| fx      | 1.0746 | 0.9799 |
| fy     | 0.9388      |   0.8440 |
| cx |  2.3688    |   2.6880 |
cy | 3.3163     |    2.5091 |

Table 1. Relative errors of obtained with Setup 1 intrinsic parameters  (in percents).

| Distortion parameters | Factory  |ZED calibrated  |
| ------------- |-------------| ---------|
| k1     | 0.1869 | 0.1841 |
| k2     | 0.0338  |   0.0333 |
|p1 | 0.0009     |   - |
|p2 | 0.0010     |    - |
|k3 | 0.0129    |   - |

Table 2. Absolute errors of distortion parameters obtained with Setup 1  (in **milimeters**).


| Intrinsics | Factory  |ZED calibrated  |
| ------------- |-------------| ---------|
| fx      | 1.2570 | 1.1624 |
| fy     | 1.2305      |   1.1360 |
| cx |  2.1288    |   2.4488 |
|cy | 2.1984     |    1.4000 |

Table 3. Relative errors of obtained with Setup 2 intrinsic parameters  (in percents)

| Distortion parameters | Factory  |ZED calibrated  |
| ------------- |-------------| ---------|
| k1     | 0.1868 | 0.1841 |
| k2     | 0.0696  |   0.0692 |
|p1 | 0.0006     |   - |
|p2 | 0.0010     |    - |
|k3 | 0.0314    |   - |

Table 4. Absolute errors of distortion parameters obtained with Setup 2  (in **milimeters**).

## Stereo camera calibration

## Calibration camera-projector system
Before calibrating the system of camera and projector, camera should be calibrated to find corresponding intrinsics and distorion parameters. Then in the process of calibrating the system we find extrinsic parameters between camera and projector.
Calibration of projector depends on photos of specific patterns as well. Usually they are vertical or horizontal black and white lines of different width.

### 1. Image collection
Our setup is as follows. Reference grid (same as in single camera calibration) is fixed horizontally on the wall.  In front of it we place a projector on the distance such that pattern we project is not smaller than  reference grid.  We captured photos of patterns projected onto chessboard from different perspectives and angles similarly to single camera calibration. However, it is worth to mention that camera and projector were nearly in the same position with respect to each other. Such conditions are required to guarantee correct work of the algorithm.  

We had 44 pattens in total, including white and black patterns. We selected 5 different perspectives: frontal, left and right turns.  Every pattern was captured from every perspective resulting in 220 photos in total. While capturing photos we minimize amount of light as much as possible. Experiments were conducted under small amount of natural light.
![](https://res.cloudinary.com/duewxx1op/image/upload/c_scale,w_300/v1583411412/chessboard_wall_pygfat.jpg)  ![](https://res.cloudinary.com/duewxx1op/image/upload/c_scale,w_300/v1583411268/chessboard_wall_projector_rhgox5.jpg) 

Other from black and white patterns are vertical or horizontal parallel consecutive black and white lines of different step shown on the figures above. They are required for projector calibration. White pattern is used for camera calibration.



We observed that under specific angles white lines from the pattern become too bright, such that chessboard behind is not visible on the image. Black lines from pattern are not as dark as expected on the image. It is caused by high amount of light produced by projector. In order to get better samples projector should be the only source of light.

### 2. Calibration algorithm

There several ways to calibrate projector-camera system. Particularly they differ in the preprocessing steps, such as calibration of camera and projector beforehand. In our experiments do calibrate camera and projector before calibrating the system, because this approach is more reliable. 

Therefore, the calibration algorithm includes 3 major steps

1. Calibrate camera

2. Calibrate projector

3. Calibrate projector-camera stereo system

   Step 1 is identical to calibration of single camera described in corresponding section. The intermediate step here is identifying chessboard internal corners (denote them as 'camera corners'). We use them for projector calibration.
   
   Step 2 involves identifying intrinsics, extrinsics and distortion parameters of a projector. Firstly we find the projection of camera corners onto projector patterns. To this end we calculate perspective transformation matrix using `cv2.findHomography()` . Finally obtained projector points are employed to perform projector calibration using the same algorithm as in step 1 implemented in `cv2.calibrateCamera()` function.
   
   In Step 3 we exploit results obtained on the previous steps, including camera corners and projector corners (i.e. chessboard corners on camera and projector image planes), both camera and projector intrinsics and distortion parameters, to calculate refined values of camera and projector intrinsics and distortion parameters as well as rotation and translation matrices between camera and projector coordinate systems. For that we use algorithm from OpenCV implemented in function `cv2.stereoCalibrate()`.  

### 3. Results

Here we present obtained intrinsic and extrinsics of camera-projector system.

| c1          | c2           | c3           |
| ----------- | ------------ | ------------ |
| 708.8245877 | 0.           | 633.82181154 |
| 0.          | 705.17722107 | 355.51967291 |
| 0.          | 0.           | 1.           |

Table 5. Camera intrinsic parameters after Step 3. (They are the same as obtained after Step 1)

| k1         | k2         | p1         | p2         | k3          |
| ---------- | ---------- | ---------- | ---------- | ----------- |
| 0.00517938 | 0.00041854 | 0.00047684 | 0.00182914 | -0.00104936 |

Table 6. Camera distortion parameters. (They are the same as obtained after Step 1)

| c1         | c2         | c3         |
| ---------- | ---------- | ---------- |
| 1382.54655 | 0.         | 636.816247 |
| 0.         | 1370.00275 | 762.426041 |
| 0.         | 0.         | 1.         |

Table 7. Projector intrinsic parameters after Step 3. (They are the same as obtained after Step 2)

| k1         | k2          | p1          | p2          | k3         |
| ---------- | ----------- | ----------- | ----------- | ---------- |
| 0.06433447 | -0.20983653 | -0.00779688 | -0.00899345 | 0.15728477 |

Table 8. Projector distortion parameters. (They are the same as obtained after Step 2)

| c1          | c2          | c3          |
| ----------- | ----------- | ----------- |
| 0.65894499  | -0.09471413 | 0.74620422  |
| 0.18255207  | 0.9825186   | -0.03649588 |
| -0.72970284 | 0.1602699   | 0.66471597  |

Table 9. Rotation matrix between camera and projector coordinate systems

| x             | y             | z            |
| ------------- | ------------- | ------------ |
| -228.91907704 | -104.94093294 | 177.05111065 |

Table 10. Translation vector between camera and projector coordinate systems (in mm.)



We evaluate obtained results with re-projection error similarly to the single camera case.

| Camera             | Projector         | Camera-projector system |
| ------------------ | ----------------- | ----------------------- |
| 0.4994452210654006 | 2.142720972714114 | 28.631267298289853      |

Table 11. Re-projection error (in pixels)



Calibration of camera and projector separately show good results. We acknowledge high error in calibrating camera-projector system. It may be caused by several reasons mostly present on the stage of image collection. First of all, camera and projector could not be tightly fixed, small deviations in their relative location were present. Secondly, complete darkness was not reached, small illumination was present. Finally, there could be not enough images from different perspectives, perspectives were changed only in *xy* plane. These are the subjects of an ongoing work.

## Conclusions

We experimentally showed that our camera calibration pipeline provides better results compared to the manufacturer (ZED) approaches. First of all, it allows for obtaining more accurate camera parameters than those, which are predefined by the manufacturer. Secondly, the calibration algorithm from OpenCV library performs better than provided by ZED.

The image collection process is a crucial part of the whole calibration pipeline. Illumination, the number of collected images, the stability of the system are the major properties that influence the result of the calibration. Calibration of a single camera has lower requirements for this stage (we obtained satisfactory results with relatively small efforts). In comparison, calibration of the camera-projector system has more constraints to the setup (i.e. illumination level, tight fixation of the system) and requires to stay stick to them. Standard algorithms for calibration, implemented in OpenCV library, satisfy most cases.

Improving re-projection error in camera-projector calibration is the subject for future work. 

## References 

- https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_calib3d/py_calibration/py_calibration.html

- https://github.com/kamino410/procam-calibration

- https://www.stereolabs.com/developers/release/

- http://www.dmi.unict.it/~furnari/teaching/CV1617/lab1/

- https://bingyaohuang.github.io/Calibrate-Kinect-and-projector/

- https://www.morethantechnical.com/2017/11/17/projector-camera-calibration-the-easy-way/

- https://www.researchgate.net/publication/258807987_Projector_calibration_with_error_surface_compensation_method_in_the_structured_light_three-dimensional_measurement_system

- https://www.spiedigitallibrary.org/journals/optical-engineering/volume-56/issue-07/074101/Method-for-calibration-accuracy-improvement-of-projector-camera-based-structured/10.1117/1.OE.56.7.074101.full?SSO=1

- [https://docs.opencv.org/2.4/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.html#](https://docs.opencv.org/2.4/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.html)

  

  ​                                                