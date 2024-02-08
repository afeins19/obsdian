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


# Dependencies Definitions
## Multivalued Attributes 
non key attributes or groups of non-key attributes the values of which are not uniquely identified
![[Screen Shot 2023-11-28 at 3.15.13 PM.png]]
**is this table in normalized form?**:
- does the primary key determine all other attributes? 
	- stud_id - > name, course_id -> units but we dont see any of the links: stud_id -> nor name -> units 
	- from this we can only say that stud_id can only determine the name attribute only...this is in unormalized form 
- this table is **UNF** (unormalized form)

## Partial Depndency
when a non key attribute is determined by a **part** but not the whole of a **COMPOSITE** primary key 
![[Screen Shot 2023-11-28 at 3.21.08 PM.png]]

- name is a non-key but note that there exists a functional dependency between cust_id and name (cucst_id -> name)  **this is a partial dependency**


## Transitive Dependency (TD)
when a non-key attribute determines another non-key attribute 
![[Screen Shot 2023-11-28 at 3.24.10 PM.png]]


## Heirarchy of Normalized Forms (NF)
- **Unormalized** - there are multivalued attributes or repeating groups
- 1NF - no multivalued attributes or repeating groups
- 2NF - 1NF plus no partial dependencies 
- 3NF - 2NF plus no transitive dependencies 

so a 3NF table has no partial or transitive dependencies (for example). 


## Example Question of NF
![[Screen Shot 2023-11-28 at 3.32.18 PM.png]]
- Primary key: ISB 
- functional dependencies
	- isbn -> title
	- isbn -> publisher
	- publisher -> address 

**Solution: **

![[Screen Shot 2023-11-28 at 3.34.58 PM.png]]
- note that we have a primary key so we have atleast 1NF
- it is at least a 2NF relation as we dont have any partial dependencies (no composite key)
- there exists a transitive relationship (publisher -> address (non-key relationship)) so it we cannot have a 3NF relation since there does exist a transitive relationship 

**Example 2: **
![[Screen Shot 2023-11-28 at 3.38.43 PM.png]]
Notes:
- 2 primary keys (determine description)
- relation product_id - > description (partial relation)

**solution**: we have a primary key (composite) relationship ((order_no, product_id) -> description) but there exists a partial relation (product_id -> description) so this is 1NF? 

**Example 2**
![[Screen Shot 2023-11-28 at 3.44.55 PM.png]]
Notes: 
- primary key (part_id) determines description and price
- we have non-key attributes being determined
- we have multivalued relationships

Solution: UNF because the primary key cannot uniquely determine **all** other attributes 

# Increasing NF of a relation 
unf -> 1nf (set a true pk)
1nf -> 2nf (remove partial dependencies)
2nf -> 3nf (remove transitive dependencies)

![[Screen Shot 2023-11-28 at 3.55.39 PM.png]]
- 2NF must have no partial relationships
- we remove these PR's by removing partial relationships and creating new tables for them 
- now we have 3 tables: 

![[Screen Shot 2023-11-28 at 3.56.40 PM.png]]

# EXAM DEC 7th (NO CLASS 5th )

# Normalization Practice 

## Question 1 
- lease table 
- placeNo uniquely identifies each room in all flats and is used when leasing a room to a student 

![[Screen Shot 2023-11-30 at 3.11.43 PM.png]]
1. find the functional dependencies 
2. find the primary key for the table 
3. is this table 3NF? if not, explain

1. Functional Dependencie:
flatNo -> flatAddress
bannerId -> fName, lName 
placeNo -> flatNo 
leaseNo -> All other Attributes (primary key) 

2. primary key 
leaseNo -> All other attributes (definition of primary key relation) 

3. NF rating:
Atleast 1NF? yes, primary key exists 
Atleast 2NF? yes, no partial dependencies 
Atleast 3NF? No, There exist multiple transitive dependencies so this is not 3NF 

## Converting the Above table into 3NF 
1. remove transitive dependencies:
create new individual tables for all transitive relationships: 
- bannerId -> fName, lName = studentTable: (bannerId, fName, lName) 
- placeNo -> flatNo, flatAddress = placeTable: (placeNo, flatNo, flatAddress)
**NOTE: placeTable must be further decomposed as we have the relationship flatNo-> flatAddress**s
- flatTable: (flatNo, flatAddress)

remove the following collumns from the table
- fName, lName
- flantNo, flatAddress


# Exam 2: 
(no classes next week)
- December 7th (Entire Day to solve, submit by midnight)

## Topics
- Normalization 
- ER Model (Explanation and Diagram) 
- Fact - Finding Techniques (advantages vs disadvantages) 
- DB Development Life Cycle 