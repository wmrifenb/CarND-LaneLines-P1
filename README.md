#**Finding Lane Lines on the Road** 

##Writeup

###William Rifenburgh (wmrifenburgh@gmail.com)

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./writeup_outputs/grayscale_solidWhiteCurve.jpg "Grayscale"

[image2]: ./writeup_outputs/canny_solidWhiteCurve.jpg "Canny Edges"

[image3]: ./writeup_outputs/regionimage_solidWhiteCurve.jpg "Region filtered Canny Edges"

[image4]: ./writeup_outputs/output_solidWhiteCurve.jpg "Final Output"

---

### Reflection

###1. Description of pipeline the draw_lines() modification:

My pipeline consisted of the following steps:

First, convert to grayscale:

![alt text][image1]

Second, perform canny edge detection:

![alt text][image2]

Third, filter to only the lane region:

![alt text][image3]

Fourth, use a hough transformation and modified version of draw_lines to draw the single line for the right and left lane boundaries:

![alt text][image4]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by taking the lines output by the hough transform openCV function and filtering them to find on the lines that had slope of 0.2 to 0.8 for the left boundary and between -0.8 to -0.2 for the right boundary.

For each lane boundary, the lines found to meet the slope criteria were used to create an average slope and an average y-intercept as in slope-intercept form of a line equation (y=m*x+b).

The inverse of the average slope-intercept equations was evaluated at y values for the top and bottom of the lane for both sides ( x=(y-b)/m ). The resulting x values were used to complete the coordinates for the vertices of each boundary line. 



###2. Potential (and current) Shortcomings

Shortcomings include an inability to track lane boundaries when the car switches lanes and a heavy depedence on sufficient tonal contrast between painted line markings and pavement.

The pipeline's result for the optional challenge video illustrates the last point when the road pavement briefly changes color from black asphalt to pale concrete.

###3. Possible Improvements

A possible improvement to help deal with poor tonal contrast between road pavement and lane line markings is to make use of all color channels available for edge detection.

Tracking line markings when switching lanes could be done by filtering for line slopes based on a moving average of slopes and y-intercepts across multiple image frames in time rather than filtering using hard coded values.

