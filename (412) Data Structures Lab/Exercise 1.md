1. Linked List (generic)
- Insert(): this operation is on the order of O(1) since we just append the item to an unsorted list

- DeleteMin(): this operation is O(n) since the list is unsorted and we must traverse it to find the item to be deleted 

2. Sorted Linked list
- Insert(): this operation is on the order of O(n) in the worst case since we must traverse the list to find the correct spot for the item being added 

- DeleteMin(): the sorted property of the linked list allows for a constant O(1) deletion time since the minimum valued item is always at the beginning of the list 

3. Binary Search Tree (BST):
- Insert(): in the worst case, we would have an unbalanced bst which would be [[Lab 8 (Comparing Data Structures)-1]]equivalent to the linked list in function with insertion time on the order of O(n) 

- DeleteMin(): the unbalanced BST would also have a time complexity of O(n) as we may have to traverse it entirely when its unbalanced 

4. Binary Heap: 
- Insert(): in the worst case, we could be inserting the largest element in the heap. Since we start percolating from the leaf nodes, this would take at worst O(logn) time

- deletemin(): in the worst case, we would always have an O(1) time since that element is the root, however, the "rebalancing" or percolation could take on the order of O(logn)

# Exercise 2
binary search trees can be prevented from degenerating through the use of a balancing algorithm. This ensures that the tree is kept complete when an inserted node may cause an unbalanced configuration. Binary heaps don't have this issue though, by their design they always force new nodes as left as possible creating as balanced structure since it will always fill a level first before going down. 

# Exercise 3
using dijkstras algorithm would be an effective methods to do this. We first would mark all nodes as unvisited and give them a tentative path cost of +infinity and the strating node path cost as 0. We then find all neighbors of the start node and compare the current tentative cost to the real one, swapping if real is lesser. When moving on to the next seires of neighbors, we add the previous path cost to that point with that of the neighbor. if a node is connected by paths consisting of different neighbors, the algorithm would set the cost to reach that node when it discovers the cheaper of the paths from both neighbors. 

# Exercise 4
Is the sequence ⟨24,16,21,6,8,19,20,5,7,4⟩ a max-heap? Explain?

lchild = 2i+1
rchild = 2i+2
parent = (i-1)/2

the node 7 is in index(8) so its parent is min((8-1)/2) = index 3. the node at index 3 is 6 which is smaller than 7 and this violates the property that maxheaps must have parents greater than their children. 

# Exercise 5
Describe a linear-time algorithm MaxHeapVerify(A) that checks whether a given array A is a  max-heap. Analyze the running time. We must verify that all parent nodes are greater than the child nodes. 

when looking at a binary tree, there are (N+1)/2 parent nodes for N non-parent nodes. The algorithm must then traverse each parent node and determine if the children are less (for the max heap). This requires traversing all (N+1)/2 nodes 
$$O((N+1)/2) = O(N)$$


# Exercise 6
![[Scanned Document 3.pdf]]