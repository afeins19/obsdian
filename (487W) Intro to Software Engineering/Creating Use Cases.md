(try sysml (uml outlining software))

- creating names for different groups (such as actors, stake holders) use descriptive  names 
# Actor 
a role in the use of our application. They are the beneficiary of the use case. 
# Example of a Use Case 
- **actor**: Student
- **use** **case**: Take Exam

n: Take Exam 
----------------------
A: Student
Flow of events: 
1. Student connects to exam server
2. server performs auth() on student, if auth() don't run auth()
3. student selects an exam
4. student answers questions of different modalities
5. student submits completed exam
6. **on  submit** validate exam or save state and alert student of incomplete questions 
7. logout 

**Entry**: 
1. Auth
2. Computing resources 

**Exit**:
1. complete exam or save state 
# Using Extensions on our use case
	outlining exceptions and Variations that may arrise in the use case
**Extends**
# Using Inclusions on our use case
	outling links to other use cases 
**Includes**

