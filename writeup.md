# ** Writeup of "Finding Lane Lines on the Road" **

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

#### 1.1 summary
My pipeline consisted of following 6 steps.

| step       | purpose           | how  | note(T.B.D.) |
| ------------- |-------------| -----|---------|
| convert image to grayscale      | to detect edge not depending on time or color | cv2.cvtColor(image,cv2.COLOR_RGB2GRAY) | |
| blurring | to detect edges easily. in detail, smoothing images | blur_gray = cv2.GaussianBlur(gray,(kernel_size, kernel_size),0) | about kernel_size, set to 5 |
| detect edges | to detect edges | cv2.Canny(blur_gray, low_threshold, high_threshold) | about thresholds, set low, high = 50, 150. is these standard value ? |
| Hough transform | to detect the lane lines | cv2.HoughLinesP() |
| clip lane lines | to get the lane lines | mask pixels other than lane lines |
| draw lane lines | display detected lane lines | compose two lane lines from detected edge and draw | detail, refer 1.2 |

#### 1.2 draw lane Lines

In order to draw a single line on the left and right lanes,

separate line segments left line vs right line by their slope value "(y2-y1) / (x2-x1)".<br>
to calculate slope and intercept, I used np.polyfit() method.<br>
calculate average slope from each left and right line segments.<br>
and at last, calculate the 2 lane lines position



![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

in optional challenge file, my code is no good to detect.

### 3. Suggest possible improvements to your pipeline

There are the points to improve,
first, to modify parameters about hough transform
second, to modify region of detection
