within a database, tables must be **normalized**  

# What is Normalization?
normalization is a technique for producing 

- easier for tbe user to access and maintain data
- data takes up minimal space 
# Why do we need Normalization?

Design1: Separates Staff and branch table. the bAddress must only be given once 

Design2: we have to store redundant information. for example, bAddress will store multiple value that are duplicates
	- updating will be difficult if Address is changed 
	- adding a new branch (b004 for example) is impossible as a singleton in design 2
	- deleting staff might result in the complete removal of a branch 

**Design 2 is not normalized**

![[Screen Shot 2023-11-16 at 3.16.26 PM.png]]
# Normalization Technique 
in order to normalize we must establish the **functional dependencies**

## Functional dependency 
describes the relationship between attributes 

![[Screen Shot 2023-11-16 at 3.28.33 PM.png]]
if a functional dependency exists between A and B we say that 
**A determines B**

- it is also possible for multiple values to determine a single other value 
## Example
![[Screen Shot 2023-11-16 at 3.34.48 PM.png]]
each staff number can be tied to a single position so staffNumber and position have a functional dependency 

some other functional dependencies: 
- branchNo -> bAddress
- staffNo -> sName 

*note that these relationships do not necessarily work in reverse. 
	staffNo -> postion but it is **not true** that position -> staffNo*

*note that we must make note of all possible relationships. it seems that sName must map to a single position but it may be possible that 2 employees may have the same sName entry* 

