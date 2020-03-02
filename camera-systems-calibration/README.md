# Calibration different camera systems

## Executive summary
A vast amount of industries depend on high-quality images, ranging from entertaiment to AR/VR.  In order to obtain them, correctly working cameras are crucial. The process of adjusting camera parameters is called camera calibration. Usually cameras come with parameters predefined by manufacturer. However, environment conditions such as humidity highly influence camera lens, which introduces distortions to images. The goal of camera calibration is to solve such issues.
Calibrating the camera means obtaining internal camera-specific parameters (intrinsics) and reltions of this camera to other cameras (extrinsics). Instrinsics include lens focal length and optical centers. 
 
 Calibration pipeline consists of two major steps: 
1. Collecting photos of some pattern (commonly chessboard) from more than 5 different perspectives
2. Applying algorithm, which obtains camera parameters

We run our expreriments for different patterns and calibration algorithms and compare our results  with default camera parameters on metrics namely absolute error, reprojection eror, ADD MORE.
## Single camera calibration
### 1. Image collection
 Our initial setup is as follows: 1) we fix printed chessboard on the table and make it as smooth as possible 2) Under the vertical light we collect at least 15 photos from different views by moving the camera. We make photos in the way that chessboard takes more than 90% of the picture. 
 
### 2. Calibration algorithm
For every image we find chessboard and its internal corners on the image. Then for obtaining camera parameters we apply algorithm from OpenCV library. 

## Stereo camera calibration

## Calibration camera-projector system
Distance from camera to plane: ~35cm
## Conclusions

## References 
