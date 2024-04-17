a self balancing binary search tree named after Adelson-Velsky and Landis. These trees are structured such that they are dynamically balancing. The rules of AVL trees are as follows: 
### Height
each node in an AVL tree stores a balance factor, which is the difference in heights between its left and right subtrees. This factor must be one of three values: {-1,0,+1}.
### Rotations 
to maintain the balance after insertions and deletions, AVL trees use rotations. They are the standard four rotations: 
- r-rotation
- l-rotation
- l-r rotation
- r-l rotation 
# Time Complexity 
AVL Trees always guarantee that searching will always take $O(logn)$ time. There is increased space complexity however due to the fact that each node must maintain a balance factor attribute. 