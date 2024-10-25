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

