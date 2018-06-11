---
layout: page
title: Vehicle Detection
description: 
img: /assets/img/project_vehicle_detection/vehicle_detection.png
thumbnail: /assets/img/project_vehicle_detection/vehicle_detection.png
---


In this project, our goal is to write a software pipeline to identify vehicles in a video from a front-facing camera on a car. The steps of this project are the following:
Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
Normalize features and randomize a selection for training and testing.
Implement a sliding-window technique and use our trained classifier to search for vehicles in images.
Run our pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
Estimate a bounding box for vehicles detected.


## Histogram of Oriented Gradients (HOG)

I started by reading in all the vehicle and non-vehicle images. Let's take a look at what a car image and a non-car image look like.

<img class="two" src="{{ site.baseurl }}/assets/img/project_vehicle_detection/car_vs_non_car.png">    


I then explored different color spaces and different skimage.hog() parameters (orientations, pixels_per_cell, and cells_per_block). I grabbed random images from each of the two classes and displayed them to get a feel for what the skimage.hog() output looks like. Here is an example using the RGB color space and HOG parameters of orientations=9, pixels_per_cell=(8, 8) and cells_per_block=(2, 2):

<img class="two" src="{{ site.baseurl }}/assets/img/project_vehicle_detection/hog_features.png">    


## Train SVM Model

I trained a linear SVM using LinearSVC() in skLearn. The following table shows that the test accuracy of LinearSVC using different parameters. We chose 'YCrCb' as the 'color_space' due to its highest test accuracy.


<img class="one" src="{{ site.baseurl }}/assets/img/project_vehicle_detection/svm_accuracy.png">

## Select Window Size and Overlap Ratio

Restricting search area on the image could effectively filter out false positives (cells that are not cars but identified as cars).
Note that the classifier is trained using .png files, so we need to scale the data before predicting. To select the right window size and overlap ratios for both x and y axis , I used the following possible values for window size: (32,32), (64,64), (96,96), (128,128) and the following ratios for xy_overlap: (0, 0), (0.3, 0.3), (0.5, 0.5). The following graph shows (32,32) windows with (0, 0),(0.3, 0.3),(0.5, 0.5) overlapped ratio respectively.

<img class="three" src="{{ site.baseurl }}/assets/img/project_vehicle_detection/window_size_and_ratio.png">



## Test Vehicle Detection


![Output sample]({{ site.baseurl }}/assets/img/project_vehicle_detection/test_detection.gif)
