## Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="writeup-images/overview.png" width="975" alt="Overview" />

Overview
---
In this project, we will build a software pipeline to detect lane lines on videos through advance techniques such as color transforms, gradients, perspective transform and fitting polynomial.

Goals
---
- [Camera Calibration]()
  - Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
- [Pipeline (test images)]()
  - Apply a distortion correction to raw images.
  - Use color transforms, gradients, etc., to create a thresholded binary image.
  - Apply a perspective transform to rectify binary image ("birds-eye view").
  - Detect lane pixels and fit to find the lane boundary.
  - Determine the curvature of the lane and vehicle position with respect to center.
  - Warp the detected lane boundaries back onto the original image.
- [Pipeline (video)]()
  - Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.
- [Discussion]()
  - Discuss any problems / issues we faced in your implementation of this project. Where will our pipeline likely fail? What could you do to make it more robust?

Approach
---
- Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
- Apply a distortion correction to raw images.
- Use color transforms, gradients, etc., to create a thresholded binary image.
- Apply a perspective transform to rectify binary image ("birds-eye view").
- Detect lane pixels and fit to find the lane boundary.
- Determine the curvature of the lane and vehicle position with respect to center.
- Warp the detected lane boundaries back onto the original image.
- Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

Result
---
 Project Video          |  Challenge Video |  Harder Challenge Video
 :-------------------------:|:-------------------------:|:-------------------------:
 <img src="output_videos/project_video_out.gif" width="320" height="160" alt="Project" /> |<img src="output_videos/challenge_video_output.gif" width="320" height="160" alt="Challenge" /> |  <img src="output_videos/harder_challenge_video_output.gif" width="320" height="160" alt="Harder" />
 
Required Files
---
- [CarND-Advanced-Lane-Lines.ipynb](./notebook/CarND-Advanced-Lane-Lines.ipynb) ( Note book contianing run of implementation )
- [README.md](./README.md) (a report writeup markdown file)
- [project_video_output.mp4](./output_videos/project_video_output.mp4) (a video output that applies advance lane lines)

Camera Calibration
---
- [Camera correct matrix points](./notebook/CarND-Advanced-Lane-Lines.ipynb) Ref In [3]
  - chessboard size to 9x6 however just using 9x6 you will 3 images would fail when finding points
  - Use a range as in 5,6 to 6,7,8,9 you will find how the below function work
  - cv2.findChessboardCorners: to find corners
  - cv2.drawChessboardCorners: to draw the corner
  - cv2.calibrateCamera: to calibrate camera
  - result can be found in [./output_images/corner_x](./output_images/)
  <br><img src="output_images/point-calibration.PNG" width="850" height="240" alt="Point" />
- [Chess Undistort](./notebook/CarND-Advanced-Lane-Lines.ipynb) Ref In [7]
  - cv2.undistort: to undistort image using the calibated camera
  - result can be found in [./output_images/undistorted_calibrationX](./output_images/)
  <br><img src="output_images/chess-undistort.PNG" width="850" height="240" alt="Point" />

Pipeline (test images)
---
### [Example of Distortion Corrected Image and its application on test_images](./output_images/car-undistort.PNG)
  - cv2.undistort: to undistort image using the calibated camera
  - result can be found in **./output_images** [test1](./output_images/undistorted_test1.jpg), [test2](output_images/undistorted_test2.jpg), [test3](output_images/undistorted_test3.jpg), [test4](output_images/undistorted_test4.jpg), [test5](output_images/undistorted_test5.jpg), [test6](output_images/undistorted_test6.jpg), [straight1](output_images/undistorted_straight_lines1.jpg), [straight2](output_images/undistorted_straight_lines1.jpg)
  <br><img src="output_images/car-undistort.PNG" width="850" height="240" alt="Point" />

### [Create threshold binary image](./output_images/threshold-binary.PNG)
  <br><img src="./output_images/threshold-binary.PNG" width="850" height="240" alt="Point" />
- Color Channel Selection
  <br><img src="./output_images/color-channel.png" width="800" height="640" alt="Point" />

- Color transform
- Gradients
- 
undistort_and_threshold() function in code cell 6 applies color transformation and sobel operator to generated thresholded binary image.

As you can see in the images below "Saturation" (higher threshold) and "Hue" (lower threshold) channel of HSV image detects lane lines better than others. Also, absolute sobel threshold X method seem to identify lanes better than other thresholding methods.

Together with HSV color transform (H and S channel) and Sobel threshold X gradient, we obtain thresholded binary image.

Directional and Magnitude thresholds has very minimal to no effect on thresholded binary image.
Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image. Provide an example of a binary image result.
	

A method or combination of methods (i.e., color transforms, gradients) has been used to create a binary image containing likely lane pixels. There is no "ground truth" here, just visual verification that the pixels identified as part of the lane lines are, in fact, part of the lines. Example binary images should be included in the writeup (or saved to a folder) and submitted with the project.

## Lane Mask Generation
- Sobel Operation
- Gradient Magnitude & Direction
- Color Isolation
- High Intensity Detection
- Noise Reduction

## Perspective Transformation

## Pixel Histogram Analysis

## Polynomial Fitting

## Overlay & Inverse Transformation


OpenCV functions or other methods were used to calculate the correct camera matrix and distortion coefficients using the calibration chessboard images provided in the repository (note these are 9x6 chessboard images, unlike the 8x6 images used in the lesson). The distortion matrix should be used to un-distort one of the calibration images provided as a demonstration that the calibration is correct. Example of undistorted calibration image is Included in the writeup (or saved to a folder).

TODO


The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing your pipeline on single frames.  If you want to extract more test images from the videos, you can simply use an image writing method like `cv2.imwrite()`, i.e., you can read the video in frame by frame as usual, and for frames you want to save for later you can write to an image file.  

To help the reviewer examine your work, please save examples of the output from each stage of your pipeline in the folder called `ouput_images`, and include a description in your writeup for the project of what each image shows.    The video called `project_video.mp4` is the video your pipeline should work well on.  

The `challenge_video.mp4` video is an extra (and optional) challenge for you if you want to test your pipeline under somewhat trickier conditions.  The `harder_challenge.mp4` video is another optional challenge and is brutal!

If you're feeling ambitious (again, totally optional though), don't stop there!  We encourage you to go out and take video of your own, calibrate your camera and show us how you would implement this project from scratch!


