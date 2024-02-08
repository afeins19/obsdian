# Subst 
The function replaces all elements the expression passed in with the passed in values. subst(what, for , in)
```scheme 
(define (subst [what : Exp] [for : Symbol] [in : Exp])
  (type-case Exp in
    [(numE n) in]
    [(idE s) (if (eq? for s)
                 what
                 in)]
    [(plusE l r) (plusE (subst what for l)
                        (subst what for r))]
    [(multE l r) (multE (subst what for l)
                        (subst what for r))]
    [(appE s arg) (appE s (subst what for arg))]
    [(maxE l r) (maxE (subst what for l)
                        (subst what for r))] 
    ))

#|
	8 x (+ x x) => (+ 8 8)
|#
```

### Helper function to map values 

```scheme 
(define (helper [alst : (Listof Number)] [bls : (Listof Number)]) : Boolean
  <check all conditions of list a,b being empty or not>
  <else if both not empty -> recurse> 
  
  )


```

### Making Subst accept multiple arguments
say we want to replace x, y with 8,9. 

**if we have '(8 9) '(x y) with exp '(+ x y) -> (+ 8 9)**

breaking this down we get 
```scheme
'(8 9) ;; Listof numE
'(x y) ;; Listof idE 
'(+ x y) ;; Exp 
'(+ 8 9) ;; the return we want 
```


# fun-def function 
needs to be changed to accept a list of symbols under an arg parameter to now acomodate the new subst and others 

# appE
like fundef, appE needs to be changed to accept a list of arguments too. 