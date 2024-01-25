# Declaring Langauge
```plait 
#lang plait 
```

# Primitives
- _Number:_ 1, 1.2, 3.14
- _Boolean:_ #t, #f 
- _String:_ "apple", "bananas, are cool"

# Symbol 
	some examples of symbols, declared with a tik-mark 
```haskel 
'apple

'b
```
- cannot have spaces between symbols 
# Functions 
	Plait uses parenthesized prefix notation: (<func> <arg1> <arg2> ...)

### Examples
##### Floor function 
```haskell 
(floor 1.2)
```
##### Max function
```Haskell
(Max 3 5)
```
##### Addition Function 
```Haskell
(+ 3 5)
```

##### string-append
```haskell
(string-append "apple" "banana")
```

##### string=? - comparing 2 strings 
```haskell
(string=? "apple" "Banana")
>> #f 
``` 

##### equal? - generic function that works on any type of object 
	note that we may only pass in values of the same type! 
```haskell 
(equal? 'a 'a)
>> #t

(equal? "apple" "banana")
>> #f
```

##### Generic (Just Function Name)
	simply writing the function name with no parameters gives the function description and its type - a procedure
```haskell
> max
- (Number Number -> Number)
#<procedure:+> 
```
##### equal? - just typing the function name
```haskell
> equal? 
- ('a 'a -> Boolean)
#<procedure:equal?> 
```
- the 'a 'a  implies that the function select the type 

# Lists 
	lists will create lists of strings, numbers, booleans. Note that lists must contain objects of the same type!  
```haskell 
> (list 1 2 3)
- (ListOf Number)
`(1 2 3)
```
### List Functions 
- _first_: returns the first item in the list 
- _second_: returns second item in the list 
- _rest:_ returns everything but the first item in the list
- _empty?:_ returns a boolean of whether or not the list is empty 
- _cons?:_ returns a boolean of whether or not the list was made with cons

### Cons
	takes in a value and a list of the same type and CONSTRUCTS a NEW list with those values 
```Haskell
> (cons 1 `(2 3 4 5))
- (ListOf Number)
`(1 2 3 4 5)
```

# Conditionals 
### if statement
	observe the structure of this statement. If is a syntactic form that always has 3 expressions inside of it.
```haskell 
(if (empty? `())
	`none 
	`some
	)
```
- `none - if the expression evalutes to true (which it will because the empty list is indeed empty lol)
- `some is the else statement basically 

### cond statement 
	essentially a generalized if statement. in the brackets (which are there by convention) we write the conditional expression, then the task to perform if it evalueates to true.  
```haskell 
(cond
	[<condition> <expression>]
	[<condition> <expression>]
)
```

##### Example
```haskell 
(cond
	[(empty? `()) `none]
	[(cons? `()) `some]
)
```

# Definitions 
	how we assign values to variabbles in plait
```haskell
(define pi 3.14) ;;pi=3.14
(define two (+ 1 1)) ;;two=2
```
- we can now use these as a "variables"


### Defining Functions 
```haskell 
(define (<func_name> [<arg1> : <Type1>]) : <ReturnType> 
	(stuff)
)
```
##### Example: area of a circle 
	note that we can also explicitely declare types. 
```haskell 
(define (area [r : Number]) : Number
	(* pi (* r r))
) 
```

### Defining other kinds of data 

##### Defining lists 
```haskell 
(define grocerices `("apple" "banana" "coconut" "gummy"))
```
##### recursively checking for an item in the list
```haskell 
(define got-milk? [lst : (ListOf String)] : Boolean
	(cond
		[empty? #f]
		[(cons? lst)
			(or (string=? (first lst) "milk")
			(got-milk? (rest lst))
		]
	)
)
```
what if we'd like to check for a few different kinds of dairy items being present in our list. We could of add another check (string=? (first lst) "butter") or (string=? (first lst) "cheese") etc. However we can apply some local bindings to locally define the item we are checking for. 


### Local Definitions 
```haskell
(define got-milk? [lst : (ListOf String)] : Boolean
	(cond
		[empty? #f]
		[(cons? lst)
		 (local [(define item (first lst))]
			(or (string=? item "milk")
				(string=? item "butter")
				(string=? item "cheese")
			(got-milk? (rest lst))))
		]
	)
)
```

### Defining Types 
suppose we'd like to write programs that deal with animals. we can do this just by using lists but that would be clunky and difficult to wield 

The OOP analog is to think of Animal as an interface. Tiger and snake are two classes are classes which implement the Animal interface. 

```haskell 
(define-type Animal
	 (tiger [color : Symbol]
		    [stripe-count : Number]) 
	 (snake [color : Symbol]
			[weight : Number] 
			[food : String])
)
```
- define type allows us to create our own types
- each sub expression under define-type is called a **Variant**
- each **Variant** has some fields with a name and a type 
##### Creating instance of types 
```haskell 
(tiger `orange 12)
(snake `green 5 "gummy bears")
```

##### getting fields from variants 
we can type variant-field to get the specific field of the instance of our variant for our type. 
```haskell 
> (tiger `orange 12)
> (tiger-color (tiger `orange 12))
- Symbol 
`orange 
```
# type-case 
we can define functions that dispatch based on the type of variant thats passed in. For example, say we'd like to write a function that will extract the color of the *Animal* passed into it. Assume that we've already defined the *Animal* type and variants *tiger* and *snake*. 

### type-case example: animal-color
we could have done the same thing using a cond statement but that would require explicitely getting the field names from each type of variant. Type-cases allow us to define the syntax pattern of our type and go from there. 

note that, again alagos to interfaces in Java. We have to define our type case for all variants of that type.
	
```haskell 
(define (animal-color a)
	(type-case Animal a
		[(tiger c sc) c]
		[(snake c w f) c]
	)
) 
```
# Testing 
suppose we want to define a function which checks whether or not an animal is dangerous. An animal is deemed dangerous if it is over 3 lbs. 
```haskell 
(define (animal-dangerous? a))
	(type-case Animal a
		[(tiger c sc) #t]
		[(snake c w f) (> w 3)])
	)
```
now that we've written our function, we can use the test case to test our function 
```haskell 
(test (animal-dangerous? (tiger `orange 12))
	#t)
```

### print-only-errors
plait will only print failed test cases in the CLI, you can define this globally in the program
```haskell 
(print-only-errors)
```

### Test Modules 
we can wrap our functions in a module+ test to have a collection of tests run together. Plait will run these tests at the end of the program so module+ definitions can be written **before** the function declaration if desired. 
##### module+
```haskell 
(module+ test
	(test (animal-dangerous? (tiger `orange 12))
		#t)
	(test (animal-dangerous? (tiger `white 2))
		#t)
)
```
### Syntactic Coverage
dr. racket can let us know if our test cases does not cover all of our code. For example, the above test module only covers tests for tiger variants, but does not cover any cases for snake variants. The snake variant defintion will be highlighted to show this. 

we can turn on this feature by going to preferences and turning on "syntactic test suite coverage"

