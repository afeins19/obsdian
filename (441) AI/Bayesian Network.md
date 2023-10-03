	for some probabilities, we depend on the outcomes of previous events. (Conditional Probability)
- Encodes conditional independence between variables  in a graph


_Bayesian Probability_: represents a degree of belief in an event 

_Classical Probability_: represents the actual probability of an observed behavior

# Naive Bayes Model
$$ P(C|Y_1,...Y_n) = P(Y_i|C)$$
- events in Y are disjoint (independent)
- Conditional probabilities P(Y|C) can easily be estimated from labeled data 

## Independence
for independent events, the chain of their probabilities is
$$P(C_1,...,C_n) = \Pi\: P(c_i)$$

## Conditional Independence
holds if any of the following properties are  satisfied
$$ P(A,B | C) = P(A|C) P(B|C)$$

$$P(A|B,C) = P(A|C)$$
$$P(B | A,C) = P(B|C)$$

## Graph of Baysian Network
![[Screen Shot 2023-09-26 at 12.32.55 PM.png]]

## Some Calculations 
![[Screen Shot 2023-09-26 at 12.33.11 PM.png]]

## Markov Dependence
A -> B -> C
$$P(A,B,C)=P(C|B)P(B|A)P(A)$$

## For chains of dependence
$$P(x_1,...,x_n) = \Pi \: P(x_i|parents(X_i))$$
