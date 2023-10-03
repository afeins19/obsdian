_architecture_: simply a subset of design
- is there a difference between architecture of a system
- if so what is the distinction?
- what problems do they address; that is, why do we need them?

**Architecture is the highest level of abstraction**
-> then design
-> then implementation

## Conways Law
"any organization that designs a system will produce a design whose structure is a copy of the organizations communication structure" - a companys design will mimic its current structure 

# Coupling 
- the degree to which modules are inter-related
	- loosely coupled if interaction is only through interfaces
	- tightly coupled the implementation of one module depends on the implementation of another

## Forms of Coupling
- message - send messages through interfaces
- subclass - inheritance of methods through superclass
- global - two modules share global data
- content - one module relies on the implementation of another 

# MVC Architecture 

clients data is passed through a controller which manipulates models and passes it to a view which then displays it to the user 

