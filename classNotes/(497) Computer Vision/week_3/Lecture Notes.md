# Set Theory Operations on Binary Images 

![[Pasted image 20240918214011.png]]
1. Union $(A | B)$
2. Intersection $(A \& B)$
3. Complement (~A) 
4. Difference (A & ~B)
# More Fundamental Operations 
![[Pasted image 20240918214243.png]]

1. Translation 
2. Rotation
3. Reflection
# Example 
![[Pasted image 20240918214405.png]]
![[Pasted image 20240918214522.png]]
*Negation inverts pixels that are 0 to 1 and pixels that are 1 to 0* 

# Dilation 
Dilation is essentially growing the size of an image 
1. Rotate the structuring element (matrix) by 180 degrees - reflection
2. Slid the origin of the reflected structuring element (strel) over each pixel of the entire image matrix 
3. if **any element** of the strel matrix (1's) overlaps the original image's (1's), **place as "1" at the position of the strel origin in the final output image**

### Example of dilation 
Say we want to make the image more bold to have the same effect as the one below: 
![[Pasted image 20240918215450.png]]

We can setup our structuring element as follows: 
$$
strel=\begin{bmatrix}
0&1&0 \\
1&1&1 \\
0&1&0
\end{bmatrix}$$
This will take pixels and stretch them vertically and horizontally but not diagonally 


# `strel()` Function 
This function may be used with a few different parameters to develop a structuring element. In general, we can create one with 

### Example Usage of `strel()`
```MATLAB 
se = strel('disk', 5)         % circle with radius of 5 pixels
se = strel('line', 10, 45)    % line of length 10 pixels, 45 deg. angle
se = strel('square', 4)       % 4 x 4 pixel square 

% many other are available too 
```

# Erosion 
this is essentially shrinking an image 
1. Slide the origin of the structuring element over the entire metrix **DO NOT reflect (rotate 180 deg.) for imerode)**
2. if **All elements** of the strel matrix of 1's overlap the oroginal image. then place a "1" at the positoin of the strel origin *note that the strel must fit completely inside*
![[Pasted image 20240918221630.png]]

### Example of Erosion 
Lets apply the following structuring element on the following matrix: 

let S be the structuring element with
$$ S = 
\begin{bmatrix}
1 \\
1 \\
1 \\
\end{bmatrix}$$
and let im be the image (an 8x8 matrix) 
$$im=
\begin{bmatrix}
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&1&1&1&1&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
\end{bmatrix}$$
If we run `imerode(im, S)` over the image, we get the following matrix
$$
imerode(im,S)=
\begin{bmatrix}
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
0&0&0&0&0&0&0&0 \\
\end{bmatrix}
$$
This is because there are no instances where the all 1's in a portion of the original image overlap with the structuring element 

### Example 2: 
![[Pasted image 20240918223048.png]]

# Combining Erosion & Dilation 
![[Pasted image 20240918224034.png]]
Think of the structuring element as a paintbrush. If we want to fill the inside of the 2 peaks with the circular paintbrush, we 