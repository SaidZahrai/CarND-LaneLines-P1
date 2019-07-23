** This is a lab in Udacity Nanodegree for Self-driving car, forked from [CarND-LaneLines-P1](https://github.com/udacity/CarND-LaneLines-P1) at Github.

# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)


### 1. Description of my pipeline. 

My pipeline consisted of 5 steps:
1. Converted the images to grayscale
2. Blur the image
3. Find edges
4. Mask the region of interest
5. Use Hough transform to find lines in the image

The pipeline worked after some parameter tuning.

To interpolate/extrapolate the found lines, I modified draw_lines in the following way:
1. Assume that all the discovered lines can be classified into two classes, one with positive slope and one with negative slope.
2. For each found line, calculate the slope and classify the line based on that.
3. For each class, positive and negative slopes, calculate the middle point of the found line.
4. For each class average the middle point coordinates and the value of the slope.
5. For each class, use the averaged coordinate of the middle points as one point on the line and the average slope and draw a line that goes from the lowest edge to the end of the region of interest.
This is working for most of the images, but for some, the average slope was not correctly representing the desired lane line. I solved this problem with an extra step of filtering the lines by looking at their slopes and accepting only those that have a value withing the acceptable range.


### 2. Potential shortcomings with the current pipeline

There are several potential shortcomings and the algorithm is a relatively simple one. Some of those are below ones:
1. The parameters need to be tuned based on actual conditions and quality of the lane lines. 
2. The lighting conditions have likely a strong impact.
3. Weather conditions will change the view and make the algorthm to break down.
4. Shadows and reflections will cause problems.
5. Surface damages of the road will be found as lines.  

### 3. Suggest possible improvements to your pipeline

1. Look more specifically on the color of the found regions.
2. Start with filtering of the input image and smooth out irregularities.
3. Use the knowledge about direction of motion to filter out discovered lines that are not relevant.
4. Correlate the information with the previously found information to eliminate outliers.

### 4. Challenge problem

I tried to find a solution to the final challenge. With the first solution, when many line segments are considered, the pipeline was finding many regions that were not related to the lane itself. The second method, with filtering the lines, was much more successful. Most of the time, it finds the lane lines. As the right lane line is missing markers in some regions, the right line is fluctuating a bit. This can of course be solved by time-correlation.   



