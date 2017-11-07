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

### 1. Image Processing pipeline

My pipeline consisted of 5 steps. First, I converted the images to binary black and white image, then resulting image I applied Gaussian blur to filter out noise. Next I applied canny transform to extract edges. Afterwards I used Hough transform to convert edges to lines. Finally the lines are used in custom function to aproxLines to approximate left and right line. For videos this pipeline is repeated when last step haven’t found both lines with lower threshold in binary image conversion. Here is the my pipeline in pictures:

![alt text][baseImage]

First all grey colours are converted to black colour, grey is defined as a colour for which all three components are lower than the threshold. Custom binImgFromGrey() function was used instead of provided grayscale(). It helped a lot with the shadows on the challenge video.

![alt text][binImage]

Next binary image is filtered with Gaussian blur.

![alt text][binGaussImage]

On filtered image canny edge detection is applied

![alt text][cannyImage]

After edges are detected only region in front of the car is selected

![alt text][cannyRegionImage]

On this edges Hough transform is applied to detect lines all lines.

![alt text][houghImage]

Function aproxLines was implemented to fit left and right line to the results provided by Hough transform. The lines are first first assigned to left and right category based expected pitch angle (+-7’). Finally left and right line is fitted to this lines. Using np.polyfit the best linear fit is calculated. Function aproxLines takes min and max Y coordinates of the region to draw the marking. aproxLines returns valid indicating weather both lines were detected and combined image. Valid marker is only used in Video processing pipeline to lower the grey threshold. 

![alt text][finalImage]


### 2. Shortcomings


Current pipeline is very sensitive on false edges with matching pitch angle. This weakens was mitigated by converting image to binary instead of greyscale but it could still severely impact the lines detection.


### 3. Possible improvements

A possible improvement would be to define one region for left line and one region for right line. It would easily filter out all the shadows and false lines in the middle of the road.

Another potential improvement would be more sophisticated colour information processing.

Finally for video processing information about line position from previous frames could be used to filter the output.