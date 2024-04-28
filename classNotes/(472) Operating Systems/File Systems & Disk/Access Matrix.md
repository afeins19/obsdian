Generally, a sparse matrix 
- option 1 - global table with sparse matrix representation 
	- drawback is that memory is allocated for some slots that are never used in the matrix since its sparse 
- option 2 - access lists for object 
	- each column implemented as an access list for one object
	- results in a **per-object** list that consists of ordered pairs <domain, rights-set> where rights set are the access rights 
- option 3 - capability lists for domains
	- associate each row with its domain
	- a list of objects together with the operations allowed on those objects 
	- a more fine-grained control over what each domain can do with specific objects 

# Access Matrix Implementations 
![[Screen Shot 2024-04-17 at 10.17.14 AM.png]]

# Access List 
a list of entries, eachh representing pairs of a domain and their corresponding acess rights 
- domain A: Read/Wwrite, Execute
- domain B: Read
- domain C: Write
permissions are explicit but this becomes complex in a dynamic environment 


# Capability list 
 a list of entries each representing a pair of an object and the corresponding access rights associated with that object 
 - allows for more fine grained control in dynamic environments but is more challenging to use in revocation 
	 - revoking access to a resource requires revoking the corresponding capability from each entity that holds it 

### Revocation of Access Rights 
various options to remove the access rights of a domain to an object
- immediate vs delayed
- selective vs general 
- partial vs total
- temporary vs permanent 

deleting access rights is trivial if one is using an access list but is difficult if one is using a capability list. 


### Comparing Different Access Matrix Implementations
![[Screen Shot 2024-04-17 at 10.35.20 AM.png]]

# Capability based access control system using back-pointers
- each object has a list of pointers where each pointer represents a specific access right
- each domain has a list of pointers where each pointer represents a specific access right of a specific object
- revoking a capability by simply removing the list of pointers associated with that object 

# Inode table
maintains the list of all access rights in the os globally

# Role-Based Access Control (RBAC)
- protection can be applied to non-file resources such as processes 
- privilege is the right to execute system calls or use an option within a system call
- users are assigned roles granting access to privileges and programs 
	- enable role via password to gain privileges 
### Role 
- a set of specific privileges 