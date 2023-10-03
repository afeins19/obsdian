# Exercise 1
```python
import CommandLineTools as clt
import array

"Exercise 1"

def makeSetOfInts(vals: list):
    return set([int(val) for val in vals])

a =  input("please input your first list of comma separated values: ").split(",")
b =  input("please input your second list of comma separated values: ").split(",")

set_a = makeSetOfInts(a)
set_b = makeSetOfInts(b)

clt.header("Set Operations")
clt.header("a is a subset of b?")
print(set_a.issubset(set_b))

clt.header("a is a superset of b?")
print(set_a.issuperset(set_b))

clt.header("Union")
print(set_a.union(set_b))

clt.header("intersection")
print(set_a.intersection(set_b))

clt.header("difference")
print(set_a.difference(set_b))
```
## Output
```
please input your first list of comma separated values: 1,2,3,4,5
please input your second list of comma separated values: 2,3,4,5,6

Set Operations:

A Is A Subset Of B?:
False

A Is A Superset Of B?:
False

Union:
{1, 2, 3, 4, 5, 6}

Intersection:
{2, 3, 4, 5}

Difference:
{1}

```

# Exercise 2

**How can the last element of a set be deleted? Justify your answer? 4 points**

it is not possible to delete the last element in set. Sets are unordered collections of items so the notion of "last" does not apply to them.

# Exercise 3
	I convert the array to a set. if the length of the set and the array are equal that implies that no elements were removed (which only happens when there are duplicates)
```python
"Exercise 3"

def any_duplicates(arr: array.array):
    if len(set(arr)) == len(arr): # 
        return False
    return True

clt.header("Duplicates")
print(any_duplicates(array.array('i', [1,2,3,2])))
```
## Output
```
Duplicates:
True
```

# Exercise 4:
	I convert the arrays to sets and apply the intersection operation to create a new set. I then convert this set to a new array and return it  
```python
"Exercise 4"

def get_common_elements(arr1: array.array, arr2: array.array):
    return array.array('i', list(set(arr1).intersection(set(arr2))))

common_array=get_common_elements(array.array('i', [1,2,3,4]), array.array('i', [3,4]))

print(common_array)
```

## Output
```
array('i', [3, 4]) 
```

# Exercise 5

**Answer the following? 4 points  
a. Is a set a subset of itself? Explain? 

any set is a subset of itself as every element of this subset is contained within the superset. This is true for the case where the subset is the superset. 

b. What happens if you pass a dictionary to a set constructor? for example: set(dictionary1).  
Explain?

the set only seems to make use of the keys and pays no attention to the values. With the set of keys, all normal set behaviors are applied (duplicates are removed).
### Testing 
```python 
d={'a':1,'b':2,'c':3, 'c':4, 'd':3}  
print(set(d))
```

### Output
```
{'d', 'a', 'b', 'c'}
```




