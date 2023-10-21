# Testing Types
## Unit Testing
- does each unit work as specified 

## Integration testing
- do the units work when put together?

## System testing
- does the system work as a whole 

# Unit Testing 
- example: bubble sort - what kind of unit tests what we write for this sorting algorithm 

Bubble:
	look at adjacent nodes, swap?
	next 

**swap** is the unit in this algorithm...this is what we need to be testing 

## Testing Swap 

**1,3,2,5, 1**

test: swap(1,3) -> should not swap returns (1,3)
test: swap(3,2) -> should swap returns (2,3)
test: swap(1,1) -? should not swap returns (1,1)



