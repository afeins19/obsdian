# Stable Matching Problem
	how can hospitals effectively match medical students to residency programs? Given a list of hospitals (H) and a list of medical students (S). How can we match Students to the optimum hospital where that particular match is better than all other matches (Its a huge investment for the hospital and student).

Students (in this example) select their top 3 choices of hospitals. 
### Stable Match 
	student s selects hospital h as their number 1 choice and hospital h selects student s as their primary choice. 

### Unstable Match 
	say student s1 selects hospitals h1, h2, h3 in this order and hospital h3 selects s2 s1 s3 in that order. The algorithm should always select the best possible choice for the hospital and student. In other words, any other choice for the student would be less desirable than the one the algorithm gives, even though the algorithm might not give each student their primary choice. 

the complexity of this algorithm comes from the fact that each hospital must rank each student to give a desirability value to each student. This task falls under the data preprocessing portion of the algorithm. 

### Example: Couple Matching Problem
	the algorithm is considered stable if each choice for any given person will always result in a less desirable or equal outcome.  
#### Perfect Matching 
- Monogamous 
#### Stability 
- no incentive for some pair of participants to undermine assignment by joint action 
in some matching M, an unmatched pain m-w is unstable if man m and woman w prefer each other to current partners which may result in eloping

#### Stable matching
- perfect matching with no unstable matching pairs 

#### Pseudocode

```python 
while (some man is free and hasnt proposed to every woman)
	select such a man m
	w = 1st woman on m's list to whom m has not yet proposed

	if (w is free)
		assign m and w to be engaged 

	else if (w prefers m to be her fiance over m')
		assign m and w to be angaged, let m' be free 

	else 
		w rejects m 
	```

# Proof of Correctness 
	observation 1: men propose to woemn in decreasing order of preference 
	observation 2: once a woman is matched, she never becomes unmatched; she only "trades up"

given the above observations, we make the following claim: 

### Claim 
the algorithm will terminate after at most n^2 iterations 

### Proof
let P(t) denote the set of pairs (m, w) such that m has proposed to w by  
the end of iteration t, we see that for all t, the size of P(t + 1) is strictly greater  
than the size of P(t). But there are only n^2 possible pairs of men and women  
in total, so the value of P(·) can increase at most n^2 times over the course of  
the algorithm. It follows that there can be at most n^2 iterations.

# Proof of Correctness: Perfection
	does this algorithm garuntee everyone is matched? 

### Claim
all men and women get matched 

### Proof by contradiction 
suppose for the sake of contradiction that Zeus is not matched upon termination, then there must be some woman that is not matched, then that implies that some woman, say amy, has not been matched. from our above observations, women will always accept an initial proposition. But at conclusion of the algorithm, Zuess must have proposed to everyone which contradictions the initial premise. 

# Proof of Correctness: Stability 
	garuntee no unstable pairs 

### Claim
no unstable pairs 

### Proof by contradiction 
suppose that A-Z is an unstable pair: each prefers each other to partners in a gale-shapley (GS) matching table S* 

**Case 1**: Z never proposed to A 
-> Z prefers his GS partner to A (he only proposed to more desirable partners)
-> A-Z is stable 

**Case 2:** Z proposed to A
-> A rejected Z (right now or later)
-> A perfers her GS partner to Z (woman would only trade up)
-> A-Z is stable 

as these are the only 2 cases, it must be that A-Z must be stable 