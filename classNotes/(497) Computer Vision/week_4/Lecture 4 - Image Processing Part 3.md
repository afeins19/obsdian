### Topics 
- Equalizing histogram 
- Linear (spatial) filters
- Line Detection 
- Edge Detection 
- Hough Transform 
- Lab 2
- HW 3 

# Equalizing Histogram 
takes a grayscale image and equalizes the histogram values 
- `nlev` - number of intensity levels for the output (usually 256)
```MATLAB
g = histeq(input, nlev)
```

# Linear Filter Mask 
This is is using a mask to apply a convolution over an image. The elements of the mask are multiplied by corresponding elements of the image and then they are summed

### Idea
slide the mask matrix over every pixel and perform a calculation on each overlapping cell, then add the results. Replace the image cell value located at the center of the mask matrix. Move to next pixel in the image and repeat until the last number in the mask 

### Example
Let an image be given by a one-dimensional matrix given by: 
$$
\begin{bmatrix}
0 \ 0 \ 0 \ 1 \ 0 \ 0 \ 0 \ 0
\end{bmatrix}
$$
Let a mask be a one-dimensional matrix given by: 
$$
\begin{bmatrix}
1 \ 2 \ 3 \ 2 \ 0 
\end{bmatrix}
$$
Note that the **center** of the mask is 3

We slide the mask over each index of the image and perform the operation described above in idea. 

In the end we end up with a matrix of size $n+m-1$

### Creating Masks & Filters
first we can define an image `im1` and a `mask`. We can then apply `imfilter()` to slide the mask over the image and perform the convolution 
##### Without Padding 
```MATLAB 
% image
im1 = [0 0 0 1 0 0 0 0];

% mask 
mask = [1 2 3 2 0];

% applying the filter 
imfilter(im1, mask)
```

the result will be `[0 0 2 3 2 1 0 0]` - note that by default this retains the same size as the image.

##### With Padding 
```MATLAB 
% applying the filter (with padding) 
imfilter(im1, mask, 'full') 
```

the padded result will have be analogous to the pure math result of this correlation: `[0 0 0 0 2 3 2 1 0 0 0 0]`. 



### Using Masks for Line and Point Detection 
We can design masks to perform operations such that we can reduce the image to a series of lines, edges, points etc. 

For example, if we want to perform edge detection, we may apply the following masks

**Example:**
**Detecting Horizontal Lines**
$$\begin{bmatrix}
-1-1-1-1\\
2 \ 2 \ 2 \ 2 \\
1-1-1-1
\end{bmatrix}$$
moving the 2's into the position that matches the shape of the lines we'd like to detect will allow us to detect various types of lines 

### Setting up these masks in MATLAB
```MATLAB 
% Horizontal line 
horizontal_mask = [-1 -1 -1 ; 2 2 2 2 ; -1 -1 -1 -1]; 
```

### Image Example 
![[Pasted image 20240926205448.png]]

# Edge Detection 
to detect edges, we find first order derivatives of the image using the gradient. Say the Goal is to Estimate the values of $G_x$ and $G_y$. We first find the gradient:
$$
\nabla f = 
	\begin{bmatrix}
		G_x \\
		G_y
	\end{bmatrix}
=
\begin{bmatrix}
		\frac{\partial f}{\partial G_x} \\
		\frac{\partial f}{\partial G_y} 
	\end{bmatrix}
$$
We can then find the magnitude of the gradient using the euclidean distance formula:
$$
\nabla f = mag(\nabla f) = [G_x^2 + Gy^2]^\frac{1}{2}
$$
we can then simplify this roughly by focusing only a small change  in f with respect to the variables: 
$$
\nabla f \approx |G_x^2 + G_y^2| \approx |G_x| + |G_y|
$$
We can then find the angle of the maximum rate of change in the following way: 
$$
\alpha(x, y) = tan^{-1}(\frac{G_y}{G_x})
$$
### Common Edge Detection Masks 
- Sobel 
- Prewitt
- Roberts

we can automatically generate these masks with Matlab by passing them into the `edge()` function 

**Example:**
`g = edge(Im, 'sobel')`

![[Pasted image 20240926211234.png]]

# Hough (huff) Transform 

### Brute-Force Approach
a technique used to find lines in an image (typically after edge detection is completed)

### Technique
- consider all lines that pass through a particular point (x.y) in the image given by the general equation $y=mx+b$
- we then look at the equation in **parameter space** -> convert to (a,b)
	- equation of a line in (a,b) space $b = -xa + y$
- points which are co-linear in (x,y) space is the a,b parameter space. note that this method does not apply to vertical lines as the slope $m \rightarrow \infty$ 
![[Pasted image 20240926214810.png]]

we basically draw lines through both points and the area of where they both intersect provides the parameters for the equation of that line? 

### Hough Transform Approach
The Hough transform solves the problem of inability to detect vertical lines by parameterizing the equations into a an angle and a perpendicular line (called the $\rho\Theta$ space) 

We define a line normal to $\rho$ with the following equation: 
$$xcos \Theta + y sin \Theta = \rho$$
![[Pasted image 20240926220456.png]]

in the $\rho\Theta$ space, the equivalent set of lines in a Cartesian plane appear as a pair of sinusoidal lines. The intersection of these two sinusoids indicates that points are co linear at that point in (x,y) space. We generate a point for each point in that space and then we count the intersections: 

![[Pasted image 20240926222303.png]]

its a good idea to perform some preliminary type of edge detection before doing the Hough Transform to remove unwanted noise and having to create sinusoidal waves for unnecessary points. 

### Hough Transforms For Finding Equations of Lines 
by performing edge detection with a technique above (prewit, sobel, etc.) we can then pass the processed image (or some cropped subset of the image) into a Hough Transform and get the actual equations for the lines we want

![[Pasted image 20240926222643.png]]

### Code For Hough Transform 
```MATLAB 
im = imread('circuit.tif')

% roate the image for some more difficulty 
rotim = imrotate(im, 33, 'crop')'

fog1 = imshow(rotim);

% apply canny edge detection initially 
BW = edge(rotim, 'canny');

% create hough transform 
[H, theta, rho] = hough(BW); 

% plotting the peaks
P = houghpeaks(H, 5, 'threshold', ceil(0.3*max(H(:))));
x = theta(P(:,2));
y = rho(P(:,1));

%plot lines
% highlight longest line in red 
lines = houghlines(BW, theta, rho, P, 'FillGap', 5, 'MinLength', 7);
```

The seven in the last argument in the houghlines() function indicates that we dont want to count lines with less than 7 colinear points (too small of a line)

### Hough Transform for finding circles 
Say we have the following image: *tape.png*
![[Pasted image 20240926223647.png]]

The Hough transform can a circle that's partially obscured! this is done in the following way: 
```MATLAB 
RGB = imread('tape.png');
imshow(RGB);

% need to supply estimate of radius (in pixels)
Rmin = 60;
Rmax = 100;

[center, radius] = imfindcircles(RGB, [Rmin Rmax], 'Sensitivity', 0.9)
```

**Output given those parameters**
```
center = 236.9291 172.4747 % (x,y of the center point of circle)
radius = 79.5305 % radius of the circle 
```

**Displaying the Circle**
```MATLAB
viscircles(center, radius);  % displaying the circle

% display overlay 

hold on;
plot(center(:,1), center(:,2), 'yx', 'LineWidth', 2);
hold off; 
```

### Example: Finding lane lines in the road 
![[Pasted image 20240926224320.png]]

# More Useful Matlab commands 
- `imtophat() and imbothat()` - tophat reduces the original image minus the opened image (remove uneven illumination) while bothat is the original image minus the closed image (enhances contrast)
- `medfilt2()` - remove salt and pepper noise with median filtering 
- `imclearborder()` - removing objects that are on border of the image 
- `imfill(BW, 'holes')` - filling some holes
- `BW =im1 > 100` - creates a binary image from grayscale in a shorthand way (this value may be adjusted)
- `BW2 = ~BW1` - inverts the binary image - all zeros become ones and all ones become zeros 
