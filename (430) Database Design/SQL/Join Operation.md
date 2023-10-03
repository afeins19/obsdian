# Simple Join
**Joining is performed when the FROM statement contains more than 1  table**
- list all clients who  have viewed a property along with any  comment supplied'
```SQL
SELECT c.clientNo fName, lName,
	propertyNo, comment
	FROM Client c, Viewing v
	WHERE c.clientNo = v.clientNo 
```

*select clientno, fname, lname, propertyno, comment from  client x vieweing where a client has viewed a product* 

## Sorting  a join 
```SQL
ORDER BY attr1, attr2, attr3...
```

##  Left Outer Join (Example)
list branches and properties that are in the same city along with any unmatched branches 

```SQL
SELECT b.*, p.*
FROM Branch1 b LEFT JOIN 
	PropertyForRent1 p ON b.bCity = p.pCity;
```


# Intersection
```SQL
(Select city FROM Branch)
INTERSECT 
(SELECT city FROM PropertyForRent) 
```

# Insert 
say we want to insert data into **ALL** collumns
```SQL
INSERT INTO Staff
VALUES ('attr1', 'attr2', 'attr3',...)
```
- note that we don't have to mention the columns for which attributes to insert, we will need specify the columns if we are only selecting certain ones
- **order must be maintained**

note, when inserting new rows with only some columns being filled, unspecified collumns will recieve a **NULL** entry for that row unless a **default value** is specified 

# Update 
- update all rows

### Example: all staff recieve 3% pay bump
- this implies that for each staff members current salary, we are setting the salary to 103% its currrent value
```SQL
UPDATE Staff 
SET salary = salary*1.03; 
```

### Example: only managers receive a 3% increase 
```SQL
UPDATE Staff 
SET salary = salary*1.03
WHERE staff.position = 'manager';
```

### Example: Increase rent of all flats by $50 
```SQL 
UPDATE PropertyForRent 
SET rent = rent+50
WHERE type = "flat";
```

# Delete 
- deleting rows from a table 

### Example: delete all entries for property PG4 in the viewing table
```SQL 
DELETE FROM Viewing 
WHERE propertyNo = 'PG4';
```

### NOTE: DOING THIS WILL DELETE EVERYTHING FROM VIEWING!!! 
```SQL 
DELETE FROM Viewing; 
```

