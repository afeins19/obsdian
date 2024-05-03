# Variables

```
var x : int = 5 
var y : float = 2.0 
var z : str = "hello"
```
- values assigned to variables must match the declared type 
### Possible types you can Declare Variables with  
- int
- float
- str 
# Functions 
functions will always require a return type. Each parameter that is passed into the function in its definition also requires a type:

```
def add(x : int, y : int) : int
	return x + y
end 
```
### Possible Function Return Types 
- int 
- float
- str
- void 

### Return types must match value
when a function returns a value, this value must match the type declared in the function definition. 

### Void Return Type 
functions which do not have a return value must use the 'void' keyword. Functions declared with a void return type may not have 'return' keyword in their body:
```
def doNothing() : void
	print("i do nothing...")
end 
```

# Loops

### For Loop
```
for i=0 to 5 then 
print(i)
```

**Output**
```
0
1
2
3
4
```

### While Loops 
below is an example of a while loop that terminates after the iterator reaches a certain value: 
```
# declaring the iterator 
var i : int = 0

# loop declaration 
while i < 5 then 
	var i : int = i + 1
end 
```

**output**
```
[1,2,3,4,5]
```

# Conditionals 

### if 
```
if <condition> then 
	<expression> 
end 
```

# Errors

### TypeMisMatchError 
this error is thrown in the following cases
- value type doesn't match variable that its assigned to 
- variable is assigned a function call that returns a non-matching type 
- function returns a type different than the one defined in its declaration 
- function receives a parameter with a type that does not match the corresponding parameter in the function definition

### IllegalOperationError 
this error is thrown when binary operations on numerical and non-numerical variable types are attempted 

### RuntimeError 
this error is thrown then the program detects an illegal operation or state during run time. 
- division by zero
- use of an undefined variable 

### InvalidSyntaxError 
this error is thrown when an expression is typed with incorrect syntax 
