The with keyword behaves in the following way:
```
{with {x 5} {+ x 3}}
```
this means that we apply the function `{+ x 3}` to a variable x immediately following its definition `{x 5}`. The important thing to note here is that this function is anonymous, so in mathematical notation we can write this in the following way: 
$$(λ (x)x + 3)(5)$$
## 6.1 - A Taxonomy of Functions 
there are two important things to keep note of for the with keyword: 
1. the ability to create anonymous functions 
2. the ability to define functions anywhere in the program 

### First Order Functions 
These functions are not values in the language. They can only be defined in a designated portion of the program where they **must be given names** for use in the remainder of the program 

### Higher Order Functions 
these functions can return other functions as values 

### First Class Functions 
These functions are **values with all the rights of other values**. These functions themselves can be supplied as the arguments to other functions, returned by other functions as answers, or be stored in data structures. 

## (6.2) Enriching the Language with Functions 
below are some motivating examples of the behaviors we'd like to implement: 
```haskell 
{{fun (x) (+ x 4)} 
	5}
```
we define a function with no name and immediately apply it to 5. This function should return a 9. Another function that we define using hte `with` keyword is as follows: 
```haskell
{with {double {fun (x) {+ x x}}}
		{+ {double 10}
		   {double 5}}}
```
this program works in the following way:
1. we define a function and bind it to a variable double 
2. we apply it to values 10 and 5 and sum them => (double 10) = 20 and (double 5) = 10 
3. the values are then summed. 

note that this program **instantiates the formal parameter with different actual parameters**

### BNF of our new Expressions  
```
<FWAE> ::= <num>  
| {+ <FWAE> <FWAE>}  
| {with {<id> <FWAE>} <FWAE>}  
| <id>  
| {fun {<id>} <FWAE>}  
| {<FWAE> <FWAE>}
```
### Interp Definitions 
```
;; interp : FWAE → FWAE  
;; evaluates FWAE expressions by reducing them to their corresponding values  
;; return values are either num or fun  

(define (interp expr)  
	(type-case FWAE expr  
	[num (n) expr]  
	[add (l r) (add-numbers (interp l) (interp r))]  
	[with (bound-id named-expr bound-body)  
	(interp (subst bound-body  
	bound-id  
	(interp named-expr)))]  
	[id (v) (error ’interp ”free identifier”)]
``` 

