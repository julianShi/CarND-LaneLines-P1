# **Finding Lane Lines on the Road** 

## Writeup 

### Objectives

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve_edges.jpg "solidWhiteCurve_edges"

[image2]: ./test_images_output/solidWhiteCurve_masked_edges.jpg "solidWhiteCurve_masked_edges"

[image3]: ./test_images_output/solidWhiteCurve_lines_edges.jpg "solidWhiteCurve_lines_edges"

---

### 1. The pipeline
#### Step 1: smoothify the border of lanes
#### Step 2: detect the edges of the objects
151 was chosen as the low_threshold, 250 was chosen as the high_threshold to avoid detecting low-contrast edges. 
![solidWhiteCurve_edges][image1]
#### Step 3: define the region of the lanes
The following vertice is used to adjust the region according to the size of the image. 
```py
 vertices = np.array([[(0,imshape[0]),(np.floor(0.4*imshape[1]),np.floor(0.6*imshape[0])), (np.floor(0.6*imshape[1]), np.floor(0.6*imshape[0])), (imshape[1],imshape[0])]], dtype=np.int32)
```
#### Step 4: detect lines
The following parameters are chosen to avoid detecting short lines 
```py
    threshold = 40    # minimum number of votes (intersections in Hough grid cell)
    min_line_length = 100 #minimum number of pixels making up a line
    max_line_gap = 50    # maximum gap in pixels between connectable line segments
```
![solidWhiteCurve_masked_edges][image2]
#### Step 5: anotate the lanes on the original video
![solidWhiteCurve_lines_edges][image3]

### 2. Identify potential shortcomings with your current pipeline
The major shortcoming of the current pipeline is the error detection of lanes in the Challenge.mp4 case. The edges of the patches on the road were detected as the edges of the lanes. The issue could not be avoided by simply adjusting the parameters of cv2 functions. 

### 3. Suggest possible improvements to your pipeline
A possible improvement could be to add a higher level object recognition algorithm to seperate the edges of the patchs and the edges of the lanes
