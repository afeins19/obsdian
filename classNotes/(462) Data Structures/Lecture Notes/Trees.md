	non linear data  structure - usefull for representing data which is stored in some heirarchical order. 
- comprised of a set of nodes in which elements are stored and edges connect one node to another 
- each node is located on a particular level
- a tree can only have **one** root node 
- a node can only have **one** parent 

## Nodes 
nodes are the "containers" for our data and are stored with their relations to other nodes inside the tree 

## Important Terms
_Height of Tree_: length of path from root to leaf nodes 
_Height of node_: path length from node to leaf node
_Depth of node_: path length from root to node 
_Siblings_:  nodes that share the same parent 
_Leaf Node_: node with no children 
_Internal Node_: Node with at least one child that is not the root 

## Sub Tree 
a tree structure that is made of of part(s) of the tree

## Tree Classification 
trees can be classified in a few ways. The criterion we use is the maximum number of children we can have and the "balance of a tree"

_Binary Tree_: Trees which have at most 2 children

### Balanced Tree
a tree is balanced if all the leaves of a tree are on the same level or within 1 level 

![[Screen Shot 2023-09-28 at 9.33.15 AM.png]]



### Full Tree
all leaf  nodes are in the same level
![[Screen Shot 2023-09-28 at 9.34.02 AM.png]]

### Complete Tree
all leaf nodes are on same level or 1 level below 
![[Screen Shot 2023-09-28 at 9.34.35 AM.png]]

## Tree Traversal 
- for linear structures the process of iterating through elements is fairly obvious (forwards or backwards)
- Trees are non-linear and are more interesting to traverse

_Pre-Order_: visit the root, then traverse the sub trees from left to right
- Root -> Left side -> Right Side

_Level-Order_: visit each node at each leve of the  tree from top (root) to bottom and left to right
- 1 -> 2  -> 3

_In-Order_: traverse the left sub tree, then visit the root, then visit the right side
- Left side -> Root ->  Right Side

_post order_: traverse the sub-trees from left to right  and then visit the root 
- Left side -> Right  Side ->  Root 

*Note: for traversals we always consider 3 nodes at a time*


# Binary Search Trees

## Adding elements

1. new elements are added as leaf nodes
2. start at rooth
3. follow path dictated by existing elements (compare to each element in tree)
4. continue to a node with no child 

## Removing Elements

**Cases**:
- node to remove is a leaf node 
	- trivial removal
- node to remove has one child
	- replace the node with its child
- node to remove has 2 children 
	- choose the node which will not violate the bst rule

## Software Architecture
- Node class to represent node
	- data attribute 
	- left child attribute
	- right child attribute 
	- set Node to default 



