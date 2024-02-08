- code coverage is easy to compute, intuitive but it is **NOT SUFFICIENT**
## Mutation Testing
mutation testing involves changing the logic in our code (to purposefully test fail test cases). This allows us to automate the writing of unit tests.

```python 
if a == b:
	doStuff()

# one possible mutant of this is...

if a != b:
	doStuff() 

# another 
if a > b:
	doStuff()
```
- mutants are created and pushed into our test suite 
- generally, we want to minimize the amount of mutants that pass


```java 
public int min(int a, int b){
	return a < b ? a : b;
}

//mutants 
M1: return a;
M2: return b;
M3: return a>=b ? a : b;
M4: return a <= b ? a : b;
```
**Note**
- not that M4 is not unique... the set of its returns is identical to the additional function 
- M3 is redundant, as it is a composition of the possible returns of M1 and M2 
## Detectable vs. Productive Mutants 
- Detectable mutants are good -> tests need to be written
- Equivalent mutants are bad -> no tests to write 

A more nuanced view
- productive mutants elicit better/more tests 

**look into abstract syntax trees (ast)**