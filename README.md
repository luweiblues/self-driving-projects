# *Finding Lane Lines on the Road*
---

## Reflection

## 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consists of the following steps:
1. convert the image to grayscale
1. blur the image with gaussian blur so to remove some pixel noise
1. use the Canny Edge detection algorithm to convert the image with only edges
1. mask the image with a region of interest (the region is hard-coded)
1. apply Hough transform to find pixels that are connected or on the same line
1. group the hough lines together based on the slope of each line, and if a line has a slope very close to the average slope, then add it to become part of the line group
1. do linear regression fitting to get a slope and a point of all the line points collected for each line group
1. extrapolate the line based on the slope and point from the previous step, and use the region of interest to bound the extrapolated line
1. draw the extrapolated lines onto the original image


### 2. Identify potential shortcomings with your current pipeline

**Issue 1**

The detected lines lacks some stability and is shaky. This especially obvious and problematic in the optional challenging video. This is due to the noises of hough lines. 

**Issue 2**

There is another shortcoming related to the extrapolation of the lines within the region of interest. Currently, simple the x's lower and upper limits of the region of interest are used to bound the line drawing. But it may not necessarily bound the line within the region of interest, especially when the region of interest is not of rectangular shape.


### 3. Suggest possible improvements to your pipeline

**For Issue 1**

To improve, fine-tuning parameters are needed.

**For Issue 2**

It is entirely possible to use some polygon clipping library to clip the extrapolated lines instead of using the simple lower and upper bound methods.
