# Aggregate Functions

## Count
- returns number of elements matching query
```SQL
SELECT COUNT(*) AS myCount From  PropertyForRent  WHERE rent > 350;

```
![[Screen Shot 2023-09-26 at 3.15.43 PM.png]]

## Count (DISTINCT)
-  returns only distinct elements from query

```sql 
SELECT COUNT(DISTINCT) PropertyNo As myCount FROM propertyforrent WHERE ...
```

## Group ![[Screen Shot 2023-09-26 at 3.28.55 PM.png]]
##  Sub-querrying

![[Screen Shot 2023-09-26 at 3.42.44 PM.png]]
- the embeded select statement is the subquery

## Any and All
![[Screen Shot 2023-09-26 at 3.49.59 PM.png]]