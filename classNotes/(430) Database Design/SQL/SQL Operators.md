# Selection 
```SQL
SELECT staffNo, fName, lName, salary
FROM staff 
```
## Output
- note that this outputs duplicate entries into our table 
## Distinct Operator
```SQL
SELECT DISTINCT staffNo, fName, lName, salary 
FROM staff 
```
## Where Operator 
```SQL
SELECT DISTINCT staffNo, fName, lName, salary
WHERE salary < 10000
FROM staff  
```
## Pattern Matching
- say we are  trying to find the city within the address table 
- we need to create a _pattern_ to tell SQL what to look for in the string
![[Screen Shot 2023-09-21 at 3.38.39 PM.png]]

### Like Operator 
- syntax is like -regex pattern-
- % denotes any sequence of characters containing "Glasgow"
- _ denotes any single character followed by the exact phrase
```SQL
Select ownerNo, fName, lName, address, telNo
FROM PrivateOwner 
WHERE address LIKE %Glasgow% 

Select ownerNo, fName, lName, address, telNo
FROM PrivateOwner 
WHERE fName LIKE _avid 
```
- _avid accepts: david, lavid, mavid but not davidd, ddavid

## Null Operator 
```SQL 
SELECT clientNo, viewDate 
From Viewing 
Where propertyNo = 'PG4' AND 
		comment IS NULL;
```
- we must  use IS NULL (not == null)

## Ordering 
- ordering allows us to change the order of the returned relation after our operation 
- DESC  denotes that we would like a value by descending order 
```SQL
SELECT staffNo, fName, lName, salary
FROM staff
ORDER BY type, salary DESC; 
```

- we can apply multiple orderings to our relation we do this by simply adding another attribute to order (by default it will be ordered in descending order )
