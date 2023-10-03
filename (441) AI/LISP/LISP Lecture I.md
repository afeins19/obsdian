- (1958) Second oldest programming language
- Lisp => portmanteau of list processing 

# Why LISP
- good for writing production software
- write new programs and extend old programs 
- build-in support for list (everything is a list)
- automatic storage and memory allocation
- interactive  environment which allows programs  to be developed step by step 

# Symbolic Expression
- s - expressions are composed of 3 valid objects 
```LISP
interpreted code:
> (+ 7 9 11) 
> 27

compiled code
> (write (+ 7 9 11))
> 27 
```

#  Lists
- a sequence of atoms or other lists separated by blanks and enclosed in parentheses 
```LISP
data:
(list 1 2 3); 
```

# Functions 
```LISP
Functions:
(defun average(x,y)) (/ (x+y) 2)

(write average(5,5))
> 5
```

##  Common Functions

### car() - returns first element in list
```LISP
(car (1 2 3))
> 1
```
### cdr() - returns everything but first element in list
```LISP
(cdr (1 2 3))
> 2 3
```
### Qoute()
 qoute() - returns the unevaluated expression passed in
```lisp
> (qoute (+ 1 2 3))
> (+ 1 2 3)
```
### length()
```lisp
(list-length '(1 2 3)))
> 3
```

### filter()
```lisp
(filter #'(lambda (x) (evenp x)) `(1 2 3 4)))
```


