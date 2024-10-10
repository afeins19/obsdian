Recall extracting specific pixel colors from an image in MATLAB. 
```MATLAB
% open histogram
imhist()

% red intensity
red = RGB(:,:,1); % 2=green, 3=blue
imshow(red) 
```
*Note: In order to make sure that we only detect our specific color and not white, we have to make sure that the other color intensities are lower relative to the target one*

# Sample Algorithm
create a binary image of all the red pixels which will be white and all other colors will be black. 

![[Pasted image 20241009105705.png]]

### Code 
```MATLAB
r=RGB(:,:,1); 
g=RGB(:,:,2);
b=RGB(:,:,3);

% hueristic function for determining red only
red = (r>2*g) & (r>2*b) & (r>30);

% group all red objects within 5 pixels of each other as one object (this one should be tweaked)
se = strel('disk', 5);
red = imclose(red,se); 

% remove all objects smaller than 35 pixels in area (adjust this threshold as needed)
red = bwareaopen(red, 35);

% separate red and NOT red 
s = regionprops(bwlabel(red), 'centroid');
S = vertcat(s.Centroid); 

% plotting...
figure 
imshow(rgb)
hold on
plot(S(:,1), S(:,2), '+') % identify red objects with +
zoom on
```

