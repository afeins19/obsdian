	suppose we're developing a database for a particular business. Our data relationship structure depends on the nature of the data itself. only after this can we start designing a database/conceptual model. 

## Relational Model Terminology 

- **Relation**: a table with columns and rows 
- **Attribute**: a named column of a relation
	- **Domain**: the set of allowable values for one or more attributes 
- **Tuple**: a row relation 

![[Screen Shot 2023-08-24 at 3.19.55 PM.png]]   

- **Cardinality**: The number of rows 
- **Degree**: The number of columns 

*note that each attribute can only take a specific type of data 

# Columns (attributes)
	when creating a new attribute, we must first define its domain 

![[Screen Shot 2023-08-24 at 3.32.08 PM.png]]

# Relational Database
	a collection of normalized relations with distinct relation names
	Example: a relational database is the set of all normalized tables (staff, students, departments, etc.)

- *normalized means that the relations are appropriately structure*d
# Keys 
	very important concept :)

- **Superkey**: an attribute or set of attributes that uniquely identifies a tuple within a relation 
- **Candidate Key**: a Superkey such that no proper subset is a Superkey within the relation 
- **Primary Key**: A Candidate key selected to identify tuples uniquely within the relation 
-------------------------------------------------------------
- **Alternate Keys**:  
- **Foreign Key**: if an attribute is a primary key in another table, then it is a foreign key in the current table
- **Primary Key**: The key used as reference from a foreign table 

# Foreign Keys
	a table can contain multiple foreign keys 

![[Screen Shot 2023-08-29 at 3.21.36 PM.png]]


# Composite Primary Keys
	multiple attributes are create the primary key
[[Screen Shot 2023-08-29 at 3.17.15 PM.png]]

in this case, pk = {clientNo, propertyNo} 

![[Screen Shot 2023-08-29 at 3.20.13 PM.png]]

in this case, pk = {clientNo, branchNo} 

# Relational Schema 

![[Screen Shot 2023-08-29 at 3.30.13 PM.png]]
(1) specify name of relation
(2) attribute names in parentheses
(3) underline primary key 

# Integrity Constraints 
	 a set of contraints which ensure that the data is accurate 
## Null
- represents an empty value 
## Entity Integrity
- in a base relation, no attribute of a primary key can be null 
# Referential Integrity 
- if a foreign key exists in a relation, either foreign key value must match a primary key value of some tuple in its home relation or the foreign key value must be wholly null 
- in other words, a foreign key must exist as a primary key in some other relation or must be null

# Integrity Constraints  
	defining constants for database membership counts 
# Views  

## Base Relation 
- Base Relation: a named relation corresponding to an entity. in conceptual schema, whose tuples are physically stored in the database 
## View 
- Dynamic result of one or more relational operations on base relations to produce another relation 
## Updating Views
- all updates to the base relation should be immediately reflected in all views that reference a base relation
- if a view is updated, underlying base relations should reflect the change (with some restrictions)
### Restrictions 
- updates are allowed if  a query involves. a single base relation and contains a primary key of base relation
- updates  are not allowed involving multiple base relations
- updates are not allowed involving. aggregation or grouping operations 
