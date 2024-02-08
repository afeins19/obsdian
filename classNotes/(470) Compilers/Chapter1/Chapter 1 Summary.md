### Parameter Passing 
parameters are passed form a calling procedure to the callee either by value or by reference. When large objects are passed by value, the values passed are references to the objects themselves, resulting in effective reference. 

### Call by Value
the actual parameter is evaluated (if it is an expression) or copied (if it is a variable). This value is placed in the location belonging to the corresponding formal parameter of the call procedure. 

### Interpreter
a common kind of language processor. Instead of producing a target program as a translation, an interpreter appears to directly execute the operations specific in the source program on inputs supplied by the user 


# Phases of Language Processing 

## Lexical Analysis 
The first phase of a compiler is called lexical analysis or scanning. The  lexical analyzer reads the stream of characters making up the source  program and groups the characters into meaningful sequences called lexemes. For each lexeme, the lexical analyzer produces as output a  token of the form  token-name; attribute-value

# Syntax Analysis
The second phase of the compiler is syntax analysis or parsing. The parser uses the first components of the tokens produced by the lexical analyzer to create a tree-like intermediate representation that depicts the grammatical structure of the token stream.

# Call-By-Reference
in call-by-reference, the address of the actual parameter is passed to the callee as the value of the corresponding formal parameter. Uses of the formal parameter in the code of the callee are implement Changes to the formal parameter thus appear as changes to the actual parameter. need by following this pointer to the location indicated by the caller.

# Explicit Access Control
Classes and structures introduce a new scope for their members. If p is an object of a class with a field (member) x, then the use of x in p:x refers to field x in the class definition.

# Dynamic Scope
The term dynamic scope, however, usually refers to the following  
policy: use of a name x refers to the declaration of x in the most  
recently called, not-yet-terminated, procedure with such a  
declaration.

# Type Checking 
Type checking is an effective and well-established technique to catch inconsistencies in programs. It can be used to catch errors, for example, where an operation is applied to the wrong type of object, or if parameters passed to a procedure do not match the signature of the procedure.

# Intermediate Code Generation
in the process of translating a source program into target code, a compiler may construct one or more intermediate representations, which can have a variety of forms. Syntax trees are a form of intermediate representation; they are commonly used during syntax and semantic analysis

# Symbol Table 
The symbol table is a data structure containing a record for each variable name, with Fields for the attributes of the name. The data structure should be designed to allow the compiler to and the record for each name quickly and to store or retrieve data from that record quickly.

# Binary Translation 
Compiler technology can be used to translate the binary code from one machine to another, allowing a machine to run programs originally compiled for another instruction set.

# The Static/Dynamic Distinction
### Static
for a computer language this is what decisions the compiler can make about a program. If a language uses a policy that allows the compiler to decide an issue, then we say that the language uses a static policy, or that the issue can be decided at compile time. 

### Dynamic
a policy that only allows a decision to be made when we execute the program 

# Machine and Assembly Languages 
machine languages were the first generation programming languages followed by assembly languages. programming in these languages was time consuming and error prone 

# Higher Level Languages 
languages that are simpler to interact with. Lotts of stuff handled under the hood. 

# Scope Rules 
