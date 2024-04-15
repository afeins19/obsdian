# Values 
- integer 
- bools - true, false 
- closures - $\lambda x.E$ 

# Expressions 
- numE
- boolE
- lambdaE 

# Types 
now we introduce types into our language 
- numT
- boolT 
- lamT (interesting stuff happens here) 

# Notation 
$\vdash e: \tau$  => expression e has type tau 

$\vdash n: Num$ 
$\vdash s: str$ 

### Example Proof 
**if** $\vdash e_1 : Num$ and $\vdash e_2 : Num$ **Then** $\vdash (+ \;e_1, e_2) : Num$ 

so if e1 and e2 are num types then the operation (+ e1, e2) is also Num type 

# Conditionals 
```
if C T E
```
we have: 
- $\vdash C : Bool$
- $T : \tau_1$ 
- $E : \tau_2$ 

so our output is guaranteed to be in $\tau_1 \cup \tau_2$ 
but for a strictly typed language: $\tau_1 \equiv \tau_2$ (well use this one)

for a strict language we can make the following proof 
if $\vdash c:bool, \vdash (TE): U$ (where $U \equiv 'a$)
then we can say that the entire if statement must output a result of type U 
