# **Finding Lane Lines on the Road** 

---


[//]: # (Image References)

[image1]: ./test_images_output/grayscale.jpg "Grayscale"
[image2]: ./test_images_output/canny.jpg "Canny Edge"
[image3]: ./test_images_output/lanedetectedgemask.jpg "Region Intrest"
[image4]: ./test_images_output/lanedetectlinemerge.jpg "Lane detected"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale and then I applied Guassian filter with kernal size 3 to remove noise.  Then I used Canny edge detection method to identify the edges in the gray scale image. Then I masked the edge image with a polygon to get the image region of interest. The hough line transform was used to identify the line segments in the edge detected image. 

![alt text][image1]

![alt text][image2]

![alt text][image3]

In order to draw a single line on the left and right lanes, I did following modification for the draw_lines() function 

- finding slope for each line segments identified by hough transform
- Categorizing each line to left lane/ right lane by comparing slope in specific range
- Calcuating resultant line (for both left and right lanes) by doing a ploynomial fit from corresponding category of lines.  

finally the original image and lane line image was superimposed. 

![alt text][image4]


### 2. Identify potential shortcomings with your current pipeline


I used fixed end point for the lane line (in the y axis), might not be good solution for representing lanes on curvy roads. 480 for 1280 * 720 video and 330 for 960 * 540 video.

If a line was not found in video frame (only for challenge.mp4, especially for right lanes), i used the lane  coordinates from older frame to have continuity in the video.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to Identify curvy road lanes. 
