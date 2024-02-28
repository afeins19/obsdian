```python
class Box:
	def __init__(self, val):
		self.__value = val
```
This will be a "one parameter" object. 

### What we need to implement 
```
Exp | boxE [arg : Exp]
	| unboxE [arg : Exp]
	| setboxE [b : Exp] [v : Exp]
	| seqE [b1 : Exp] [b2 : Exp]
```

### Tests
```scheme 
(let ([b0 (box 0)] [b1 (box 1)]))
	(let [(1 (list b0 bb1))])
		(begin 
			(set-box! (first lst) 1)
			(set-box! (second lst) 2) 1))) 

=> '((box 1) (box 2))
```

# Using Boxes to make Objects 
```scheme 
(define counter 
	(let [(n (box 0)])
		(lambda() (begin
			(set-box! n (+ 1 (unbox n)))
			(unbox n))))
```
closure over the counter of n , n is a pointer to that location and n was mutated. 

# Aliasing 
we can use the trace tool on aliased values to follow it through mutations 