# We will discuss defining our database 

# Data Types

**Example**      | **DataType**          | **Explanation**
- branchNo | **CHAR(4)**            | denotes a char data type with fixed length 
- address     | **VARCHAR(30)**   | denotes a char with up to a specified length (up to 30)
- bitString    | BIT(4)                 | denotes represents binary data with fixed lenght of bits
- Salary        | Decimal(7,2)      | (precission, scale). (7,2) -> 9999999.99 
- rooms       | SMALLINT          | up to 2 bytes 
- viewDate   | DATE                  | year,month,day format

# Integrity Constraints 
these are principles that enhance our data integrity 

## Required Data
example: say we specify the following collumn

position | VARCHAR(10) | NOT NUll 

## Domain Constraining 
specify that the inputted data exists in the domain 

(a) CHECK 
sex    CHAR NOT NULL
                   CHECK (sex IN ('M','F'))

(b) CREATE DOMAIN
- when we create a domain we are really creating a **custom data type**

CREATE DOMAIN DomainName AS dataType
\[DEFAULT defaultOption]
\[CHECK (searchCondition)]

for example:

CREATE DOMAIN SexType AS CHAR
	Default 'M'
	CHECK (VALUE IN ('M','F'));
=> sex SexType NOT NULL

## searchCondition 
when creating a domain, we can use a search on another table to generate allowed values for the domain 

example:
CREATE DOMAIN branchNo as CHAR(4)
CHECK ()

## Entity Integrity 
- primary key of a table must contain a unique, non-null value for each row 

-in CREATE and ALTER TABLE statements:
	PRIMARY KEY (staffNo); //staff table
	PRIMARY KEY (clientNo, propertyNo); //veiwing table 
- as we can only have one primary key, we use the **UNIQUE** key word 
- every column that appears in a UNIQUE clause must also be declared as NOT NULL
- example: UNIQUE(telNo) 
