- divide - split the input array into its left and right halves 
- conquer - use 2 recursive calls to subarrays 

### Pseudocode
![[Screen Shot 2024-01-25 at 12.42.46 PM.png]]

### Comparison Subroutine 
![[Screen Shot 2024-01-25 at 12.43.23 PM.png]]

### Analysis
![[Screen Shot 2024-01-25 at 12.45.19 PM.png]]
*at every level, for n levels, how much work do we have to do?*:
	remember, that at every level, we need to perform that array comparison subroutine. 

1. i := 1, j := 1 - 2 operations
2. for k:=1 to n - n operations 
3. if statement or else statement - 4 operations 

![[Screen Shot 2024-01-25 at 12.56.33 PM.png]]

### Big-O Analysis
![[Screen Shot 2024-01-25 at 12.56.48 PM.png]]