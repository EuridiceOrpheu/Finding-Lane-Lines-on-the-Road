# **Finding Lane Lines on the Road** 



The goals / steps of this project are the following:

* detecting line segments from images applying grayscaling, Gaussian smoothing, Canny Edge Detection and Hough Tranform line detection
* connect/average/extrapolate line segments 
* write a short report 


[image1]: ./examples/grayscale.jpg "Grayscale"

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 7 steps:
1.I converted the images to grayscale 
2.I added a Gaussian smoothing using kernel_size=5 (it should be positive and odd)
3.I applied Canny transform
4.I defined a mask to store  only the region of interes (the polygon is formed from `vertices` (which  I determined based on the size of the image )
5.I applied the Hough Tranform on mask selection
6.I extrapolate line segments returned by Houth transformation in two  lines (left and right lanes)
7.Finally I overlaped the left and right lines on  images

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by applying some formulas for extend the 
the line segment between (x1, y1) and (x2, y2)  to the line y - y1 = m * (x - x1),where m is the scope.
(By solving for y and for x, we get the equivalent formulations: y = m * (x - x1) + p.y and x = (y - y1) / m + x1.)
For y1,y2,y11 and y22  I took the value from the plot of  an image ,but for x1,x2,x11 and x22 I calculate them using  x = (y - y1) / m + x1.
(x1,y1) represent the point where left line starts and (x2,y2) represent the poin where  left line ends.Same for the right line (x11,y11),(x22,y22).
Also In the draw_lines() function,at the beginning, I filtered the line segments by slope value.(Graphically, a negative slope means that as the line on the line graph moves from left to right and a positive slope means that the line on the line graph moves from right to left). 



### 2. Identify potential shortcomings with your current pipeline

The preprocessing of video is slow and the code for finding lines on the road for "challenge.mp4" can be optimized. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to transform line segments in one curved line .
Another potential improvement could be to filtering the original image down to white and yellow at the very beginning for having better results.
