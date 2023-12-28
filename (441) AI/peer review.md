# reversi game 

## Understanding 
a turn based game where players compete to have the most amount of their pieces on the board. Players can turn opponents pieces into their own color by blocking a horrizontal, verticle, or diagonal chain of pieces with their own color. 
The game will use minimax for move selection 

## Comments 
seems like a great idea. Minimax might get a little inefficient with all the possible moves especially for a game with such a large number of moves to be made. Consider using Alpha Beta pruning.

## Recommendations 
try using alpha-beta pruning to cut down on bad moves

- minimax algorithm
	- plays until end state is reached with optimum moves or a specified depth
	- once end is reached, score is checked. your score is subtracted from the AIs score and play fitness is calculated
- 
![[Screen Shot 2023-12-05 at 12.20.28 PM.png]]

# psu parking navigator

## understanding 
this app will guide users to an available parking spot in the woodland lot. The parking lot will be modeled by a graph and a traversal will find the next open spot

## Comments
really solid idea. I would personally love to see something like this up and running. 

## Recommendations
consider trying to generalize the graph to any parking lot if possile. It might be possible to model those "sections" or rows of the parking lot generally so you could extend your program to other lots on campus

![[Screen Shot 2023-12-05 at 12.27.33 PM.png]]

## 20 Questions

- uses nlp to accurately guess 
- animal theme is currently being used 
- csv to hold animals and animal attributes
- alogirthm generates probabilities for possible animals and narrows search as game progresses
- at this stage game only narrows down to a set of animals
- attributes are predefined 
  (lays eggs or not, mamal or not, etc.)

## Understanding 
will use nlp to guess the game that the person is playing. Currently an animal theme to cut down the search space a little bit. There is an algorithm that will narrow down the animal by asking questions about attributes, narrowing down the search space further each time. 

## Comments
seems like a great idea. Were using nlp for our project too and it might be a bit difficult to kind of set up a neural network for this specific thing, i dont know the nlp approach that would be used though 

## Recomendations
if nlp works well thats great, otherwise consider using a search algorithm like a tree traversal. 