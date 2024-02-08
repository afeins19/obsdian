in the order of progression down to machine level code

example: say the programmer entered the following statement: 
```java
positions = initial + rate * 60;
```

# Lexical Analyzer
	accepts a charecter stream and serializes variables named by the programmer with some ID.

```
(id,1) (=) (id,2) (+) (id,3) (*) (60)
```

# Syntax Analyzer 
	looks at the statement as a whole and determines if it is valid or not. (is this a valid expression?). Everything is still a token at this point and is not typed. 

# Semantic Analyzer 
	used to determine the type of the tokens and start doing the necessary operations to correctly covert the values into their correct types. 
```
example: 
(id,1) (=) (id,2) (+) (id,3) (*) (60)

(60) => interfloat 
```
- intermediate float generation 

# Intermediate Code Generator 
	an internal simpliefied rpresentation of the code given by the programmer. Each operation is given on a new line 
```
t1 = interfloat(60)
t2 = id3 * t1
t3 = id2 + t2
id1 = t3
```

# Code Optimizer 
	after simplification, we try to optimize the code into the most efficient operations 
```
t1 = id3 * 60.0 
id1 = id2 + t1

```
- *note: 60 has been converted to a float*
- we use less instructions and registers, note that t2 and t3 is skipped and we go right to id1

# Code Generator
	converts the final optimized expression into asssembly language. 
```Assembly  
LDF R2, id3
MULT R2, R2, # 60.0
LDF R1, id2,
ADDF R1, R1, R2
STF id1, R1 
```