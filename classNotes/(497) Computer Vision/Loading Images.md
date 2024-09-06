### Storing an image in a variable
```
im = imread('peppers.png'); 
```
### Displaying an image 
wont pop up, will create a clickable link 
```
imshow(im)
```
### Getting Dimensions and Image Attributes
```
% dimensions 
size(im) 
```
### Launching the imagetool
the image tool allows us to measure distances between pixels, select regions of pixels etc. We can zoom in enough to actually see the RGB values of each pixel
```
imtool(im) 
```
### Changing Display Planes 
matlab has images in 3 dimensions (x,y,z) where z is the color plane (1-3)
```
red = im(:, :, 1) % all red values of each pixel in the image
```
this will display things brighter that contain high values of the selected color plane and dimmer that contain less of the selected color plane 

### Grayscale 
the grayscale algorithm selects sort of middle ground average brightness for the conversion
```
rgb2gray(im) % grayscaling the image 
```
### Statistical Data of the Image 
getting min, max, and average pixel values for the image 
```
% say we have a grayscale image
gray = rgbb2gray(im)

% minimum of each column
minimum = min(gray) % note this returns the min val for each column only

% true minimum
true_minimum = min(min(gray)) 

% average 
% avg = sum(gray) / size(gray
```
### Histogram
shows quantity of pixels at a particular brightness value for our color plane 
```
% histogram 
imhist(gray)

```
