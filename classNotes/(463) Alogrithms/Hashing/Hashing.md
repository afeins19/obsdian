a technique that retrieves the value using the index obtained from the key without performing a search. 
### Hash Table
a data structure that can be searched and deleted in O(1) time. A hash table (map, dictionary are also names) is a data structure that stores values as a list and uses the key to access the index of the function.

the idea is to create a mapping where the key and the value both map to the same index. 
# Modulo Technique 
for a list of size n, we can take our element with value e and do $h(e) = e\; mod\; m$ where h(e) gives us a unique index for the items. However, we may get collisions if h(e) returns the same value for a different input - this is a collision. 

# Folding Method
divides the item into equal-size pieces (the last piece may not be of equal size). These pieces are then added together to give the resulting hash value. The items are then modded with the size of the value -> social security number -> add them together -> mod by length of the number 

# Mid-Square Method
first square the item, then extract some portion of the resulting digits and then do modulus on the middle values. This reduces the amount of collisions. 

# Perfect Hash Function
a hash function that maps each search key to a different index in the hash table is called a perfect hash function. Given an arbitrary collection of items, there is no systematic way to construct a perfect has function. One way to get a perfect hash function is to simply increase the size of the hash table so that each possible value in the item range can be accommodated. 

# Collision Resolution 
a collision occurs when two keys are mapped to the same index in a hash table 

## Open addressing 
the process of looking for another slot after a collision this may be done with the following methods: 
### linear probing 
moving to the next available unit linearly from the collision index. Linear probing garuntes that an available cell can be found for insertion as long as the table is not full. However, there is no such guarantee for quadratic probing 

### Quadratic Probing
newhashvalue = rehash(holdhashvalue)

where rehash(pos) = (h+i^2) % tableSize 
h is the first slot 
do this for i > 0 
1. pos = 1^2=1
2. pos = 2^2=4
3. pos = 3^3 = 9 ...

# Separate Chaining 
places alll entries with the same hash index into the same location rather than finding new locations. Each location in the chaining scheme is called a bucket  -> a container that hollds multiple entries. We can then perform a linear search on the bucket. This is commonly done with a linked list 


# Load Factor and Rehashing 
the load factor $\lambda$ is a measure of how full the hash table is. If the load factor is exceeded, increase the hash table and reload entries into the new hash table - this is called rehashing. $$\lambda = \frac{n}{N}, \; 0<=\lambda<=1$$
where n is the number elements and N is the number of locations in the hash table. Practical studies show that for open addressing you want to have $\lambda < 0.5$ and for separate chaining you want $\lambda < 0.9$. 

# Map
a dictionary or a hash-table hashing is efficient implementation to realize a map. We can use: 
- Array-lists: O(n)
- AVL tree: O(logn)
- Hash Function: O(1) (in best case)

# Applications of Hash Tables
a network router is tasked with blocking data packets from certain IP addresses perhaps belonging to spammers. Every time a new data packet arrives, the router must look up whether the source ip address is in the blocklist, if it is then it drops the packet. We must quickly be able to make a determination since there are many packets being sent. 