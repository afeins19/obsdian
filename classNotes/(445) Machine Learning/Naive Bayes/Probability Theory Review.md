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

# Bayes Rule
![[Screen Shot 2024-02-16 at 1.34.32 PM.png]]
- since we dont know P(W), we can instead use total probability to find alll scenarios for wet in the sample space

$$P(R|W)=\frac{P(WR)}{P(W|R)P(R)+P(W|\neg R)P(\neg R)}$$

# Posterior Probability
![[Screen Shot 2024-02-16 at 1.38.16 PM.png]]
- we combine likelihood of some event occurring given the probability of the prior event occurring that it depends on 

# Maximum Aposteriori Estimation (MAP)
This states that the best hypothesis for some space H given observed training data D is given by

$$H_{MAP} = argmax_hP(H|D) = argmax_H\frac{P(D|H)P(H)}{P(D)} = argmax_HP(D|H)P(H)$$

note that we drop the denominator P(D). We do this because for each element $H_i$ it is already given that D occurred so D is constant for all  elements in H. 

### Equal Priori Probability 
![[Screen Shot 2024-02-16 at 1.58.18 PM.png]]
with the condition that all sub events in H are the same, the priori probability is equal to the maximum likelyhood hypothesis 

