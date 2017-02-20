**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I used Canny filter to extract the edges. Next, I add a region of interest mask that just focused on a triangle in the middle of image. Next, used hought transformation to detect lines in the region of interested and draw them on the image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by seperating the lines to "left", "right" and null, lines with slop between [0.5,1.5] belong to left lane line, lines with slop between [-1.5, -0.5] are right lane lines, everything else are noises that will be ignored. Then calculated the average of slop and intercept for all right lines and left lines. Finally, drew two lines between image bottom and middle as lane lines.
To avoid flicker lines, I cached the most recent 100 slop and intercept and use them to average, so that line position changes smoothly.


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are interfering lines like tree shadow, poor condition roads, draw_line will count wrong lines.
Another shortcoming could be it doesn't work for curve lanes.


###3. Suggest possible improvements to your pipeline


One improvement is to use weight when averaging the lines, longer lines have bigger weights, so that small noise lines won't effect the result a lot.
I also need to try better parameters.
