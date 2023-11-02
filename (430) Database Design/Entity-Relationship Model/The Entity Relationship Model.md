# Concepts of the ER Model
- Entity Types
- Relationship Types
- Attributes 

# Entity Type 
A group of objects with the same properties (physical or conceptual)
An Entity Type is identified by:
- name
- list of attributes 

## Entity Occurence 

each uniquely identifiable object of an entity type is referred to as an entity occurrence (analogous to the rows a relational db)

## UML Symbol 

![[Screen Shot 2023-11-02 at 3.20.46 PM.png]]

# Relationship Type
- a set of meaningful associations among entity types 
	- each relationship type is given a name that describes its function 

## Relationship Occurence
- A uniquely identifiable association, which includes one occurence from each participating entity type 

## Semantic net of a *Has* relationship type 
![[Screen Shot 2023-11-02 at 3.25.10 PM.png]]
- branch b003 has staff sg37, sg14
- branch b007 has staff sa9 

## UML Symbol 
- each realtionship type is shown as a line connecting the associated entity types and labeled with the name of the relationship 
- Normally named using a verb (ex Supervises,  Manages etc)
- labeled with direction b <- a = a has b

## Degree of a Relationship 
the number of participating entities in a relationship is called the degree 
- binary relationship: degree 2
- ternary relationsip: degree 3
- complex relationship: > degree 3

### UML Symbol
![[Screen Shot 2023-11-02 at 3.34.24 PM.png]]

## Recursive Relationship ![[Screen Shot 2023-11-02 at 3.35.15 PM.png]]
- some staff are supervisors and their role is to supervise other staff (supervisees)

## Multiple Relationships Between Entities 
![[Screen Shot 2023-11-02 at 3.38.40 PM.png]]
- its good to write the specific role of the relationship above the relationship 

# Attributes 

## Attributes of an Entity Type 
this is similar to a column in a relational database
- property of an entity 

## Attribute Domain 
the set of allowable values for one or more attributes 
- the constraints on the values that are allowed in the columns 

![[Screen Shot 2023-11-02 at 3.42.20 PM.png]]

### Attribute Values
![[Screen Shot 2023-11-02 at 3.45.19 PM.png]]
- attributes an sometimes accept more than one value 

### Derived Attribute 
an attribute that represents a value that is derivable from the value of a related attribute or set of attributes
![[Screen Shot 2023-11-02 at 3.47.21 PM.png]]

## Example of all the above Components
![[Screen Shot 2023-11-02 at 3.48.40 PM.png]]
