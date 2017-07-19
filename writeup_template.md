# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

### Reflection

My lane detection pipeline was build as follows:
1) Convert the original image (video frame) to a grayscale image
2) Build masks for yellow and white pixels
3) Isolate yellow and white pixels
4) Apply gaussian blur to supress the noise
5) Apply a Canny edge detection
6) Isolate "region of interest" in front of the vehicle
7) Apply Hough transform and detect lines
8) Use np.polyfit to identify the lanes
9) Overlay lanes as two red lines over the original image (frame)

The step 8 required changes in the draw_lines function. I added detection of the slope for every line which was found in the step 7, so I could separate lines between right and left lane.
Then I used approximation with np.polyfit to identify first degree polynomial which represents a lane. By solving it with minimum "y" coordinate which was exctracted from all of the detected lines, I was able to get two lines which roughtly represent lanes on the road. 

### 2. Potential shortcomings with your current pipeline

The provided solution works for well for videos with straight lanes but in the "challenge" video there are problems with lane detection due to curved lanes in the top of the region of intrest. This happens due to my approach to the classification of hough lines by their slope, so in order to improve the pipeline I'll have to find a way to detect change in the slope of the lane.

It's also worth noting that test videos are recorded in the daylight and from straight point of view. If these conditions will not hold, my approach to find a region of intrest will fail to provide the correct region.

### 3. Suggest possible improvements to your pipeline

There is also a room for improvement to the approximation of lane lines. They should be approximated not just by regular line, but for some higher degree polynomial. I actually tried that, but could not supress the noise completely in the corners of the region of intrest, so I did not include this code to the review.
