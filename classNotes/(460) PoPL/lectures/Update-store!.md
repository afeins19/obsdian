```scheme 
(list (cell location value)...) 
'((cell 1 1) (cell 2 2) (cell 3 3))

; adding new cell
+ new cell (cell 1 4)
; output (this is WRONG: we need the value at (cell 1 1) to be replaced with (cell 1 4)
'((cell 1 4) (cell 1 1) (cell 2 2) (cell 3 3)) 

;; -> we need to write a function that updates the store 
```

# Setbox psuedocode (to be changed)
"the box is the worlds crappiest object **instance**" 
```PSUEDOCODE 
(set-box! bx val
		  (with (bx-l) (bx-sto)) (interp bx env sto) 
		  (with val-l v-sto) (interp val env (bx-sto))) ;; final store state that we arrive at 
``` 

# Update-store! pseudocode 
```PSUEDOCODE 
(set-box! bx val
		  (with (bx-l) (bx-sto)) (interp bx env sto) 
		  (with val-l v-sto) (interp val env (bx-sto))
		  (update-store! bx-sto bx-l val-v)) ;; new addition! 
```


lets type-case over this 
```scheme
typecase (listof Storage) val-sto
	[(cons c rest)] ;; check if the cell location (c-l) and see if thats the one were updating 
	[(empty (cons (cell location value) empty))] ;; otherwise we didnt find it and just make a new cell and add it to the end of the list 
```


