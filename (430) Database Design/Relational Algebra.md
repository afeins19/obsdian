# What is Relational Algebra
- _variables_ in the case of database are relations in our database 
- _operations_ involve the cartesian product of the two relations 
- the _cartesian product_ is itself a relation 
							A x B = C
# Purpose
- formal foundation for relational model operations
- used as a basis for implementing and **optimizing queries** in the query processing and optimization modules that are integral parts of relational database management systems
## Basic Operations 
- selection
- projection
- cartesian product
- union
- set difference 
## advanced operations
- join
- intersection
- division 
# Our Database![[Screen Shot 2023-08-31 at 3.29.56 PM.png]]

# Selection (or Restriction)
$$  \sigma_{Predicate} $$
works on a single relation (R) and defines a rule that selects only those tuples of R that satisfy the rule

- The "List all staff with a salary greater than 10,000" is our query 
- the mathematical expression is our relation 
![[Screen Shot 2023-08-31 at 3.26.22 PM.png]]

# Projection 
allows you to show only specified columns of a relation table 
$$ \Pi_{col1, ...,  coln}(R)$$  
![[Screen Shot 2023-08-31 at 3.46.40 PM.png]]
(Nested Operations may be performed)

## Eliminating Duplicates 
- projections will remove duplicates from our relation! 
![[Screen Shot 2023-08-31 at 4.09.50 PM.png]]

# Order of operations
-  need to prioritize order in such a way that we will not lose any information after applying an operation 
# Set Operations

## Union (R U S)
- a union of two relations r and s defines a relation that contains all the tuples of R, S, or Both R and S **with duplicate tuples eliminated**
- *note that R and S must be union-compatible*

Union is only possible if the schema of the two relations match... if they have the same number of attributes with each pair of corresponding attributes having the **same domain**

![[Screen Shot 2023-09-05 at 3.23.34 PM.png]]
$$\Pi_{city}(Branch)$$
- Contains all cities with a branch
$$\Pi_{city}(PropertyForRent)$$
- Contains all cities with a rentable property 

$$\Pi_{city}(Branch) \cup\ \Pi_{city}(PropertyForRent)$$
- contains the union of cities from both projections (duplicates removed)

## Difference (R - S) 
$$\Pi_{city}(Branch) - \Pi_{city}(PropertyForRent)$$
- will contain all elements in the first projection removing elements in the second projection 

## Intersection 
$$\Pi_{city}(Branch) \cap\ \Pi_{city}(PropertyForRent)$$
- contains cities with **BOTH** a branch and a property for rent 

## Cartesian Product (R X S)
- defines a relation that is the concatenation of every tuple relation **R** with every tuple relation **S** 

Let R and S be the following:
$$R = \{a, b, c\},
\; S=\{1,2\},
\;\;R\times S = \{(a,1),(a,2),(b,1),(b,2),(c,1),(c,2)\}
$$
![[Screen Shot 2023-09-05 at 3.42.11 PM.png]]

# Theta Join
$$  R\bowtie_{F} S = \sigma_{F}(R\times S) $$
can be expressed with the relation and cartesian product operation.
- first apply your relation 
- then apply cartesian product to the sets 
![[Screen Shot 2023-09-07 at 3.20.55 PM.png]]
![[Screen Shot 2023-09-07 at 3.16.16 PM.png]]

# Equijoin 
when the relation being applied is equality (=)
(*This is a special case of Theta Join*)

# Natural Join 
$$R\bowtie S$$
- an equijoin of the two relations R and S over all common attributes x
- as natural join is the application of equality, we will only keep the tuples which are equal 

![[Screen Shot 2023-09-07 at 3.32.18 PM.png]]
- note  that we only kept the tuples that had **equal** corresponding columns 

# Left Outer Join 
- all rows of the argument on the left side should be inserted 
- if an item in a tuple will be repeated, it must be replaced with a **NULL** space 
# Right Outer Join
- all rows of the argument on the right side should be inserted 
- if an item in a tuple will be repeated, it must be replaced with a **NULL** space 

# Full Outer Join![[Screen Shot 2023-09-07 at 3.47.28 PM.png]]
-  the union  of [[#Left Outer Join]] and  [[#Right Outer Join]]
# Semijoin
- define  a relation that contains the tuples of R  that participate in the join of R with S
- may be defined  in terms of simpler operations
$$\Pi_{A}(R\bowtie_F S)$$
# Division 
-  division  allows us to apply specific constraints to our selections 
![[Screen Shot 2023-09-07 at 3.56.59 PM.png]]
![[Screen Shot 2023-09-07 at 4.00.06 PM.png]]

# Announcement - Exam 1 September 14th  
- class before (sep 12th will  be canceled)
- Topics
	- database  overview
	- relational model
	- relational algebra 