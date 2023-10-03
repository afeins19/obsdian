	consider a game of sudoku with some numbers already filled, the filled numbers reduce the size of the solution set  

- __variables__: the empty boxes to be filled in on the board
- __Domain__: the set of values which can be put into a given variable
- __constraint__: rules of the game which constrain the values of a given variable

# Popular Problems Solved with CSP
- CryptArithmetic (coding alphabets to numbers)
- n-Queen problem
- Map-coloring (coloring regions of a map such that no 2 regions have the same color)
- crossword puzzles
- sudoku

# CryptArithmetic Problem

|     | L (9)| O |  G |  I | C | |
| --------| -------- | -------- | -------- | -------- |-------- | -- |
|     | L (9)| O |  G |  I | C | + |
|   P (Carry 1) | R | O |  L |  O | G | |
|   (1)| (8) | (0) |  (9) | (0) | (4) |  |

- _Domain_: {0,1,2,3,4,5,6,7,8,9}
- Constraints
	1. Every character should have a unique value 
	2. Cannot start with 0 
	3. Only One solution allowed 
	4. Addition of two numbers should be even
	5. Carry should always be 1 

## Creating More Constraints for our problem as we solve 
	1. O must be 0 as o+o=o
	2.  G+G=l => G+G = 9
	3. I + I must end in 0 so let I = 5 => I+I=10

_Solution_: {
	0 -> O 
	1 -> P
	2 -> C
	3 
	4 -> G
	5 -> I
	6 
	7
	8 -> R
	9 -> L  }

## Example: Map Colorization Problem 

__Variables__: {WA, NT, Q, NSW, V, SA, T}
_Domain_: {red, green, blue}
constraints: 
1. neighboring regions must have differing colors

![[Screen Shot 2023-09-12 at 1.02.22 PM.png]]