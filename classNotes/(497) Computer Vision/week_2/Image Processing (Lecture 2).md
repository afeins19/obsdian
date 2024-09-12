# Image Processing vs Computer Vision 
although theres alot of overlap, image processing usually refers to preprocessing of images while computer vision is a continuation and more complex interpretation of images

# Image types 

### RGB Image 
- m x n x 3 dimensional image 
- Each pixel is in range 0-255 (8-bit architecture)
- Each pixel is in range 0-1023 (10-bit architecture)
- Indexing: (row, col, color_layer)

# Intensity image 
this is also known as gray-scale. Its A single layer image. 
- m x n image (single layer)
- each pixel is 0-2555 (for 8-bit)
- indexing: (row, col)
- created with `rgb2gray(im)`

# Binary image 
- m x n (single layer)
- Each pixel is **0 or 1**
- indexing: (row, col)
- created with `imbinarize(im)` 
Its also possible to binarize an image by setting a threshold value to quantize pixels too. For example, say we have a binarized image `bw1 = imbinarize(im)`. We can also do something like `bw2 = im > 100` which quantizes all pixel intensities greater than 100 to 1 and less than or equal to 100 to 0. 

# Image Pixel Coordinate System 

### General Pixel Indexing
note that in MATLAB there are 2 pixel indexing systems in use. The first is the one on the left which is the most familiar to us. Pixels are index (row, col, color_plane). Note that the x-axis applies to the column and the y-axis applies to the row.  

In things like IMTool, the second type of coordinate system is applied. Pixels are addressed by their (x,y) position with x going from 0 to image_width and y going from 0 to image height.
![[Pasted image 20240911121132.png]]

# In Class Lab - Detecting Round Objects

![[Pasted image 20240911123433.png]]

This lab will show us how to write a program to overlay a display of how "round" a given object is. 

### Algorithm For Detecting Circular Objects
1. first read in am image `rgb = imread(RGB);`
2. create a gray-scale version of the image `gray = rgb2gray(rgb)`
	- we will also find what MATLAB determined was the gray threshold value with `threshold = graythresh(gray)` - this is done so that when the image is binarized, we can get the clearest contrast image 
3. Using the gray image and the threshold value, we can binarize the image using the gray threshold value for max contrast - `bw = imbinarize(gray, theshold)` 
4. Remove all objects containing fewer than 30 pixels (note that this number depends on the size of the image and other factors such as noice...its adjustable) This is done to remove any grains or noise from the image 
	- `bw1 = bwareaopen(bw, 30);`
5. Fill a gap in the marker cap (green object in top right). We can use a paint brush object to close the gap between the 2 seemingly separated portions of the marker cap 
	- we select the structuring element aka the paintbrush with                         `se = strel('disk', 2);`
	- we then fill the gap with `bw2 = imclose(bw1, se);`
6. We then fill in all holes in the image (any enclosed areas will have their internal areas filled) 
	- this is done with `bw3 = imfill(bw2, 'holes');`
7. Get the pixel which represent the boundaries of each object 
	- This is done with `[B,L] = bwboundaries(bw3, 'noholes');`
		- B is a data structure which holds the boundaries of objects and the L is a label matrix holds the distinct objects within the image as unique integers. The label essentially groups pixels together that correspond with a particular object enclosed by a boundary 
	- We can then apply some color to display the distinct objects that the algorithm found `imshow(label2rgb(L, @jet, [.5 .5 .5]))`
![[Pasted image 20240911130511.png]]
8. by typing `hold on` after step 7, we can allow multiple graphics to be added to the same plot 
9. Another cosmetic step, we use the boundary variable to plot the boundary pixels in black. This is done with the following code
```MATLAB
for k = 1 : length(B)
	boundary = B{k}
	plot(boundary(:,2), boundary(:,1), 'w', 'LineWidth', 2)
end 
```
10. Find the area (in pixels) of each object and the centroid coordinate (x,y) for each object in the label matrix with `stats = regionprops(L, Area, 'Centroid');`
11. Loop over each object in the boundary data structure and sum the distances between each pixel in the boundary using the standard euclidiean distance formula (full code below)
$$d = \sqrt{(x_2-x_1)^2 +(y_2=y_1)^2}$$
12. we then super impose a circle with the same area as a given object with the same area in the following way: 

A circle's perimeter is represented by 
$$p = 2\pi r$$
give that we know the perimeter of the object, we can find the radius of a circle with the same perimeter by rewriting in the following way: 
$$r = \frac{p}{2\pi}$$
Given that the area of a circle is given by $$a=\pi r^2$$
we can insert our radius value into the formula: 
$$a = \pi r = \pi (\frac{p}{2\pi})^2 = \pi \frac{p^2}{4\pi^2} = \frac{p^2}{4\pi} $$
13. we then find the true area of the figure using the raw pixel values 
	- `area_true = stats(k).Area;`
14. We Compute the "circularity" metric by seeing how much of area_true is contained within area 1 
	- `metric = area2/area1`
15. assign a threshold value for "circular enough" objects and plot a black circle in the center of each object 
```MATLAB 
% plot a circle about the centroid 
if metric > threshold 
	centroid = stats(k).Centroid; 
	plot(centroid(1), centroid(2), 'ko');
end 

% plot the roundness or ciruclarity metric near the object 
text(boundary(1,2)-35, boundary(1,1)+13, metric_string, 'color, 'y','FontSize', 14, 'FontWieght', 'bold'); 
```




