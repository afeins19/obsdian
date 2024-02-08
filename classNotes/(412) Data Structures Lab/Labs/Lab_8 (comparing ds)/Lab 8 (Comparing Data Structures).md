# Code 

## Imports & Libraries
```python
# value generation  
import random  
import timeit  
from prettytable import prettytable # used for printing data in tabular format  
from LinkedLists.SinglyLinkedList import linkedlist as ll
```

## Data Structure Testing 
```python
# generating 1000 integers between 1 and 1000  
vals_list = [random.randint(1,1000) for i in range(10000)]  
  
# generating a dictionary of the integers  
vals_dict = {k : v for k,v in zip(vals_list, vals_list)}  
  
# generating a linked list from the values  
vals_ll = ll()  
for val in vals_list:  
vals_ll.append(val)  
  
# generating a bianry search tree  
vals_bst = build_tree(vals_list)  
  
# custom utility functions  
def measureTime(fun, vals=None, run_count=1):  
if vals:  
return timeit.timeit(lambda: fun(vals), number=run_count)  
return timeit.timeit(lambda: fun(), number=run_count)  
  
# order of times is list, dict, bst, ll  
time_dict = {  
"print": [],  
"retrieve": [],  
"insert": [],  
"delete": []  
}  
```
## Getting Time Values 
```python 
# Printing:  
time_dict["print"] = [measureTime(print, vals_list),  
measureTime(print, vals_dict),  
measureTime(vals_bst.pre_order_traversal),  
measureTime(vals_ll.traverse)]  
  
# Retrieval  
  
# generating 5 unique random numbers  
to_find = random.sample(vals_list, 5)  
  
def findVal(iterable):  
return [i in iterable for i in to_find]  
  
# Measure retrieval time  
# measureTime(vals_list.index, vals=to_find[0])  
time_dict["retrieve"] = [measureTime(findVal, vals=vals_list)/5,  
measureTime(findVal, vals=vals_dict)/5,  
sum([measureTime(vals_bst.search, vals=i) for i in to_find])/5,  
sum([measureTime(vals_ll.find_node, vals=i) for i in to_find])/5]  
  
# removal (will remove random numbers generated in to_find)  
# getting indecies for the values to pop from the list  
time_dict["delete"] = [sum([measureTime(vals_list.remove, vals=i) for i in to_find])/5,  
sum([measureTime(vals_dict.pop, vals=i) for i in to_find])/5,  
sum([measureTime(vals_bst.delete, vals=i) for i in to_find])/5,  
sum([measureTime(vals_ll.delete, vals=i) for i in to_find])/5]  
  
time_dict["insert"] = [sum([measureTime(vals_list.append, vals=i) for i in to_find])/5,  
sum([measureTime(vals_dict.update, vals={i:i}) for i in to_find])/5,  
sum([measureTime(vals_bst.insert, vals=i) for i in to_find])/5,  
sum([measureTime(vals_ll.append, vals=i) for i in to_find])/5]  

```
## Table Creation 
```python
# average time Table creation and populating  
avg_time_tb = prettytable.PrettyTable()  
avg_time_tb.title = "Average Times"  
avg_time_tb.field_names = ["Operation", "List", "Dictionary", "BST", "Linked-List"]  
  
# statistics table  
ds_indicies = ["list", "dict", "bst", "ll"]  
min_time_dict = {}  
  
rank_table = prettytable.PrettyTable()  
rank_table.title = "DS Sorted by Min Time"  
rank_table.field_names = ["-", 1,2,3,4]  
  
  
for k in list(time_dict.keys()):  
# adding rows to the table for each value in the dict for each operation  
row=[k]  
row.extend(time_dict[k])  
avg_time_tb.add_row(row)  
  
  
  
for k in list(time_dict.keys()):  
# adding rows to the table for each value in the dict for each operation  
row = [k]  
vals = [ds_indicies[time_dict[k].index(val)] for val in sorted(time_dict[k])]  
  
row.extend(vals)  
  
rank_table.add_row(row)  
  
  
#[ds_indicies[time_dict[k].index(val)] for val in sorted(time_dict[k])]  
print(avg_time_tb)  
print(rank_table)
```

# Raw Data Table
![[Screen Shot 2023-12-08 at 1.26.44 PM.png]]

# Ranking Data Structures Table 
![[Screen Shot 2023-12-08 at 1.27.21 PM.png]]

# Conclusion 
Each of these data structures has their own unique advantages and disadvantages. 
pythons dictionary however seems to trump all other data structures across these operations. For operations like retrieval and printing (which is retrieval with a few more steps), dictionaries offer performance on the order of O(1) as they rely on a simple memory lookup. Deletion is also quite fast for dictionaries since there the values are not "tied" to any other values in the data structure other than the key (which is also deleted). 

Binary Search Trees are a close second for all except insertion. This is reasonable as (when a tree is balanced), we can expect performance on the order of O(logn), however, if the tree is not balanced the performance degrades to O(n) and essentially mimics a linked list. My binary search tree was not self balancing so we may not reach the full O(logn) performance potential. When testing an insert, we must still traverse quite a few elements to reach a leaf node.

Linked lists did not provided great performance comapred to the other algorithms. This is also true in some cases for general lists. This is likely due to having to make wider traversals than the other data structures. Bsts will inherently reduce walks needed (if atleast a little balanced), and dictionaries are always O(1). The random nature of this lab ensures that we may only expect lists to do when data is near the start. 