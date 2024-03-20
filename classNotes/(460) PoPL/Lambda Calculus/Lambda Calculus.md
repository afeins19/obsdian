### Grammar 

$\lambda x.x$ the first x is the variable and the second variable is the body 

E::= var/func/applications
- var - name (x,y,f,g, etc.)
- functions - $\lambda var(s).E$
- applications - $(\lambda x.x)(\lambda x.x)$ applications of an expression to an expression 
- xy
- f(xy)(hy)

# Properties 

### Selection
$$
\lambda xy.x => \lambda x. \lambda y.x
\lambda xy.y => \lambda x. \lambda y.y
$$
### Application (self application)
$$
\lambda x.xx 
$$

$$
x(\lambda y.y)z 
$$
this means we apply the lambda function to x which then gets applied to z 

### Beta-reduction 
 $(\lambda x.E)f => [f/x]E$
we substitute f for x in E => just substitution 

another example: 
$(\lambda x. \lambda x. x) y => \lambda x.x = \lambda y.y => [y/x]\lambda x.x$ 

