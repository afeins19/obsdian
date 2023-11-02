# Assumptions
- markov states that future states depend only upon the current state (not on previous states)
- Total possibilities must sum to 1 

# Example Problem
![[Screen Shot 2023-10-26 at 1.55.53 PM.png]]

![[Screen Shot 2023-10-26 at 1.56.29 PM.png]]

## Assumptions 
![[Screen Shot 2023-10-26 at 1.56.58 PM.png]]

![[Screen Shot 2023-10-26 at 1.57.20 PM.png]]- sum of all transitions from current to next state must be 1 

![[Screen Shot 2023-10-26 at 1.58.22 PM.png]]

# Hidden Markov Models
- predicting weather based on todays **observations** (not states themselves)
- can we predict the next state using reported observations?
- can we predict the state sequence using these reported observations too?
- **YES**

![[Screen Shot 2023-10-26 at 2.02.17 PM.png]]

![[Screen Shot 2023-10-26 at 2.02.38 PM.png]]

## Definitions

