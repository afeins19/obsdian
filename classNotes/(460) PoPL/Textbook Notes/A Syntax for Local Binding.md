# BNF for Expressions 
expressions defined here are **abstract** - they must actually be evaluated later! 
```
<expr> ::= <num>  
| {+ <expr> <expr>}  
| {let1 {<var> <expr>} <expr>}  
| <var>
```
this syntax lets us do the following 
- define a terminal plus expression
	- with non-terminal expression operands 
- define a terminal let expression 
	- with non-terminal variable statements 
	- non-terminal expression statements 
	- and a a non-terminal body statement 

# Local Binding 
```haskell 
{let1 {x 1}  
	{+ {let1 {x 2} x}  
	x}}
```
the above program demonstrates the concept of local binding. The inner definition of x (x=2) shadows the outer definition of x (x=1). Importantly, the inner x is not a modification of the outer x but is in fact a **new definition**. A variables binding is determined by its position within the program. 


# Static Scoping 
static scoping is the idea that variables should have a concrete binding at all times, their binding should not be dependent on the programs control flow or some other non-deterministic outcome. For example: 
```haskell 
{let1 {x 1}  
	{+ {if {moon-is-currently-full}  
		4  
		{let1 {x 2} x}}  
	x}}
```
in this example, depending on an external event, the program might evaluate to one of two different values! This is called **Dynamic Scoping** and it is the **unambiguously wrong design choice**. 

# Extending the Evaluator to handle Local Binding (let1E)
```haskell 
(define-type Exp  
	[numE (n : Number)]  
	[plusE (left : Exp) (right : Exp)]  
	[varE (name : Symbol)]  

-- new letE definition 
	[let1E (var : Symbol)  
		(value : Exp)  
		(body : Exp)])
```

# Environment 
the crucial feature which makes local binding possible is substitution. Instead of constantly rewriting variable bindings (a process that grows ~$O(n)$ with the program for every variable binding), we can do a space-time tradeoff to save time - we do this by implementing a **cache**. This specific cache is a data structure called the **environment**. We define the environment in the following way: 
```haskell 
(define-type-alias Env (Hashof Symbol Value))  
(define mt-env (hash empty)) -- "empty environment"
```
note that we'll also need to modify the interpreter to take in the environment as a formal parameter. Whenever a variable is encountered in the program, we try to find its binding in the environment - such a binding may or may not exist. 

# Lookup Function
we can define a helper function to perform the actual task of querying the environment 
```haskell 
(define (lookup (s : Symbol) (n : Env))  
	(type-case (Optionof Value) (hash-ref n s)  
		[(none) (error s "not bound")]  
		[(some v) v]))
```
if a value is found, we return it wrapped in a some type - this provides a clean way of returning the binding without having to worry about its type. 

calls to lookup() will always have the following clean and readable form: 
```haskell 
[(varE s) (lookup s nv)]
```
# Handling Let1E Expressions 
In order to handle let1E expressions, we need to evaluate the body of the expression with...
- the extended environment 
- a new name
- a new bound value 

# Extending the Environment 
to extend the environment, we define a function - extend() to perform the task of adding our new binding definition to our environment 
```haskell 
(extend : (Env Symbol Value -> Env))  
(define (extend old-env new-name value)  
	(hash-set old-env new-name value)))
```
# Implementing This Into the Interpreter 
now we have all the building blocks we need for the interpreter to actually perform the local bindings: 
```Haskell 
(define (interp e nv)  
	(type-case Exp e  
		[(numE n) n]  
		[(varE s) (lookup s nv)]  
		[(plusE l r) (+ (interp l nv) (interp r nv))]  
		[(let1E var val body)  
			(let ([new-env (extend nv  
								   var  
								   (interp val nv))])  
			(interp body new-env))]))
```

### Exercise:  
-  **What if we had not called (interp val nv) above?**   
		if we didnt call (interp val nv), then the val that we will be binding might not be reduced to its terminal form. This means that well store the raw  value of the val and it will need to be interped later at some point -> inefficient 
		
-  **What if we’d used nv instead of new-env in the call to interp?}**  
		if we used nv, then we wouldn't have the most up to date environment. This might either lead to an incorrect binding for a variable or a free-variable error 
		
-  **Are there any other errors in the interpreter based on copying what we had before?**  
		we need the other functions to handle the environment and possible perform lookups to get the operands they need? 
		
-  **We seem to extend the environment but never remove anything from it. Is that  okay? If not, it should cause an error. What program would demonstrate this  error, and does it actually do so? (If not, why not?)** 
		this wont be an issue, this is because the new binding only exists in a new data structure instance of the env thats extended by the new binding. Once that recursive call is handled, that environment is discarded (usually by built in garbage collection). 

