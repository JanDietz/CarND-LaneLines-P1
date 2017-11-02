# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/solidWhiteCurve.jpg "Original"
[image2]: ./test_images_output/gray_solidWhiteCurve.jpg "gray"
[image3]: ./test_images_output/edges_solidWhiteCurve.jpg "edges"
[image4]: ./test_images_output/edges_masked_solidWhiteCurve.jpg "edges masked"
[image5]: ./test_images_output/line_image_solidWhiteCurve.jpg "lane lines"
[image6]: ./test_images_output/image_final_solidWhiteCurve.jpg "final image"

---

### Reflection
### 1. Description
My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I detected edges in the image. Next step was masking the image with edges. Next I performed a Hough transform and determined lane lines. Last I added the new left and right lane line boundary to the original image by keeping them transparent.

The pipeline including the output can be seen on the following images:

#### 1. Coversion image to grayscale

![alt text][image2]

#### 2. Detecting edges

![alt text][image3]

#### 3. Masking edges

![alt text][image4]

#### 4. Determining lane lines
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separation section into left and right lines and a interpolation section to genereate one line for left and right side. Please note here that the drawing part is outsourced to function draw_polynom.

The separation is done by checking the line's slope for being negative or positive. In case of a negative slope I assigned it to left lanes group. In case of positive I assigned to the right. To make the code more robust the line's slope must have a magnitude greater than 0.5. Than I used function np.polyfit to interpolate the lines for each side. Function Output are parameters of a Polynomial of degree 1. Therefore x values must be calculated upon defined Polynomial parameters and y values. For y I defined that the line starts at the bottom of the image and ends almost in the middle of the image.

![alt text][image5]

#### 5. Put lane lines over original image

![alt text][image6]




### 2. Potential shortcomings


- One potential shortcoming would be that the separation is done by only checking the line's slope. Also the line's location in an image could be an indicator for the correspond side.

- Also the edge dectection performs not well on overexposed images.

- Curves can simulated not well by one line. A line covers the information for a very short distance.

### 3. Possible improvements

- Considering line's location for the separation

- Make the edge detection more adaptive 

- Another potential improvement could be to detect curves somehow by using a multi Polynomial curve fitting function which enables the machine an anticipatory driving.
