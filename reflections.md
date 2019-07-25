
# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps:
* Convert the image to grayscale
* Add Gaussian blur
* Add Canny edges
* Add a mask to specify a region of interest on top of the image with the Canny edges.  The masked was made with a simple triangle.
* I found the lines in the image using the Hough transformation which found points of intersection in Hough space that represented lines in image space.
* Then drew the lines using `draw_lines()`
* Finally I composited the two images together using `weighted_img()`

In order to draw a single line on the left and right lanes, I enhanced the simple the `draw_lines()` function by separating the lines based on slope.  If it had a positive slope it would be a line on the left-hand side.  If it had a negative slope, it was a line on the right-hand side.  This only worked because the sample data only contained images of long roads that did not curve. 

I then took the grouped lines and found the line of best fit through all the points.  I used this slope and y-intercept to make a nice long line from the bottom of the image to about the middle of the image.


### 2. Identify potential shortcomings with your current pipeline
The code to determine if a line corresponded to the left or right lane does not work for curved roads.  It's simply using slope as the delimiter which only works for straight roads. 

I also hard-coded the area of interest.  This would not work for steep roads or hilly roads where the road is not always a set below a certain y-axis in the image.

My code would also fall apart if the car was crossing lanes.


### 3. Suggest possible improvements to your pipeline
 A more robust solution to determine lane grouping of the lines would be to take position into account and use a clustering algorithm.  I tried using K-means clustering to separate the lines into two groups, the left and right lane, but actually got worse results then with my simple algorithm. 

An image segmentation algorithm would be great for determining which area of the image is the road.  By preprocessing the image to segment out the road from the image automatically I could then apply my lane extraction code.
