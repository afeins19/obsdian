### Functions 
```haskell 
(define (merge [op: (Number Number -> Boolean)]))
			   [int-list1 : (Listof Number)]
			   [int-list2 : (Listof Number)]) : (ListOf Number)
```
- op: (Number Number -> Boolean) defining an operator which works on 2 numbers and returns a boolean
- this function overall returns a (ListOf Number)
- **there must be whitespace around the colon** 