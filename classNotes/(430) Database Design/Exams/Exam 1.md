# Question 2

## (1) First and Last Name of clients at branch "b003"
![[Screen Shot 2023-09-14 at 11.03.03 PM.png]]

```
$$\Pi_{fName,lName}(\sigma_{branchNo=b003}(\Pi_{clientNo, branchNo}(Registration) \bowtie \Pi_{clientNo, fName, lName}(client)))
$$
```

![[Screen Shot 2023-09-14 at 7.08.55 PM.png]]
## (2) Which staff members were born after 1955?
$$\sigma_{DOB > 1955}(Staff)$$
- this will return the entire tuple for staff matching that selection 

![[Screen Shot 2023-09-14 at 7.10.29 PM.png]]
$$\Pi_{fName,lName}(\sigma_{DOB > 1955}(Staff))$$
- this will return only the first and last names of the staff
![[Screen Shot 2023-09-14 at 7.57.38 PM.png]]
## (3) Flats with rent less than $500 
$$\sigma_{rent<500}(\sigma_{type=flat}(PropertyForRent))$$
![[Screen Shot 2023-09-14 at 7.11.47 PM.png]]
## (4)  Phone numbers of owners with property in London
![[Screen Shot 2023-09-14 at 10.58.28 PM.png]]
```
$$\Pi_{telNo}(\sigma_{city='london'}(\Pi_{city,owNo}(PropertyForRent) \bowtie \Pi_{telNo, owNo}(PrivateOwner)))$$
```
# Question 3

## (1)  
![[Screen Shot 2023-09-14 at 7.49.23 PM.png]]


##  (2)
![[Screen Shot 2023-09-14 at 7.14.39 PM.png]]

## (3)
![[Screen Shot 2023-09-14 at 7.50.49 PM.png]]
## (4)
![[Screen Shot 2023-09-14 at 7.53.39 PM.png]]
##  (5)

![[Screen Shot 2023-09-14 at 7.15.20 PM.png]]