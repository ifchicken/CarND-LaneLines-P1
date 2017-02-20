#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./report/org.jpg "Org"
[image3]: ./report/grayscale.jpg "Grayscale"
[image4]: ./report/edge.jpg "Edge"
[image5]: ./report/masked_edge.jpg "Masked_edge"
[image6]: ./report/hough_line.jpg "Hough_line"
[image7]: ./report/hough_line_with_extend.jpg "Hough_line_with_extend"
[image8]: ./report/result.jpg "result"


---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
* 1. change original image to grayscale image

![alt text][image2]
#### original image

![alt text][image3]
#### Grayscale image

* 2. call openCV function on gray scale image to gererate a Gaussian-smoothed image

* 3. call canny edge detection function on Gaussian-smoothed image to generate a edge image

![alt text][image4]
#### Edge image

* 4. define a mask area for the focus region and filter out other area, combine mask area with edge image to generate masked-edge image

![alt text][image5]
#### Masked-Edge image

* 5. call hough transform function with some threshold parameter to detect lines for mask-edge image, then draw the hough lines and combine with original image

![alt text][image8]
#### result image

In order to draw a single line on the left and right lanes, I created a new function called extend_lines() by moodified the draw_lines() function. I collected lines data and seperated them into left line and right line, then averaged each of them to get the average slope and extended them to boundary of image

![alt text][image6]
#### hough_line with original draw_lines() function

![alt text][image7]
#### hough_line with extend_lines() function

#If you'd like to include images to show how the pipeline works, here is how to include an image: 

#![alt text][image1]


###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be happened when there's some tree's shadow on the road(like situation in challenge.mp4), the noise would be large in masked-edge image, then the average of left and right line could be shifted a little bit


###3. Suggest possible improvements to your pipeline

A possible improvement would be to if we detected the line's color or slope at first and use it as reference, it could eliminate the noise a lot
