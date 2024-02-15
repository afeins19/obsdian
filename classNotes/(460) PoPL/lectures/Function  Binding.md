```python
def f(x):
	def g(y):
		return x > y
	return g

#[] 
g = f(7) 

#[x=7]
g(6) #[x=7, y=6] - environment

g = f(7) #[x=-1, y=17, x=7] - environment 
```


```scheme
(let ([y 4]))    ;;y<-4
	(let [(x 2)] ;; x<-2
		(unlet x ;; y<-4 (x is removed from the local env at that level)
			(+ y 3)) 
	
```
# Closure Value
- parameter
- body
- corresponding environment (At the time of invocation)





