# **Finding Lane Lines on the Road** 

## Report

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[baseImage]: ./test_images/solidWhiteCurve.jpg "Base Image"
[binImage]: ./test_images_output/binsolidWhiteCurve.jpg "Binary image"
[binGaussImage]: ./test_images_output/binGaussolidWhiteCurve.jpg "Filtered binary image"
[cannyImage]: ./test_images_output/CannysolidWhiteCurve.jpg "Canny esges image"
[cannyRegionImage]: ./test_images_output/cannyRegionsolidWhiteCurve.jpg "Canny esges region image"
[houghImage]: ./test_images_output/houghLinessolidWhiteCurve.jpg "After Hough Transform"
[finalImage]: ./test_images_output/solidWhiteCurve.jpg "Final Image"



---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][baseImage]

First all grey colors are converted to black color, grey is defined as a color for which all three components are lower than the threshold.

![alt text][binImage]

Next binary image is filtered

![alt text][binGaussImage]

On filtered image canny edge detection is applied

![alt text][cannyImage]

After edges are detected only region infront of the car is selected

![alt text][cannyRegionImage]

On this edges hough transform is applied to detect lines

![alt text][houghImage]

This lines are filteded based on expected angle (+-10) finally left and right line is fitted to this lines

![alt text][finalImage]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
