# Testing Types
## Unit Testing
- does each unit work as specified 
- **all functions that we write should have unit tests**

## Integration testing
- do the units work when put together?
- checks interactions between different modules
- verifies that integrated components work together

## Functional Testing
- examines the the apps functionality 
- validates that the software meets requirements
- **does our project actually do what we want (in terms of satisfying use cases)**

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

# Continuous Integration 
	Goal is to identify Integration Issues Early on. This is done by automated testing.

- continuous pushing code to our repository 
- Integration usually happens when you write some new code, and write some tests for it demonstrating that it works
- Regular (usually daily) integrations are done by the developers
- When a push is made, an automatic build and test is triggered 


