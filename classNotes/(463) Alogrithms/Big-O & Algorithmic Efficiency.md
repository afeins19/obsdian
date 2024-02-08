# Execution Time
The time that a program takes to execute depends on the system load 
- CPU speed
- how many other tasks are running? 

# Growth Rate Approach 
	we want a measure of time complexity that does not depend on the hardware running it, only on the algorithm itself. We dont measure speed, we measure the increase in time relative to the increase in operations 
- approximates the effect of a change on the size of the input
- measures how fast an algorithms execution time increases as the input size increases 
- this approach compares two algorithms by examining their **growth rates**

# Big-O Notation 
- this notation obtains a function for measuring algorithm time complexity 
- ignore multiplicative constants and **non-dominating** terms in the function 

### How to Measure Time Complexity
- analysis is generally considered for the **worst case**
- if searching through a list of length n, if each search takes T seconds, then...
	- **Best case:** T(s) - the target item is first in the list 
	- **Average Case:** (T(s))/2 - the target is generally around the middle 
	- **Worst Case**: n(T(s)) - the target is at the end of the list 

### Big O Rules
![Screen Shot 2023-09-14 at 9.37.34 AM.png](app://ad2f7035d7a0644758f619cb5b640c4da28c/Users/aaronfeinberg/Documents/ObsidianVaults/School/Attachments/Screen%20Shot%202023-09-14%20at%209.37.34%20AM.png?1696375621524)

### Constant Time 
- Big O notation estimates the time of execution relative to the input size 
- if the time is **not** related to the input  size, the algorithm is said to take constant time with the notation O(1)
### Example 1
```python 
for i in range(n): 
	k += 5 
```
O(n) = c * n = n 

### Example 2
```python
for i in range(n): # O(n * n * c) = O(N^2) execution time 
	for j in range(n): # O(c * n) execution time
		k += i + j # constant O(c) execution time
```
- o(n^2)
### Example 3
```python
for i in range(n):
	for j in range(i):
		k += i + j # execution takes (c) or constant
```
- note that the big-o for this one is the same as the last one **O(n^2)** since we always consider the worst case (n -> infinity)

### Mathematically Deriving (Example 3)
| n | t (time) | i (iterator) |
| ---- | ---- | ---- |
| 0 | c | 0 |
| 1 | 2c | 1 |
| 2 | 3c | 2 |
| n | nc | n-1 |
$$ T = c + 2c + 3c + 4c + ... +nc = c(1+2+3+...+n) = c \frac{(n(n+1)}{2}$$
we then can reduce this to 
$$ T = c(\frac{n^2}{2} + \frac{n}{2})$$
$$O(c((n^2/2) + (n/2)) = O(n^2)$$

### Conditional Statements 
```python 
if e in list:
	print(e)

else:
	for e in list:
		print(e)
```
we still will be evaluating based on the worst case scenario, we must assume that both of the if and the else statement will execute 

**if statement** -> O(n) for the search (e in list) which will take O(n) time, the print function will take constant (c) time so in total we have O(n*c) = O(n)

**else statement** -> O(n) for the loop (for e in list) and constant time (c) for the print statement so in total we have O(n*c) = O(n)

combining the two statements, we have
$$ O(2O(n)) = O(2n) = O(n) $$
### Example: power function 
```python 
r = 1

for i in range(n): # O(n) time
	r *= a # constant time (c)
```
- time complexity is O(n * c) = O(n)

can we make this faster though?

```python 
r = a

# we let n = 2^k 
for i in range(k): 
	r = r * r
```

**Growth rate for this Algorithm **

| n | k |  |
| ---- | ---- | ---- |
| 1 | 0 |  |
| 2 | 1 |  |
| 4 | 2 |  |
| 8 | 3 |  |
| 16 | 4 |  |
| 32 | 5 |  |
| ... | ... |  |
| 256 | 8 |  |
| 1,048,576 | 20 |  |

Big-O now depends on **k** and we can derive that...
$$ k = log_2(n)$$
so our Big-O comes down to
$$O(c * log_2(n)) = O(log_2(n)) $$
this is much better than O(n) which grows much faster than log(n)

### Binary Search Efficiency
	binary search involves traversing a sorted list of elements. Start at the middle. If the target element is less than current value, disregard right half of list. If item is greater than current value, disregard the left have of the list. Continue until item is found. 

Binary search has a time complexity of 
$$ T(n) = T(\frac{n}{2}) + c = T(\frac{n}{2^2} + c + c) = T(n/2^k) + kc $$
- k = log_2(n) so the term T(n/2^k) = T(n/n) = T(1)
$$T(n) = T(1) + c(log_2(n)) = 1 + c(log_2(n)) => O(log_2(n)) $$
### TODO: Research growth rate of tower of hanoi (look at powerpoints from today's slides)

# Fibonacci Numbers 
$$0,1,1,2,3,5,8,13 \\...$$

recall the recursive approach to finding these 
```python 
def fib(index):
	if index == 0: # base case 
		return 0
	if index == 1: # base case 
		return 1
	else:
		return fib(index-1) + fib(index-2)
```

### Time Complexity with recursion 
	if we let just use the above function, we end up with 2 operations for first index, 4 for the second, 8 for the third and so on which leaves us with an exponential time complexity:

$$O(n) = 2^n$$
this value diverges the quickest of all time complexities. 

# Asymptotic Analysis
	a mathematical definition of Big-O notation 

_Asymptote_: a line that continually approaches a given curve but does not meet it at any finite distance 
![[Screen Shot 2024-01-18 at 12.20.41 PM.png]]

### Upper Bound 
	worst case. This is what Big-O is. 

![[Screen Shot 2024-01-18 at 12.24.56 PM.png]]![[Screen Shot 2024-01-18 at 12.25.05 PM.png]]
- if we find a number c and n_0 such that
- $$T(n)\le c \times f(n) \:\:\: \forall n \ge n_0 $$
### Lower bound 
	we also have a definition for the lower bound (best case scenario for our algorithms)
	
![[Screen Shot 2024-01-18 at 12.38.46 PM.png]]
### Exact Bound  
	we can find a range where T(n) is bounded between 2 functions 

![[Screen Shot 2024-01-18 at 12.39.43 PM.png]]

