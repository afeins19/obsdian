_Sorting_:  Arranging records in order
_Searching_: Finding a specific value in a record 

# Analysis of Search Algorithms
	finding a   particular value  in a list that checks each element in a sequence until the desired element is found or the list is exhausted
##  Linear  Search
### Time Complexity
_Best-Case_: Variable is at the start of the data structure -> O(1)

_Average-Case:_ Variable is on average half-way down the structure
->  O(N/2)

_Worst-Case:_ Variable is at the end ->  O(N)

## Binary Search
	divides the list we are searching into sections and searches within those sections, THIS REQUIRES THAT THE LIST BE ORDERED. 

1.  select start/end/mid-point elements in from the list 
2. if the element we are looking for is greater than mid point, we can ignore everything to the left of the mid-point (visa-versa for our element being less than the midpoint)
3. Repeat until our element is the mid point 

### Time Complexity 
	as we iterate over the list, we reduce the list size by 1/2. 

1. iteration 1: N/2 elements remain
2. iteration 2: N/4 elements remain
3. iteration 3: N/8 elements remain
...

_Worst-Case:_ O(Log(N)) 

## Selection Sort 
	start at first index and locate smallest element in the rest of the list. if smallest element in the rest of the list is smaller than the current element, we swap 

### Time complexity
	by the nature of this algorithm, we will always need to compare the selected element to every other element

**O(N^2)**

## Insertion Sort 
	orders values by  repetitively inserting into a min/max value into a sorted subset of the list  

- each time we select the next element, we  must compare  it to the elements previously sorted in the list

### Time Complexity 
_Best-Case_:  **O(N)**  - since the list  is  sorted, the element will not be compared against previously sorted elements 

_Worst-Case_: **O(N^2)** - we must compare with every element like selection sort

##  Bubble Sort
	orders  a list of values by repetitively comparing neighboring elements and swapping their positions if necessary. (values bubble to the top)

1. start  at first  element  and  compare  adjacent
2. if current is larger, swap it with adjacent 
3. set current to adjacent 

- after each pass the largest element in the unsorted  left side of the list will be in its correct position 

### Time Complexity 
_Best-Case:_ O(N)
_Worst-Case:_ O(N^2)

## Merge Sort 
	takes the list and divides the list in half until it consists of separate groups of 1 element. makes use of divide and conquer 

## Algorithm
1. divide the list into two roughly equal parts
2. recursively divide each part in half until a part contains only one element
3. merge the two parts into a single sorted list
4. continue to merge parts until the recursion unfolds 

_Time Complexity_: O(n log(n))









