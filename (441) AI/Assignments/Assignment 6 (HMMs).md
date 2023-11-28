# Problem 1 
**Assume an HMM with two hidden states, Hot and Cold. What's the most probable weather  
sequence for observation sequence (1,2)?  

Hot -> Cold: 0.3, Hot -> Hot: 0.7, Cold ->Cold: 0.4, Cold -> Hot: 0.6, Start -> Cold: 0.3, Start -> Hot:**

![[Scanned Document 2.pdf]]
(using viterbi algorithm)
# Problem 2
**Write short notes on Baum-Welch algorithm?**

The Baum - Welch algorithm was designed to optimize the values for transition probabilities, hidden states, and initial states are not known or are inaccuratly define. It follows a two step process called the EM process

the algorithm first accepts some observation sequence. 

Step E: in this first step, the algorithm finds the number of occurances for each transition and emision for that observation sequence and forms expectation values based on this information

Step M: the HMMs values are updated based on these expectations 

the hmm probability values are continously refined 

# Problem 3
**What are the Limitations of HMM?**

The limitation of HMMs lies in their simplicity. They model probabilities of event sequences with the i-th occurrence only depending on the (i-1)th occurrence. if there is a relationship that depends on some complex long-term patterns in the sequence, hmms are not adept at capturing these.

Another factor is that HMMs assume that the system as a whole does not change. It does not account for systems where the probabilities may change as a given sequence is followed. 


# Problem 4
**Given a set of state s and a set of observable symbols, describe the various sets of numbers needed  
to completely define a Hidden Markov Model**

Parameters:
- S - the set of hidden states 
- V - the set of observations 
- A - the transition probability matrix (holds probabilities for transitioning from one state to another)
- B - the emission probability matrix (holds the values for emissions for a being in particular state)
- π - the initial state vector which maps a probability value for starting at some state in S 
- O - the observation sequence which is some tuple of N-observations 

# Problem 5
**Given an observation sequence and an HMM, what exactly does the Forward algorithm compute?**

the forward algorithm is basically the opposite of the way we used HMMs in class. The Algorithm gives the likelihood of the given observation sequence occurring within some HMM. The observation sequence is followed from observation-1 to observation-n thus its name. This algorithm follows all possible paths through the HMM.


# Problem 6
**Given an observation sequence and an HMM, what does the Viterbi algorithm compute?**

the Viterbi Algorithm finds the most likely sequence of states that were traversed given some observation sequence. starting from the end, It only selects the most probable transition at each step and back tracks to the previous state via that transition. 

# Problem 7
**Can HMM be used for solving temporal probabilistic reasoning? Explain your reasoning?**

Yes, HMMs are built to work with a sequence of events and probabilities for those events. This captures the notion of temporal reasoning as the observations follow some sequence. The drawbacks for using HMMs for temporal probabilisitic reasoning are the same as the drawbacks of HMMs in general, namely that they cant model long term sequential relationships. 

Transition probabilities represent the probability of moving from one state to the next in the sequence and emissions represent the likelyhood that a particular observation implies a corresponding state change. 

# Problem 8
**‘HMM is widely used for prediction’. Justify this statement with a real time example. With a neat  
sketch, show how HMM can be employed to provide a solution. Show all the steps necessary to  
model the problem using HMM**

HMMs have great utility in, for example, the healthcare sector. An HMM might be used to fine-tune a patients treatment plan for a particular diagnosis. States might correspond to a stage of disease progression such as the standardized group of cancer stages (0-4). An hmm might be trained on a data set of patients symptoms and a known cancer stage value for each patient. From there it will tune its emission matrix to for each symptom. 

From this point, the HMM might be used to predict the next severity rating based on current symptoms and help doctors in planning a more accurate treatment approach for this patient. 

# Problem 9 

**What could be the hidden states in HMM model used for speech recognition?**

**States**: states model the most basic components of speech called phonemes. These are the most "basic" sounds that all speech can be broken down into

**Transitions**: transitions correspond to the probability of going from one phoneme to another 

**Observations**: some sequence of data from an audio signal that will be related through some probabilities to some set of states 

The states of the HMM will correspond to the phoneme building blocks for words and when a sequence of observation is read, it will be mapped to the most likely sequence of transitions from phoneme to phoneme.  This  set of state transitions will hopefully map to written text which accurately represents the speech signal. 