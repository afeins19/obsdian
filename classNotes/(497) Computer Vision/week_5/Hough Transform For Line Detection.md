# Hough Transform 

(Notes From https://docs.opencv.org/3.4/d9/db0/tutorial_hough_lines.html) 

a line in Cartesian space is usually represented with parameters $(m, b)$. We may also apply the polar coordinate system and parameterize using $(r, \theta)$.

![[Pasted image 20241024223302.png]]

For Hough Transforms, we can express lines in the Polar Coordinate System. The equation for line Y can be expressed as 
$$y = (-\frac{\cos\theta}{\sin \theta})\;x \; + \; (\frac{r}{\sin \theta})$$
- $x = r \cos\theta$
- $y = r \sin \theta$ 

we know that $x^2 + y^2 = r^2$ and so $r = \sqrt{x^2 + y^2}$. To obtain our angle $\theta$, we apply
$$\frac{y}{x} = \frac{r\sin \theta}{r\cos \theta} = \tan \theta$$
so the inverse yields...
$$\theta = \tan^{-1}(\frac{y}{x})$$
we then construct a Hough accumulator matrix (H) in the following way:
- rows = different values of r
- columns = different values of $\theta$

$$\begin{bmatrix} 
r_{1}\theta_1 \; r_{1} \theta_{2} \; \dots \\
r_{2}\theta_{1} \; r_{2}\theta_{2}\; \; \; \ddots 
\end{bmatrix}$$

Since these $(r, \theta)$ values represent lines, points that are co linear will vote on the same values values of $r$ and $\theta$ that correspond to their line in Hough Space. 


### Canny Edge Detection  

We first apply Canny Edge Detection to find the edges in the given image. This follows an algorithm of blurring the image slightly and detecting areas with relatively high changes in their intensity gradients (a key property of edges). We can then sort these into real edges, potential edges, and non-edges. We then look at adjacent points on potential edges to see if they are similar.

# Code 
I implemented the the code to perform the above theory. the `detectLines()` function takes in the path to some image and then performs the hough lines detection. I had to tweak the sensitivity parameter of the  `cv.HoughLines()` function for each image due to the distance each photo was taken from the road. 

```python 
import cv2 as cv
import numpy as np
import math
import time



def detectLines(img_loc, sensitivity):
    
    # loading image 
    img = cv.imread(img_loc, cv.IMREAD_GRAYSCALE) # convert to gray

	# canny edge dectetion
    canny = cv.Canny(img, 50, 200, None, 3)

    # save edges to be displayed later im final image 
    img_edges = cv.cvtColor(canny, cv.COLOR_GRAY2BGR)
    
    # apply hough transform 
    lines_detected = cv.HoughLines(canny, 1, np.pi /180, 125, None, 0, 0)

    # constructing accumulator matrix
    accum = []

    if lines_detected is not None: 
        # make and draw lines 
        for i in range(len(lines_detected)): 
            rho_cur = lines_detected[i][0][0]
            theta_cur = lines_detected[i][0][1]

            # get x,y coordinates of each point in cartesian space
            a = math.cos(theta_cur)
            b= math.sin(theta_cur)     
            x0 = a * rho_cur
            y0 = b * rho_cur

            # store values 
            accum.append((rho_cur, theta_cur))

            # generate points and plot 
            pt1 = (int(x0 + 1000*(-b)), int(y0 + 1000*(a)))
            pt2 = (int(x0 - 1000*(-b)), int(y0 - 1000*(a)))
            cv.line(img_edges, pt1, pt2, (15,230,230), 2, cv.LINE_AA)

        print(f"Lines={len(accum)}")
        
       


    else:
        print("no lines")


    cv.imshow("Original:", img)
    cv.imshow("Detected Lines: {str(len(lines))}", img_edges)

    while True:
        k= cv.waitKey(1) & 0xFF
        if k== 27: # esc
            cv.destroyAllWindows()

   
if __name__ == "__main__":
    import os

    os.environ["QT_QPA_PLATFORM"] = "xcb" # linux issue
    IMG_LOC = '/home/aaron/Projects/classWork/CMPSC497/learn_opencv/hw_labs/hough_line_detection/test/highway.jpg'
    detectLines(IMG_LOC, sensitivity=440)
```
# Testing
testing took quite a bit of tweaking of the sensitivity parameter.

### Original Image

![[Pasted image 20241025111600.png]]

### Grayscale

![[Pasted image 20241025111632.png]]

### Canny Filtered and Lines Overlayed
![[Pasted image 20241025111636.png]]