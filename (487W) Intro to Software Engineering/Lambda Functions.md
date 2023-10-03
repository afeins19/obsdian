
```python

def binaryGate(a,b, strategy)
	return strategy(a,b)

andStrat = lambda x,y: x and y 

andGate = lambda x,y: binaryGate(x,y andStrat)

>> andgate(1,1) 
1 
```