# Referential Integrity

recall that we establish relationships between tables when we use a primary key of one row as a foreign key of another
![[Screen Shot 2023-10-05 at 3.18.45 PM.png]]

- in the PropertyForRent table, we must specify that propertyNo is a Foreign Key 
- We also specify that branchNo is a foreign key for PropertyForRent

Suppose that we remove a branch from the branch table, any row in PropertyForRent that used that branch as a foreign key must now know what to do. The DBMS must account for this.
- cascade 
- set default
- set null
- no action

# DBMS Instruction examples 

## 
```sqlite
FOREIGN KEY (staffNO) REFERENCES Staff
ON DELETE SET NULL; 
```

# CASCADE (update)
- if a primary key is changed, all tables that use this primary key as a primary key will receive the updated value

```

```

# SET DEFAULT 
- if a primary key is deleted, the table which uses it as a foreign key will insert a default value 
```sqlite
```

# No Action 
- the dbms will **NOT** allow you delete your primary key 

# General Constraints 
- updates to tables may be constrained by enterprise rules 
	- Example: a member of staff cannot manage more than 100 properties at the same time

### Example: Creating the property for rent table 
![[Screen Shot 2023-10-05 at 3.34.59 PM.png]]


### Example: Applying Various Constraints 
![[Screen Shot 2023-10-05 at 3.39.06 PM.png]]

# Altering a Table
Say wed like to:
- add a column
- drop a column
- add a new table constraint
- set a default value for a column
- dropa default for a column 

![[Screen Shot 2023-10-05 at 3.43.16 PM.png]]

## Horizontal View Creation
- we restrict rows

![[Screen Shot 2023-10-05 at 3.46.25 PM.png]]
- views represent a goal or reason for why wed want to format and filter data in this way 

```sqlite
CREATE VIEW Manager3Staff -- creating the view 
```

## Vertical View Creation 
- we restrict columns

# Drop View 
```SQLite 
DROP VIEW (Manager3Staff);
```
