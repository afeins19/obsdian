where X=SQL

# Database Operations

### Create
```sql
CREATE DATABASE myDatabase; 
```

### Delete
```SQL
DROP DATABASE myDatabase; 
```

### List 
```SQL
SHOW DATABASES;
```

### Use
using a specific database
```SQL
USE employeeDatabase
```

# Selection 

### General Selection 
select all rows and columns from the current database's table 
```SQL
SELECT * FROM employees;
```

### Select with Columns
select all rows from a table but only display the selected columns. (*note: it is ok to split up commands across multiple lines for readability*)
```SQL
Select employee_name, employee_salary FROM employees;
```

### Select with Row Limit
select all columns but just the up to the specified amount of rows 
```SQL 
SELECT * FROM employees LIMIT n --n is some integer 
```

### Select with Sub-string search 
retrieve all column values from the table that match the given sub-string 
```SQL
SELECT employee_name FROM employees WHERE employee_name LIKE '%greg%'; 
```

### Selection with Sub-string length matching
in this example, we retrieve all column values that start with an 'S' and have exactly 4 characters after it (where each "\_" denotes a single character))
```SQL
SELECT * FROM departments WHERE department_name LIKE `S____`;
```

### Selection with distinct 
only return unique values from a given table (don't show duplicates)
```SQL
SELECT DISTINCT color FROM favorite_color_table; 
```

### Selection with Ordering 
ordering the returned result by either ascending (ASC) or descending (DESC). By default, the command may be used alone and will use ascending order by default. 
```SQL
SELECT salary from employee_table ORDER BY salary ASC; 
SELECT height from medical_details ORDER BY height DESC; 
```

### Selection with comparison operators 
its possible to make selections using the comparison operator symbols `(=, <, >, <=, >=, <>)`
```SQL
SELECT * FROM movies WHERE rating > 90 OR release_year < 2002;
```

### Selection with set membership 
using the 'IN' keyword, we can select rows with column values that must be in the given set.
```SQL
SELECT * FROM packages WHERE hazard_Category IN ('CHEMICAL', 'SHARP'); 
```

Its also possible to use the negation to select rows with column values that are **not** in the given set 

```SQL
SELECT * FROM students WHERE major NOT IN ('IST', 'CMPSC', 'EE')
```

### Select with a range specifier 
specify a range of values to select between
```SQL
SELECT * FROM vintage_cars WHERE model_year BETWEEN 1950 AND 1980; 
```

# Counting Number of Occurrences 
the `COUNT` keywords returns the number of elements produced by a given SQL Query. 
```SQL
SELECT COUNT(*) FROM employees WHERE fav_icecream = 'Chocolate';
```

# Aggregate Functions 







