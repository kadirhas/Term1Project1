# **Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/solidWhiteCurve_lanes.jpg "Result of lane detection function"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
I have defined several functions to solve this problem. The first one was for lane detection. In this function, I have converted the image to HLS color space since it is easier to seperate bright colors such as white and yellow in HLS. I have applied threshold to only luminosity value 200 since most of the time lanes have the brightest colors. Then I've applied a mask to only get the lines in the region of the interest and remove the unnecessary parts of the image to reduce cpu workload. After that, I've used canny function has been used to find the edges. With hough function, only several lanes are left to interpolate.

![alt text][image1]

To draw the lanes, first left and right lanes are seperated by their slope in the draw_lines function. If they are horizontal or vertical, they aren't collected Then for each of the lane groups (left and right) y = mx + b formula has been used to find their slope (m in the formula) and intercept (b in the formula). Since the longer lines are more valuable, their length are calculated and for each lane to use as weight. Then I've used weighted average of the intercept and slope. After that since the lanes should be start and finish at the edges of region of interest, using these average m and b values, I have calculated two x points for the lane.




### 2. Shortcomings


* Currently the threshold values didn't set for yellow and white seperately. So it might miss some of the lanes. 
* Since there is no tracking, a disturbance would distrupt the result. 
* Current algorithm only works for 960x540 images.

### 3. Possible improvements

* Different thresholds for different colors would improve the chance of getting more lanes
* After converting the image in grayscale, using something like CLAHE would remove the effects of shadows
* Applying Kalman filter, or any other tracking method would increase robustness of the algorithm
* A parametric approach would remove the 960x540 requirement. 