$$\begin{bmatrix}  
a & b \\  
c & d   
\end{bmatrix} \times \begin{bmatrix}  
e & f \\  
g & h   
\end{bmatrix} = \begin{bmatrix}  
ae + bg & af+bh \\  
ce + dg & cf + dh   
\end{bmatrix}$$
in order to apply our algorithm on the positions of values, we need to note the positions of each element. The solution array with the relative positions of each element to their respective matrix is...
$$Z = \begin{bmatrix}  
x_{11}y_{11} + x_{12}y_{21} & x_{11}y_{12}+x_{12}y_{22} \\  
x_{21}y_{11} + x_{22}y_{21} & x_{21}y_{12} + x_{22}y_{22}   
\end{bmatrix}$$

In general, we we can get formula for each element of Z
$$Z_{ij} = \sum_{k=1}^n{x_{ik}\:y_{kj}}$$

The, we can find the values of Z for each element 
$$Z_{11} = \sum_{k=1}^2{x_{(1)k}y_{k(1)}}$$
$$Z_{12} = \sum_{k=1}^2{x_{(1)k}y_{k(2)}}$$
$$Z_{21} = \sum_{k=1}^2{x_{(2)k}y_{k(1)}}$$
$$Z_{22} = \sum_{k=1}^2{x_{(2)k}y_{k(2)}}$$
With our indexed matrices, we can now relate each element in z to the sum of elements in x and y. In general, 
$$z[i][j]=z[i][j]+x[i][k]+y[k][j]$$