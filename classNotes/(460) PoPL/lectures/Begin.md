```scheme 
(begin  1
		2
		3
		4
		5)
```

### New Expression
- begin is a new expression that takes a list of expressions
```scheme 
beginE (bs: (Listof Exp)) 
```

### Parser 
```scheme 
(begin ANY ANY)
(cons (second s) (map parse rest))
```



