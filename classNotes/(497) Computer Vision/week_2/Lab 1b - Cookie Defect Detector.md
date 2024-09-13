*Aaron* Feinberg
CMPSC-497
Lab 1b - Detecting Defective Cookies 
Materials: Matlab, Cookies Camera (Phone)

# Discussion 
In this Lab, I tweaked and extended `processImage()` function from my Lab 1a to optimize it for the task of distinguishing Intact cookies from broken ones. The function will output a processed image, with the defective cookies having a large black 'X' through their center.  Each Cookie will also have its roundness metric displayed next to it. 

# Code 
The code is quite similar to that of Lab 1a, but there are a few adjustments. Below is the full function followed by the adjustments: 
```MATLAB 
% Importing cookie images 

im_1 = imread('/home/aaron/Pictures/cookies_2.jpg');

processCookies(im_1, .85, .2)

% importing function from previous lab 
function [total_objects, round_objects] = processCookies(im, roundness_threshold, graypoint)
    % display original image 
   imtool(im);
   
    % converting to grayscale 
    im_gray = rgb2gray(im);
    
    
    % binarizing the image (passing -1 lets us have the default algorithm choose the gray point)
    if graypoint == -1
        graypoint = graythresh(im_gray);
    end
    
    im_bin_threshold = imbinarize(im_gray, graypoint); % removes objects 
    
    % removing noise/grains 
    im_bin_denoise = bwareaopen(im_bin_threshold, 1000); % lots of tweaking 
    
    % filling in any holes in the image 
    se = strel('disk', 20); % lots of tweaking 
    im_bin_closed = imclose(im_bin_denoise, se); 
    im_bin_filled = imfill(im_bin_closed, 'holes');

    
    % Boundary and Label Matrices 
    [B, L] = bwboundaries(im_bin_filled, 'noholes')
    imshow(label2rgb(L, @jet, [.5 .5 .5])) % Displaying the distinct objects 
    
   
    
     % getting true and circular areas 
     stats = regionprops(L, 'Area', 'Centroid');
    
     % counting round objects (those that are above threshold value)
     objects_exceed_threshold = 0; 

      % appending more data to the graph 
    hold on 
  
    
    % drawing boundaries
    for k = 1 : length(B)
	    boundary = B{k}
	    plot(boundary(:,2), boundary(:,1), 'w', 'LineWidth', 2)
        
        delta_sq = diff(boundary).^2; 
        perimeter = sum(sqrt(sum(delta_sq,2))); 
    
        area1 = perimeter^2/(4*pi);
        area2 = stats(k).Area;
        
        area_true = stats(k).Area;
        metric = area2/area1
        
        metric_string = sprintf("%2.2f",metric);
        
        % plot a circle about the centroid 
        if metric < roundness_threshold 
	        centroid = stats(k).Centroid; 
            objects_exceed_threshold = objects_exceed_threshold + 1;
	        plot(centroid(1), centroid(2), 'KX', 'MarkerSize', 50);
        end 


    
        % plot the roundness or ciruclarity metric near the object 
        text(boundary(1,2)-100, boundary(1,1)+120, metric_string, 'color', 'y','FontSize', 14, 'FontWeight', 'bold'); 
    end 
    
     hold off

    sprintf("Total Cookies: %.f", length(B))
    sprintf("Total DEFECTIVE Cookies: %.f", objects_exceed_threshold)
    sprintf("Total INTACT Cookies: %.f", (length(B) - objects_exceed_threshold))
    
end
```
### Roundness Value 
it was interesting to note that a seemingly round cookie was actually not as round as expected (no intact cookies had a metric higher than 91%)
```MATLAB
processCookies(im_1, .80, .2); % roundness value of 85%
```
### Gray Point 
this also helped with the contrast and therefore the roundness calculations (although only slightly - in the range of ~5% increase for intact cookies)
```MATLAB 
processCookies(im_1, .80, .2); % graypoint of .2
```
### Disk approximation 
Adjusting this value to 20 allowed for slightly better roundness values for all intact cookies 
```MATLAB 
se = strel("disk", 20);
```

# Results 
![](file:////tmp/ConnectorClipboard9201542074631996431/image17261976060650.png)


![](file:////tmp/ConnectorClipboard9201542074631996431/image17261976060841.png)

ans = "Total Cookies: 12"

ans = "Total DEFECTIVE Cookies: 5"

ans = "Total INTACT Cookies: 7"

# Analysis & Conclusion 
There were a few interesting things to note from this lab. First, using my previous experience working with LAB 1a, I selected the Ritz Cracker Bites as their light color would contrast well against the black background. These cookies were stacked and although I did not expect it to be such a factor, the fact that the cookies were stacked crackers with a filling combined with the fact that there was a slight angle to the shot reduced their level of roundness. This explains the reduction in roundness overall of the intact cookies (10%) which was higher than expected. This however did not impede the algorithms ability to distinguish between intact and defective cookies. 