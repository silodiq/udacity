# **Finding Lane Lines on the Road** 

## By 狄强(John Di)

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image_from_pipline]: ./test_images_output/solidWhiteRight.jpg 

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 10 steps. 
1. get gray image from original image
2. define a kernel size and apply Gaussian smoothing
3. define our parameters for Canny detection
4. we'll create a masked edges image using cv2.fillPoly()
5. define a four sided polygon to mask
6. define Hough transform parameters,make a blank the same size as our image to draw on
7. Run Hough on edge detected image,Output "lines" is an array containing endpoints of detected line segments,lines = cv2.HoughLinesP(masked_edges, rho, theta, threshold, np.array([]),min_line_length, max_line_gap)
8. Iterate over the output "lines" and draw lines on a blank image ,draw_lines(line_image, lines, color=[255, 0, 0], thickness=5)
9. Create a "color" binary image to combine with line image
10. Draw the lines on the original image,original_img_with_lines = cv2.addWeighted(original_img, 0.8, line_image, 1, 0) , α=0.8, β=1., γ=0.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by "Add the judgment of the slope, filter out the line of the mutation."



image = mpimg.imread('test_images/solidWhiteRight.jpg')
image_from_pipline = lane_finding_pipeline(image)
plt.imshow(image_from_pipline)
mpimg.imsave('test_images_output/solidWhiteRight.jpg',image_from_pipline)

Can't get image by using method up, could you give me some help? Thanks.

![alt text][image_from_pipline]


### 2. Identify potential shortcomings with your current pipeline

1.The algorithm has low efficiency in filtering slope jitter.
2.The far end of the line has a burr, not clear enough.

### 3. Suggest possible improvements to your pipeline

1.Try a more efficient and real-time algorithm.
2.no idea...
