# reversi game 

- minimax algorithm
	- plays until end state is reached with optimum moves or a specified depth
	- once end is reached, score is checked. your score is subtracted from the AIs score and play fitness is calculated
- 
![[Screen Shot 2023-12-05 at 12.20.28 PM.png]]
- certain moves are legal
- you can consume pieces in a linear fashion 


# psu parking navigator

- finding parking 
- woodland lot is mapped using dijkstras 
- finds the closest available spot
- at each intersection for each row, find the closest spot to that intersection point![[Screen Shot 2023-12-05 at 12.27.33 PM.png]]

## 20 Questions

- uses nlp to accurately guess 
- animal theme is currently being used 
- csv to hold animals and animal attributes
- alogirthm generates probabilities for possible animals and narrows search as game progresses
- at this stage game only narrows down to a set of animals
- attributes are predefined 
  (lays eggs or not, mamal or not, etc.)