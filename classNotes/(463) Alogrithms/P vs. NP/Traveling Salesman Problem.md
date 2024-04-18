![[Pasted image 20240418121908.png]]
if there is a salesman trying to visit every city, find the most efficient path for him to take (minimize). 
$$g(i,S) = min_{k \in S}(C_{ik} + g(k, S- \{k\}))$$

- g = cost function
- i = starting vertex
- k = current location
- s = remaining vertices 