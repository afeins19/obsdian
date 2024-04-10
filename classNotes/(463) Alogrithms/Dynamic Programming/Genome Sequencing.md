Suppose you are trying to figure out the function of a region of a complex region, like the human genome for example. One approach is to look for similar regions in other animals (such as mice) and conjecture that those regions are "similar" to the corresponding part in humans. 


### Problem: Sequence Alignment
**input**: two strings X,Y over the alphabet $\sum = \{A,C,G,T\}$ some penalty value $\alpha_{xy}$ for each symbol pair $x,y \in \sum$, and a nonnegative gap penalty $\alpha_{gap} >= 0$.  

**output**: An alignment of X and Y with the minimum possible total penalty. 

a letter mismatch has a penalty of 2 while a gap mismatch only has a penalty of 1 for example ($\alpha_{gap} = 1$). 

ex: 
AGTACG
ACATAG
penalty = 8

A--GTACG
ACA-TA-G
penalty = 4 

### Brute Force 
the brute forces approach is wildly inefficient. For 2 sequences of 8 nucleotides, there are $10^{75}$ different allignments! 

![[Screen Shot 2024-04-09 at 12.32.15 PM.png]]

### Dynamic Programming Approach 
from any given position on the board except the border pieces. We can move down, right, or diagonally. So from every inner position, we can make 1 of 3 moves.


for example, the green position may be reached from the black, blue, and yellow positions.
![[Screen Shot 2024-04-09 at 12.33.19 PM.png]]
so we solve the subproblems for reaching those positions recursively until the first move. We can approach this systematically: 
![[Screen Shot 2024-04-09 at 12.35.27 PM.png]]

# Formal Algorithm 
![[Screen Shot 2024-04-09 at 1.08.26 PM.png]]![[Screen Shot 2024-04-09 at 1.12.49 PM.png]]