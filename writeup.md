# **Finding Lane Lines on the Road** 

## Report


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

### 1. Image Processing Pipeline

My pipeline consists of 6 steps:
* Conversion to binary black and white image;
* Filtering the noise by applying Gaussian blur;
* Edges extraction using Canny transform;
* Region selection;
* Edges to line conversion using Hugh transform;
* Distinction of left and right line; 

Those above steps are repeated until the two lines are found by decreasing the threshold value by 5 with each iteration.

Here is my pipeline in pictures:

![alt text][baseImage]

All grey colours are converted to black. Grey is defined as a colour for which all three components are lower than the threshold. Custom binImgFromGrey() function was used instead of provided grayscale(). It helped to eliminate the tree shadows on the challenge video.

![alt text][binImage]

The binary image is filtered by applying Gaussian blur.

![alt text][binGaussImage]

Afterwards the Canny edge detection is applied. 

![alt text][cannyImage]

Subsequently the region of interest is selected.

![alt text][cannyRegionImage]

On this edges Hough transform is applied to detect lines.

![alt text][houghImage]

Function aproxLines selects left and right line. The lines are assigned to left and right category based on expected pitch angle (+-7’). The best linear fit is calculated using np.polyfit. Function aproxLines takes min and max Y coordinates of the region to draw the marking and returns the combined image, and information weather both lines were detected or not.

![alt text][finalImage]


### 2. Shortcomings


Current pipeline is very sensitive on false edges with matching pitch angle inside the region of interest. This weakness was mitigated but not 100% solved by converting image to binary.


### 3. Possible Improvements

A possible improvement would be to define one region for left line and one region for right line. It would easily filter out all the shadows and false lines in the middle of the road.

Another potential improvement would be more sophisticated colour information processing.

For video processing information about line position from previous frames could be used to filter the output.
