
# Self-Driving Car Engineer Nanodegree


## Project: **Finding Lane Lines on the Road** 

---

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

[solidWhiteCurve]: ./test_images/fl_solidWhiteCurve.jpg "Solid White Curve"
[solidWhiteRight]: ./test_images/fl_solidWhiteRight.jpg "Solid White Right"
[solidYellowCurve]: ./test_images/fl_solidYellowCurve.jpg "Solid Yellow Curve"
[solidYellowCurve2]: ./test_images/fl_solidYellowCurve2.jpg "Solid Yellow Curve 2"
[solidYellowLeft]: ./test_images/fl_solidYellowLeft.jpg "Solid Yellow Left"
[whiteCarLaneSwitch]: ./test_images/fl_whiteCarLaneSwitch.jpg "White Car Lane Switch"

---

### Reflection

### 1. Description of the pipeline.

My pipeline consisted of 6 steps:
1. I converted the images to grayscale,
2. I applied a gaussian blur on the grayscale image to smooth the locals high variations of the colors' intensity,
3. I applied a Canny transformation on the blured image,
4. I applied a mask to define a region of interest; this region of interest corresponds to a perspective view, with a focal almost at the center of the image,
5. I then applied a Hough transformation to find the lanes.
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
    Iterate on each line and:
    1. calculate the slope of the line,
    2. discard the line having an outbound slope, ie a slope greater than 0.8 or lesser than 0.3,
    3. if the slope is lesser than 0, put the 2 points defining the line in the left lane array,
    4. if the slope is greater than 0, put the 2 points defining the line in the right lane array,
    
    Then, for each lane:
    1. compute the center of this cloud of points,
    2. compute a linear regression of this cloud of points,
    3. discard the outbound slope of this linear regression,
    4. compute 2 points to define a line, having the slope of the linear regression and passing by y = height, y = half height and the center,
    

I obtained the following results:

---

1. Solid White Curve: ![Solid White Curve][solidWhiteCurve]
2. Solid White Right: ![Solid White Right][solidWhiteRight]
3. Solid Yellow Curve: ![Solid Yellow Curve][solidYellowCurve]
4. Solid Yellow Curve 2: ![Solid Yellow Curve 2][solidYellowCurve2]
5. Solid Yellow Left: ![Solid Yellow Left][solidYellowLeft]
6. White Car Lane Switch: ![White Car Lane Switch][whiteCarLaneSwitch]

---


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the day is not as sunny as in the white.mp4 and yellow.mp4 videos (when it rains, or during the night, or the sunset). The Canny transformation outlines accurately the lanes because there is a strong contrast between the road and the lanes. For example, in the extra.mp4 video, a part of the road is light (instead of dark). The current pipeline cannot find successfuly the lanes on several images, because the contrast is not high enough.

Another shortcoming could be when there is for example a shadow of a tree on the road. The pipeline not optimized for the challenge finds the contour of the shadows of the threes and messes up the computation of the lines.

Another shortcoming could be when the car changes of lane. As the region of interest of this pipeline is the focal point of the image, the current pipeline could not find lines with a higher slope.


### 3. Suggest possible improvements to your pipeline

A possible improvement could be to have a bird-eye view of the image, to have parallel lanes, instead of converging lanes.

Another potential improvement could be to use polynomial regression (at least of degree 3), instead of a linear regression to draw the lines, to have lines which follow the lanes in the curves.


### 4. Optional challenge

In order to find the lanes on a part of the challenge video, I added a filter to highlight the white and yellow of the images.
It works fine for this challenge but it does not work in case where the lanes are not yellow, nor white.


```python

```
