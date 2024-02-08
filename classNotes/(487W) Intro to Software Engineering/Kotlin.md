	simple and consice language based on java. Runs on the JVM. 
## Table of Contents
### Intro 
- [[#Compare this to java:|Compare this to java:]]
- [[#Println()|Println()]]
### Variables 
- [[#Data Types|Data Types]]
- [[#Data Types#Type Inference|Type Inference]]
- [[#Data Types#Val & Var Keywords|Val & Var Keywords]]
- [[#Data Types#Const Keyword|Const Keyword]]
- [[#Null Safety|Null Safety]]
### Strings 
- [[#Strings|Strings]]
- [[#Strings#String Templates|String Templates]]
- [[#Strings#Multiline Strings|Multiline Strings]]
- [[#Strings#String Comparison|String Comparison]]
### Logic and Math 
- [[#Strings#Arithmetic Operators|Arithmetic Operators]]
- [[#Strings#math()|math()]]
- [[#Strings#better way... imported classes are made available globally|better way... imported classes are made available globally]]
- [[#Strings#Incrementing and Decrementing|Incrementing and Decrementing]]
### When Statement 
- [[#Strings#Used as a Statement|Used as a Statement]]
- [[#Strings#Used as an Expression (it now returns a value)|Used as an Expression (it now returns a value)]]
- [[#Strings#Used in Place of If Statements|Used in Place of If Statements]]
- [[#Strings#When with variables within a range|When with variables within a range]]
### Data Structures 
- [[#Arrays|Arrays]]
- [[#Arrays#Array Functions|Array Functions]]
- [[#Lists|Lists]]
- [[#Lists#Read-Only Lists|Read-Only Lists]]
- [[#Lists#Mutable Lists|Mutable Lists]]
- [[#Lists#Empty Mutable Lists|Empty Mutable Lists]]
### Loops 
- [[#For Loop|For Loop]]
- [[#Looping Over Indicies  and Reversing|Looping Over Indicies  and Reversing]]
- [[#For Each Loop|For Each Loop]]
- [[#While  Loop|While  Loop]]
- [[#Do While Loop|Do While Loop]]
### Functions 
- [[#Parameters & Arguments|Parameters & Arguments]]
- [[#Default Arguments|Default Arguments]]
- [[#Functions as Arguments|Functions as Arguments]]
- [[#Return Keyword|Return Keyword]]
- [[#Return Values From Functions|Return Values From Functions]]
- [[#Returning Multiple Values From Functions|Returning Multiple Values From Functions]]
### Classes
- [[#Getters & Setters|Getters & Setters]]
- [[#Behaviors|Behaviors]]
- [[#Constructors|Constructors]]
- [[#Multiple Constructors|Multiple Constructors]]
- [[#ToString (how to get string representation of an object)|ToString (how to get string representation of an object)]]
- [[#Object Comparison (Equality)|Object Comparison (Equality)]]
- [[#Object Comparison (Equality)#Str|Str]]


# Hello World
	just as in java, each kotlin program requires a main method to run.
``` kotlin
fun main(args: Array<String>){
	println("Hello World")
}
```
### Compare this to java: 

``` Java
public class main{
	public static void main(String[] args){
		System.out.println("hello world")
	}
}
```
# args (program arguments)

```Kotlin 

println("Program arguments:${args.joinToString()}")

```

program arguments may be passed in by going to the button with 3 vertically stacked dots and going to 'edit configuration'. Then you simply add arguments to the appropriate text box.

## Println()
	the println() function has similar versatility to that of python
```Kotlin 
println("hello")
prtinln(3)
println('c')

print("newline: \n  this is on a new line")
```

# Variables

```kotlin 
var name: String = "Jamal"
var age: Int = 18
println("${name} is ${age} years old.")
```
## Data Types 
	kotlin does not use primatives,it instead supports built in objects to represent data types
``` Kotlin 
var number: Int = 19
var l: Long = 100L
var d: Double = 3.14
var f: Float = 3.14F 
var b: Boolean = true 
var s: String = "test"
var c: Char = 'A'
```

var supports the "any" data type, all of the above "primitives" are subclasses of any. 

```Kotlin 
var test: Any = "Hello"
```
### Type Inference
	most often used, kotlin automatically determines the type of the variable you are creating.

```kotlin 
var number = 19
var l: 100L
var d: 3.14 
//...
```

### Val & Var Keywords
	we can define variables in two differnet ways
```Kotlin 
var greetVar = "Hi"   //mutable
greetVar = "Bye"

val greetVar = "Hi"   //imutable
greetVar = "Bye"     //illegal operation
```

- var allows you to define a variable and **assign it a new value later**
- val functions as final in Java

### Const Keyword 
	same as static final in Java. Note that we must define this globally 

``` Kotlin 
const val PI = 3.14 //static final

fun main(args: Array<String>){
	//do stuff...
}
```

- a value stored in a "const val" is "known" to the program before compilation 

Example of this concept 

``` Kotlin 
const val PI = getValueOfPi() //this is illegal and will throw an error

val PI = getValueOfPi() //this is perfectly legal, definition happens at compile-time

fun main(){
	//...
}

fun getValueOfPi(): Double = 3.14
```

## Null Safety
	Kotlin places a big emphasis on null safety

Example of an illegal null assignment:
``` Kotlin 
var name = "Mark"
name = null //illegal operation 
```

If we do in-fact want our variable to be assigned a Null value at some point, we can still do this in the following way: 

```Kotlin 
var name: String? = "Thomas" //"?" allows this variable to point to null
name = null  //now this is legal
```

Since we've defined our variable "name" to point to a string or null, Kotlin has builtin features to safely check which one our variable points to. Example Below:

```Kotlin 

var name: String? = "sue"
println(name?.uppercase()) //output: SUE

name = null 
println(name?.uppercase()) //output: NULL
```

## Strings 
	kotlin has many string operations built in
``` Kotlin
fun main(){
	val name = "tobby"

	//some methods, functions and properties
	name.uppercase()
	name.lowercase()
	name.length
	name[0] 
	name.isEmpty() //returns boolean 
	//...
}
```

### String Templates 
```Kotlin 
//use string templates to format strings
val msg = "name: $name, age: $age" 

```
### Multiline Strings
```Kotlin 
var name = "greg"

val email = """"
	Hello %s
	How
	Are
	You?
""".trimindent() //trimIndent() maintains the indentation 

println(email.format(...args:"Ana"))
```
### String Comparison

- double equals compares memory locations 
- triple equals compares objects, although objects may contain the same content, they are distinct 
``` Kotlin 
val name1 = "Saleh" 
val name2 = "Tim" 
val name3 = String(name2.toCharArray()) //this creates a new String Object. 

//comparing...
println(name1 == name2)         //false 
println(name1.equals(name2))    //false

println(name2 == name3)         //true 
println(name2 === name3)        //false...different object
```
### Heap and String Pool Memory ![[Screen Shot 2023-08-24 at 2.44.59 PM.png]]
	this diagram exaplains the conecpt of string comparison 

Although both name2 and name3 both point to a string with value "Saleh", name3 actually points to a completely different space in memory than name2 

**String Pool** -  a space reserved in memory by the jvm to hold strings. when creating a variable in the normal way (var s = "test"), jvm checks to see if that string already exists in the String Pool and if it does, points that variable to it.

**String()** - when we create a String() object, it is actually stored in a different memory location (the heap) and does not in fact point to a string in the String Pool. 

# Math 
### Arithmetic Operators 
	the usual...
``` Kotlin 
val number1 = 10
val number2 = 2

println(number1 + number2)
println(number1 - number2)
println(number1 * number2)
println(number1 / number2)
println(number1 % number2)
```

### math() 
```Kotlin 
//the long dumb stupid way 
kotlin.math.PI
```

### better way... imported classes are made available globally 
```Kotlin 
import kotlin.math.*

fun main(){
	val n1 = 5
	val n2 = 43

	println(max(n1,n2)) //max function from Math
}
```
	note that we must either import each function individually or import all classes within the package 

### Incrementing and Decrementing
	++ & -- 

```Kotlin 

fun main(){
	var number = 10
	println(++number) //increments first THEN returns | 11
	println(number++) //returns the current THEN Increments | 11
	println(number)   //will now show 12 

	//same applies to decrementing
	println(--number) //10
	println(number--) //10
	println(number) //9
}
```
# Converting Data Types 
```Kotlin 
fun main(){
	var number = "10"
	println(10 + number.toInt())  //20

	//consice way to concatenate different var tpes in a string format
	println("10$number")
}
```

# Booleans 
```Kotlin 
fun main(){
	val isAdult = false 
	val isMale = true
	println(isAdult) //false

	val orderCompleted: Boolean? = null 
	println(orderCompleted) //null 
}
```
	naming convention for booleans should describe the state of a condition starting with the words "has, is"  

Examples:
- isOn
- isBlue
- hasEaten 
# Logical Operators 
``` Kotlin 
fun main(){ 
	val isAdult = true
	val isFemale = false 

	//add
	println(isAdult && isFemale) //false

	//or
	println(isAdult || isFemale)  //true

	//negation
	println(!isAdult) //false
}
```
# Comparison Operators
```Kotlin 
val n1 = 10
val n2 = 20 

//will print booleans
println(n1 > n2) //false
println(n1 < n2) //true
```

# Storing Value Conditionally
```Kotlin
val value = if(n1>=2 || n1 <= 30){
	//println(":)")
	":)"
} else{
	":("
}
```

# Ternary Conditionals 

```kotlin
var result = if (n1 >= n2) ":)" else ":("
```

# When 
	similar to Switch statement in Java

### Used as a Statement
``` Kotlin

val gender = "F"

//when statement may be used as statement or expression
when(gender){
	"F" -> println("FEMALE")
	"M" -> println("MALE")
	else -> { 
		println("Other")
	}
}
```

### Used as an Expression (it now returns a value)
```kotlin 

val gender = "asdf"

///when statement assignsa value to g 
val g = when(gender){
	"F" -> "FEMALE"
	"M" -> "MALE"
	else -> {
		"OTHER"
	}
}
```

### Used in Place of If Statements 
```Kotlin 
val n1 = 10
val n2 = 25

//this when replaces a series of if..else if...else statements 
when{
	(n1 >= n2 || n1 <= 30) -> println(":)")
	(n1 == 100) -> println("100")
	(n2 == 200) -> println("200")
	else -> println(":(")
}
```

### When with variables within a range 
```Kotlin
val age = 18

//this when statement allows "age" to be within a specfied range
when (age){
		in 13..19 -> println("Teenager") //13<= age <=19
		in 0..12-> println("Child") //0<= age <=12
		else -> println("other")
}
```

# Null Booleans 
```Kotlin 
val isAdult: Boolean? = null //? allows for null type safety

if(isAdult){
	println("not null and true")
} else{
	println("false or null")
}
```

# Data structures

## Arrays 
	- arrays sizes are fixed at instantiation
	- if we dont specify a type for our array, it will accept objects of differing types, we can constrain the array by defining its type
```Kotlin 
//creating an array in kotlin 
val names = arrayOf("Jack", "John", "Jill", 2)

//we can define the type of our array aswell
val names = arrayOf<String>("Jack", "John", "Jill") //2 will throw error

//printing an array
println(names.contentToString())
println(names[0])

//asignment 
names[0] = "Sarah"
```

### Array Functions 
```kotlin 
val names = arrayOf<String>("Jack", "John", "Jill") 

//size of the array
println(names.size)

//printing an array
println(names.contentToString())

//creating an array of 5 empty spaces
val null_array = arrayOfNulls<String>(5) 
println(null_array.contentToString())

null_Array[4] = "hello"
println(null_array.contentToString())

//filling an array
null_array.fill("*") 
println(null_array.contentToString())
//null_array = ["*","*","*","*","hello"]

//conditional based on membership
if("Sarah" in names)
{
	println("Found")
} else{
	println("Not Found")
}
```

## Lists 
	lists can be resized at compile time

### Read-Only Lists
```kotlin 

//note that this definition only creates a read-only list!
val names: List<String> = listOf(
	"Jack",
	"Jill",
	"Sally",
	"Peter"
)

//printing a list is possible just by passing list into println
println(names) //["Jack", "Jill", "Sally", "Peter"]
println(names[0]) 

//size
println(names.size)

//membership boolean
println(names.contains("Peter"))

//adding WILL NOT WORK with this read-only list
names.add() //error

//first item
println(names.first())

//last item
println(names.last())

//index of
println(names.indexOf("Jill")) //1

```

### Mutable Lists
	items can be added and removed
```kotlin

//list can now be resized 
val names = mutableListOf(
	"Jack",
	"Jill",
	"Sally",
	"Peter"
)

//removing 
names.remove("Jill")

//adding 
names.add("Mark")

//creating separate variables for items in a list
val (one, two, three) = names 
println($one $two $three) //Jack, Jill, Sally

//we can also omit items
val (one, _, three) = names
println($one, $three) //Jack, Sally
```

### Empty Mutable Lists
``` Kotlin 
//this list is empty
val emptyList = mutableListOf<Any>()

//demonstration
println(emptyLits.isEmpty()) //true 
```

*NOTE: Never mix data types in any data structure...shit gets confusing real quick*

# Loops

## For Loop
```Kotlin 
val names = listOf("mary", "ali", "alex")
val numbers = intArrayOf(1, 2, 3, 4, 5)

//iterating over objects
for (name in names){
	val n = name.replaceFirstChar{ //operations on the object
		it.uppercase() 
	}
	println(n)
}
```

## Looping Over Indicies  and Reversing
```Kotlin 

val letters = charArrayOf(
	'A', 
	'B',
	'C',
	'D',
	'E'
)

//prints index of each char in letters array 
for (index in letters.indicies) {
	println($index - "$letters[index]") //0 - A, 1 - B, ...
}

//printing in reverse
for (index in letters.indicies.reversed()) {
	println($index - "$letters[index]") //4 - E, 3 - D, ...
}

//looping through a string 
val school = "Penn State University"

for (c in school.indicies.reversed()){
	println(l) //ytisrevinu...
}

```

# Range 
```Kotlin 
//printin numbers 1 to 5
for (i in 1..5) println(i)

//print numbers 5 to 1
for (i in 5 downTo 1) println(i)

//step function 
for(i in 100 downTo 10 step 5) prinln(i)
```
## For Each Loop
	- builtin iterating function
	- "it" functions as the place holder for the object 
```Kotlin 
val names = listOf("mary", "ali", "alex")

//for each it in names{ println (it)}
names.forEach{
	println(it)
}
```
## While  Loop
```Kotlin 
var school = "pennstate"
var i = 0

while (i < school.length) {
	println("${school[index]}") 
	++i
}
```

## Do While Loop 
```Kotlin 
/*
do this while some condition is true
the body of the 'do' portion will always be executed atleast once
*/
do {
	println("hello") //will print hello ONCE
} while(false) 
```

# Break  & Continue
	NOTE: Break and continue are only allowed inside of loops, it will not work anywhere else, even foreach functions!!!
	
```Kotlin 
val nums = intArrayOf(1,2,3,4,5,6,7,8,9)


//this for loop will only print the odds and break if n > 5
for (n in nums){
	if (n %2 == 0){
		continue 
	}

	if (n > 5){
		break 
	}
		println(n)
}

//illegal usage 
nums.forEach{
	if (it == 2){
		continue //error 
		break //error 
	}
}
```

# Functions
	- all functions are public by default without an access modifier 
	- Default return type is unit (unit = void return type in java


## Parameters & Arguments
```Kotlin 
fun main(){
	greet("shpoop", 41)

	//we can also explicitely define arguments
	greet(age = 23, name = "greg")
}

fun greet(name: String, age: Int){
	println("Hello 👋 $name")

	When {
		(age >= 18) -> println("$name is an adult")
		else{
			println("$name is a child")
		}
	}
}
```

## Default Arguments 
```Kotlin  
fun main(){
	greet("shpoop", 41)

	//we can also explicitely define arguments
	greet(age = 23, name = "greg")
}

//default value for age
fun greet(name: String, age: Int = -1){
	println("Hello 👋 $name")

	When {
		(age >= 18) -> println("$name is an adult")
		(age < 18)  -> println("$name is a child")
		(age == -1) -> println("AGE NOT PROVIDED")
	}
}
```

## Functions as Arguments 
```Kotlin 
fun main(){
	greet("shpoop", 41)

	//we can also explicitely define arguments
	greet(age = 23, name = "greg")
	foo( bar = {
		//put any logic in here 
		println("THIS  IS THE BAR FUNCTION")
	})

	//we can also omit the parenthesis and simply call foo with the println() function as an argument
	foo{
		println("bar function") //"moo bar function"
	}
}

//default value for age
fun greet(name: String, age: Int = -1){
	println("Hello 👋 $name")

	When {
		(age >= 18) -> println("$name is an adult")
		(age < 18)  -> println("$name is a child")
		(age == -1) -> println("AGE NOT PROVIDED")
	}
}

//bar is essentially a lambda function kinda complicated
fun foo(bar: () -> Unit = {}){
	println("moo")
	bar()
}
// the return type of our bar() function can be any kind 

```
*Note, this only works if the function being passed in is the LAST argument*

# Return 
## Return Keyword
```Kotlin 
val age = 23

//return simply leaves the whole if statement
if (age==-1){
	println("age not provided")
	return //skips the else statements 
} 

else if (age >= 18){
	println("adult")
} else{
	println("child")
}
```

## Return Values From Functions
```Kotlin 
fun main(){
	val mynum = double(10)
}

//specify the return type of the function with : <type> 
fun double(n: Int) : Int { 
	return n * 2
}

/*its also possible to write a function in one line if it consists of a SINGLE expression*/
fun double(n: Int) : Int = n * 2
```

## Returning Multiple Values From Functions 
	- functions can return multiple values with pair() and triple()
```Kotlin 
fun main(){
	//we can store the output of our functions in two distinct variables
	val (v1, v2) = twoValues() 
	val (v1, v2, v3) = threeValues()
}

//the pair return type allows for returning multiple data types
fun twoValues(): Pair<String, Int>{
	return "I am" to 23
}

//also recall we can use "=" if our function returns a sinlge expression
fun twoValues(): Pair<String, Int> =  "I am" to 23

//we could also invoke the Pair() objeect
fun twoValuesWithPair(): Pair<String, Int> = Pair("I am", 23)

//returning three values
fun threeValues(): Triple<Char, Int, String>{
	//we must return an instance of a Triple object
	return Triple(
		"$",
		20,
		"In my account"
	)
}
```
# Classes & Objects
	- in Kotlin, we do not need to use the "new" keyword as we would in java
``` Kotlin 
fun main(){
	val tv = SmartDevice()
	tv.brand = "Samsung"
	tb.price = 1000.0 
	
	val phone = SmartDevice()
	phone.brand = "Apple"
	phone.price = 1200.5
}

//creating our class 
class SmartDevice {
	//define properties...variables
	var brand: String = ""
	var price: Double = 0.0 
	//give some behaviors...functions
	//...
}
```

## Getters & Setters 
```Kotlin 
fun main(){
	val tv = SmartDevice()
	tv.brand = "Samsung"
	tb.price = 1000.0 
	
	val phone = SmartDevice()
	phone.brand = "Apple"
	phone.price = 1200.5

	//directly accesing an attribute...nononono
	println(${tv.brand} "is" ${tv.price})
}

//get() = field ... is whats used by default and not needed
/*
	get() and set() are placed below the the class variable definition. By default they are set to return the field of the variables of they represent. 
	
*/
class SmartDevice {

	var brand: String = ""
		get() = field //this is redundant...just here to show whats goin on under the hood
		
		set(value){
			field = value //this is redundant...just here to show whats goin on under the hood
		}
		
	var price: Double = 0.0 
		get() = field 
		set(value){ 
			field = value.uppercase() //will return uppercase version of value inputed
		}

}
```

## Behaviors 
```Kotlin 
fun main(){
	val tv = SmartDevice()
	tv.brand = "Samsung"
	tv.price = 1000.0 
	tv.turnOn()
	
	val phone = SmartDevice()
	phone.brand = "Apple"
	phone.price = 1200.
	phone.getDeviceState()
}

class SmartDevice {
	var brand: String = ""
	var price: Double = 0.0 
	var isPoweredOn: Boolean = false

	fun getDeviceState() {
		println("$brand is Powered on: $isPoweredOn()")
	}

	//$brand reffers to the current instance of the class 
	fun powerOn() {
		isPoweredOn = true
		println("$brand is powering on...")
	}
	
	fun powerOff() {
		isPoweredOn = false 
		println("$brand is powering off...")
	}
}
```

## Constructors
	constructors are defined in parenteses after the class decleration...
	class myclass (<constructor>) { }
```Kotlin 
fun main() {
	val tv = SmartDevice("Samsung", 1000)
}

//we specify constructors in the definition 
class SmartDevice (
	//we can assign instance variables directly in the constructor  
	var brand: String
	var price: Int
	var isPoweredOn: Boolean = false //default value 
) {
	

	fun getDeviceState() {
		println("$brand is Powered on: $isPoweredOn()")
	}

	//$brand reffers to the current instance of the class 
	fun powerOn() {
		isPoweredOn = true
		println("$brand is powering on...")
	}
	
	fun powerOff() {
		isPoweredOn = false 
		println("$brand is powering off...")
	}
}
```

## Multiple Constructors 
```Kotlin 
fun main() {
	val tv = SmartDevice("Samsung", 1000)
	val laptop = SmartDevice("Asus") //no price given 
}

 
class SmartDevice (
	var brand: String? = null
	var price: Int? = null
	var isPoweredOn: Boolean = false 
) {
	//other constructors
	constructor() : this("",0.0) //this reffers to the main constructor

	//this constructor allows the ommision of the price field 
	constructor(
		brand: String //note that we take a brand but no string 
	)  

	fun getDeviceState() {
		println("$brand is Powered on: $isPoweredOn()")
	}

	fun powerOn() {
		isPoweredOn = true
		println("$brand is powering on...")
	}
	
	fun powerOff() {
		isPoweredOn = false 
		println("$brand is powering off...")	
	}
}
```

## ToString (how to get string representation of an object)
	printing the object directly just prints the hashed memory address we want to print the actual data

IntelliJ has an automatic function generation, to make the toString():
- right click -> generate -> toString()
``` Kotlin
class SmartDevice {
	var brand: String = ""
	var price: Double = 0.0 
	var isPoweredOn: Boolean = false

	fun getDeviceState() {
		println("$brand is Powered on: $isPoweredOn()")
	}

	//$brand reffers to the current instance of the class 
	fun powerOn() {
		isPoweredOn = true
		println("$brand is powering on...")
		
	}
	fun powerOff() {
		isPoweredOn = false 
		println("$brand is powering off...")
	}

	override fun toString(): String { 
		return "SmartDevice(brand=$brand, price=$price, isPoweredOn=$isPoweredOn)"
	} 
}
```

## Object Comparison (Equality)
	to autogenerate an equals() and hashcode()...
	right click -> generate -> equals() and haschode()

```Kotlin 
fun main() {
	var tv1 = SmartDevice("Samsung", 1000)
	var tv2 = SmartDevice("Samsung", 1000)
	println(tv1 == tv2)  //they are distinct objects...they reffer to different places in memory 

	//if we create a new var and assign it to tv1...
	var tv3 = tv1 
	println(tv3 == tv1) //true 
}

class SmartDevice (
	var brand: String? = null
	var price: Int? = null
	var isPoweredOn: Boolean = false 
) {

	fun getDeviceState() {
		println("$brand is Powered on: $isPoweredOn()")
	}

	fun powerOn() {
		isPoweredOn = true
		println("$brand is powering on...")
	}
	
	fun powerOff() {
		isPoweredOn = false 
		println("$brand is powering off...")
	}

	/*WE MUST ADD THIS TO HAVE FUNCTIONING COMPARISONS

		this is an auto-generated function with intellij
	
	*/
	override fun equals(that: Any?): Boolean {
		if (that == null) return false
		if (that !is SmartDevice) return false
		if (this.brand == that.brand) {
			return true
		} else {
			return false
		}
		if (this.price == that.price) {
			return true
		} else {
			return false
		}
		if (this.isPoweredOn == that.isPoweredOn) {
			return true
		} else {
			return false
		}
	}

	//Also autogenerated with right click -> generate -> hashCode()
	override fun hashCode(): Int{
		//=== functionality i think 
	}
}
```
### Str
uctural and Referential Equality 
- obj1 == obj2  (negated is !=) -  we are comparing objects  (Structural Equality)
- obj1 === obj2 (negated is !== ) - we are comparing memory addresses (Referential Equality )