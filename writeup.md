

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./output_images/actual_image.jpg "actual image"
[image2]: ./output_images/undistroted_image.jpg "Undistorted"
[image3]: ./output_images/combines_grad_s_image.jpg "combined grad image"
[image4]: ./output_images/warped_image.jpg "Warp Example"
[image5]: ./output_images/final_image_image.jpg "final image"
[video1]: ./project_video.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Advanced-Lane-Lines/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The code to calcualte the camera matrix  and distortion coefficient is available in the first cell. nIt take image path as input and calculate object points and image points for all the 20 images in the directory. It then uses these points to calculate different camera metrics using sc2.cameracalibration. We then use these metrics to calibrate an incoming image from the fornt camera.



### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

The above function is applied to the image below  
![alt text][image1]
and the output was
![alt text][image2]


#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

The Code to apply gradient tranformation and colr transformation is available in 3rd, 4th, 5th and 6th cell on the ipython notebook.
The code first applied sobel gradient x and then sobel gradient y and the magnitute gradation and lastly directional gradient. A combination all these four gradients and then applied along with the saturation part of the HLS colr spec. All this resulted in the following image

![alt text][image3]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

The code to apply perspective transformation is given in 7th cell of the ipython notebook. Given an img , source and destination it applies cv2.getPerspectiveTransform to give a matrix, which went applied on the image gives the wrapped image.
I apply this on the output from the transfromed image. The ouput of this is.

![alt text][image4]
#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

To identify lane lines and fit a poltnomial function on top of it. I used a sliding window approach. Here I draw a window around the lane lines and choose the pixels with positive value, the mean of those pixel is then choosen. the code for this is availabel in 9th cell of the ipython notebook.



#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

code to calculate the curvature is available in the  8th cell. it takes the first the 2nd derivative of the polynomial output from the previoius method and outputs the curvature for left and right lanes along with the distance of the car from the center of the lane. 

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

The final image was created after unwrapping the wrapped image back to the normal image frame. Resulting in

![alt text][image5]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_video.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

The problem that I faced during this was mostly coming up with the vales of the parameters for the Sobel gradients. The scenarios where the pipeline is nor going to do a good prediction are chnages in the color of the road. We need to come up with better combination of the mixting the gradients and color specs. Also the pipeline is not going to wrong in snowy road. We can use the car in front as a reference point in this case 
