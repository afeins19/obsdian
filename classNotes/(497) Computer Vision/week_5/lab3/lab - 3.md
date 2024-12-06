In this lab, the goal was to implement a color tracking algorithm to distinguish between red and non red objects on the screen. The algorithm will place a centroid in each red object the screen as well as a bounding box around the object 

# Algorithm 
the algorithm works in the following way: first we separate the image into color intensity matrices for each pixel value color. This lets us compare color intensities for each pixel color (Red, Green, Blue) for each pixel in the original image. We then apply the following heuristic:  
```red = (r>2*g) & (r>2*b) & (r>30);```

This ensures that the pixel currently being observed is at least twice as bright as the other values and at least 30 units above 0 in brightness. These conditions filter out non-red light, or white light which, although it has a high red intensity, also has a high intensity of the other pixel values. 

# Custom Code
in this function i implemented the code to do two things:
1. Plot a '+' in the centroid of each object in some given image
2. draw a bounding box around an object 

```MATLAB
function [] = processIm(im_loc)
    
    im = imread(im_loc)
    
    r=im(:,:,1); 
    g=im(:,:,2);
    b=im(:,:,3);
    
    % hueristic function for determining red only
    red = (r>2*g) & (r>2*b) & (r>30);
    
    % group all red objects within 5 pixels of each other as one object (this one should be tweaked)
    se = strel('disk', 35);
    red = imclose(red,se); 
    
    % remove all objects smaller than 35 pixels in area (adjust this threshold as needed)
    red = bwareaopen(red, 20);
        
        % Centroid 

    % separate red and NOT red 
    s = regionprops(bwlabel(red), 'centroid');
    S = vertcat(s.Centroid); 
    
    % plotting...
    figure 
    imshow(im)
    hold on
    plot(S(:,1), S(:,2), '+') % identify red objects with +
    zoom on
        

        % Bounding Box
    % get all red objects (appear as white blobs from intensity graph)
    stats = regionprops(red, 'BoundingBox', 'Centroid') % passing in red intensity binarized image
 
    hold on
    % This is a loop to bound the red objects in a rectangular box.
    for object = 1:length(stats)
        bb = stats(object).BoundingBox;
        bc = stats(object).Centroid;
        rectangle('Position', bb, 'EdgeColor', 'r', 'LineWidth', 2) % draw bounding box
        plot(bc(1), bc(2), '-m+') % mark centroid (x, y) with '+'
        a=text(bc(1)+15,bc(2), strcat('X: ', num2str(round(bc(1))), ' Y: ', num2str(round(bc(2)))));
        set(a, 'FontName', 'Arial', 'FontWeight', 'bold', 'FontSize', 12, 'Color', 'yellow');
    end 
end
```


# Results

### Initial Testing for Recognition of Red Objects

![[Pasted image 20241206091610.png]]


![[Pasted image 20241206092413.png]]

### Testing with Blue Object in frame 
```stats = struct with fields:
       Centroid: [1.2762e+03 227.7381]
    BoundingBox: [1.1755e+03 103.5000 201 253]
```
![[Pasted image 20241206091754.png]]

![[Pasted image 20241206093011.png]]

### Max Size Red Object Identification
`stats = 3×1 struct`

| Fields | Centroid              | BoundingBox                   |
| ------ | --------------------- | ----------------------------- |
| 1      | [637.7427,261.0458]   | [498.5000,94.5000,262,316]    |
| 2      | [895.3445,940.8040]   | [846.5000,812.5000,82,238]    |
| 3      | [1.0668e+03,312.3210] | [1.0145e+03,237.5000,111,126] |
![[Pasted image 20241206091117.png]]

`stats = 4×1 struct`

| Fields | Centroid              | BoundingBox                   |
| ------ | --------------------- | ----------------------------- |
| 1      | [956.2740,228.5847]   | [776.5000,7.5000,369,439]     |
| 2      | [1.2713e+03,638.5724] | [1.1815e+03,542.5000,184,186] |
| 3      | [1.2836e+03,48.7600]  | [1.2025e+03,1.5000,175,91]    |
| 4      | [1.4014e+03,191.1850] | [1.3555e+03,104.5000,91,174]  |
![[Pasted image 20241206091322.png]]
```stats = struct with fields:
       Centroid: [203.3797 193.3496]
    BoundingBox: [138.5000 119.5000 136 146]
```

### Unsuccessful or Faulty Recognition 
![](file:////tmp/ConnectorClipboard973424819504329071/image17334952236310.png)
*improper bounding boxes*

![[Pasted image 20241206092817.png]]
*no red objects detected*
# Conclusion 
This lab was a good first introduction into color recognition but the task gets a bit more difficult when we have images with both large and small red objects. By setting a static structuring element size, we may be overlooking or under filtering red objects. Also, as is clear from the `book.png` photo, its interesting to note that the bounding box combined adjacent red portions of the image (in the Japanese text) with the red book. I played with the `strel` size and got varying results to bound the red images .