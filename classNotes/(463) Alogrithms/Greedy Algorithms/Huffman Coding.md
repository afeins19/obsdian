Definitions: 
- alphabet ($\sum$) a finite non-empty set of symbols 
	- a set of 64 symbols that includes all 26 letters (both upper and lower case) plus punctuation and some special characters 

- binary code of an alphabet is a way of writing each of its symbols as a distinct binary string 

Say we want to encode the message `Hello World`. We have the following chars with their frequencies 
- l 3
- o 2
- h 1
- e 1
- _ 1
- w 1
- r 1
- d 1
This alphabet contains 8 members so we need at minimum $2^3 = 8$ bits to represent all unique combinations. 

we can reduce this further by using variable length codes for each symbol of the alphabet. however, we run into the issue of sending messages that are difficult to decode: let A = 0, b=1, c=10. is the string "10"=c or "10" = ba? To remove this issue we need to ensure that the prefix of each character is different from that of the others. these are called **prefix-free** codes. 

# Optimal Prefix Codes Problem 
whats the mechanism for ensuring that we have the optimum scheme for prefixes that minimizes the average symbol length in bits.

### Huffman Tree Solution...


# Huffman's Greedy Algorithm 
continuously try to pair a set of symbols ordered by frequency. We will have (n-1) merges that will be performed on n leaf nodes (the symbols of the alphabet) 

# Time Complexity 
total: O(nlogn)