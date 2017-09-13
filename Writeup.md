
# **Finding Lane Lines on the Road** 

---


[//]: # (Image References)

[image1]: solidWhiteRight_grey.jpg "Grayscale"
[image2]: solidWhiteRight_canny.jpg "Canny"
[image3]: solidWhiteRight_roi.jpg "ROI"
[image4]: solidWhiteRight_hough.jpg "Hough"
[image5]: solidWhiteRight_final.jpg "Final"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale and applied Gaussian smoothing by using the function gaussian_blur() with a kernel_size = 5.
![alt text][image1]

Canny function is called on the Gaussian-smoothed grayscaled image to detect edges using parameter values of high_threshold = 150 and low_threshold = 50
![alt text][image2]

Then the detected edges are filtered using region of interest mask.
![alt text][image3]

The filtered images are then passed through Hough transform using the parameter values of rho = 2, theta = pi/180, threshold = 5, min_line_len = 30 and max_line_gap = 20
![alt text][image4]

The lines are then overlayed on the edge image.
![alt text][image5]

Function draw_lines() draws lines with color and thickness on the image. Based on the slope of the edge lines, I split the points into left and right lines. Then I used polyfit() to get the left and right coefficients. From the coefficients, I calculated the xmin and xmax for the left and right lines. Function cv2.line() was used to draw the lines on the edge image.

### 2. Identify potential shortcomings with your current pipeline

1. The lane detection seems to overshoot the lane markings when there are curves.

2. The line drawings on the videos is shaky.


### 3. Suggest possible improvements to your pipeline

1. Instead of linear model, if we fit line to polynomial it could probably work better when the road is curvy.

