# Example: Dice 
the basic example involves rolling a pair of dice 
- **trial** - an experiment 
- **outcome** - an ordered pair of numbers representing the dice values for each trial 
- **Sample space** - the set of all possible outcomes in some experiment given by $\Omega$
- **Event** - any subset of the sample space 

# Probability Distribution
a mapping between the set of all events and the set of real numbers $\mathbb{R}$. It may be a function if the probability of some event t maps to one and only one value every event. 

# Random Variable 
a variable whose possible values are numerical outcomes of a random phenomenon
- intuitively it is an outcome of a random phenomenon

# Joint Probability 
for events A and B, joint probability P(AB) stands for the probability that both events happen 

# Conditional Probability 
with joint probability, we can now extend it to conditional probabilities the probability of some event A occurring given that some event B has occurred 
$$P(A|B) = \frac{P(AB)}{P(B)}$$
# Independence 
two events A,B are independent if 
$$P(AB) = P(A)P(B)$$

# Prior Probability
the probability that a proposition is true before any other facts or evidence is obtained (the probability of the event just by itself)

# Posterior probability 
the probability of some event occurring given some piece of evidence. P(A|B). 

# Law of Total Probability 
if A_i is mutually exclusive then the probability over all partitions A_i comprise the entire sample space and sum to 1. We then calculate the probability of B occurring in each probability given A_i, we then sum those. 
$$P(B) = \sum_{i=1}^nP(B|A_i)P(A_i)$$
