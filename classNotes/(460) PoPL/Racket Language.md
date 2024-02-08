	based on LISP (list Processing) language. Conceptually, we pass a list of items to some function. 
# Syntax 

### Pre-fix 
racket is prefixed language (we put the operator first)
	1 + 2 => (+ 1 2)
	example: (* (+ 2 3) (- 3 4)) ... evaluates to -5 

### Assignment 
```haskell
(define x 3)

(define y (+ x 1)) 
```
x = 3 and y = x + 1 

# Functions 
```haskell
(define (sqr x)
		  (* x x) )


(define (inc value)
	(+ value 1))
```

example of a procedure definition. Following the "define" keyword, we give a function name along with parameters, we then write the function. Note that racket is functional so it would just return the last line in function definition. 

# Symbols/Tokens 
	'mySymbol 
we can do symbolic programming in racket. To define a symbol we first do a tick mark. 

# Comparison   
```haskell
(= 1 2) 

(> 1 2)
```

### Non-Numerical Comparison 
```lisp 
(equal? 'nate 'nate)
```

# Conditional Expressions 
```haskell 
;; defining our incrementor function 
(define (inc value)
  (+ value 1))

;; does 1 = inc(0)? (yes)
(if (= 1 (inc 0))
    #t
    #f)

;; function that uses a conditional 
(define (abs x)
  (cond
    [(> x 0) x]
    [(= x 0) "bruh"]
    [else (- x)]))
```
### Cond keyword 
	this allows us to define a series of new conditional expressions an each new line within a (cond) parenthesis block. 
# Recursion 
	demonstrating with the factorial function 
```haskell
(define (fact n)
  (cond
    [(= n 0) 1]
    [(= n 1) 1]
    [else (* n (fact (- n 1)))]))
```

# S-Expression 
	s-exp 
### Example of S-Expression 
```Haskell 
`(+ ,(number -> s-exp (+ 1 2)) 3)
```