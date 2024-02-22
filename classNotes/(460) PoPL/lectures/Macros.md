--> on test <-- 
# While Loops 

### Python
```python 
x=0 

while x<10:
	x+=1 
```


```scheme
(while cnd 
	   body)
```
- body will be a recursive call back to while with some modification to the condition 

# Strict-if
```scheme
(define (strict-if C T E)
  (if (boolean? C)
	  (if C T E
	  (error 'strict-if "not a bool"))
	  )
  )
```

### Macro to realize the strict if 
```scheme

(define-syntax strict-if2
  (syntax-rules ()
  [(strict-if2 C T E)
  ((if (boolean? C)
	  (if C T E)
	  (error 'strict-if "not a bool")))]))
```

# Let Macro
```scheme 
(define-syntax my-llet 
  (syntax-rules () 
  [(my-let ([var val] ...) body)
  ((lambda(var ...) body) val ...)])) 
```

### How does this work? 
```scheme
((lambda (s) b ) v)
((lambda (x) x ) 2)
```
