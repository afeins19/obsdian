
# Exercise 1

## SQL Command
```SQL
SELECT propertyNo, city 
FROM propertyforrent 
WHERE propertyNo IN 
	(SELECT propertyNo 
	 FROM viewing); 
```
## Output Table
![[Pasted image 20231004205202.png]]

# Exercise 2

## SQL Command
```SQL
SELECT staff.staffNo, staff.lName, (staff.salary) / 12 
FROM staff 
WHERE (staff.salary) / 12 < 1000; 
```
## Output Table

![[Pasted image 20231004205711.png]]
# Exercise 3

## SQL Command
```SQL
SELECT client.clientNo, client.lName, client.email 
FROM client 
WHERE client.email LIKE '%flintyrock%'; 
```
## Output Table
![[Pasted image 20231004210547.png]]
# Exercise 4

## SQL Command
```SQL
SELECT COUNT(staff.sex) as NumOfFemaleStaff 
FROM staff 
WHERE staff.sex LIKE '%F'; 
```
## Output Table
![[Pasted image 20231004211413.png]]
# Exercise 5

## SQL Command
```SQL
SELECT branchNo as BranchNumber, COUNT(*) as MyCount, AVG(staff.salary) as MyAverage 
FROM staff 
GROUP BY branchNo 
HAVING MyCount >= 2; 
```
## Output Table
![[Pasted image 20231004213103.png]]
# Exercise 6

## SQL Command
```SQL
-- Updating the property 
UPDATE propertyforrent 
SET rooms = rooms + 1, rent = rent * 1.1 
WHERE propertyNo = 'PL94'; 

-- getting the row 
SELECT * 
FROM propertyforrent 
WHERE propertyNo = 'PL94'; 
```
## Output Table

![[Pasted image 20231004220902.png]]

