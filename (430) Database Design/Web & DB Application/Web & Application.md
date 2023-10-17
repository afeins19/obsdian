Here we learn to create an application to allow users to structure and create queries to our database

![[Screen Shot 2023-10-12 at 3.17.45 PM.png]]
# Process 
1. data from ui is sent to php
2. php creates the sql query and send to the db
3. php will receive the db response with the data it returned 
4. php will then pass it to the UI

*note: the backed php layer is the most important one here to focus on*

# Setting up 

1. create a directory to hold the php file 
2. create a new file in a text editor 
3. click explorer on XAMPP
4. inside the XAMPP find htdocs
5. create the cmpsc430 folder

# Creating a connection to our DB 
within the cmpsc430  folder, create a file with the following code
```php
<?php
$servername = "localhost";  //php uses  '$' to denote variables
$username = "root"; 
$password = ""; //when database was created, we left the password field empty

$dbname = "universitydb"; 

//create database connection --  order is important: (server, username,password,dbname)
$conn = new mysqli($servername, $username, $password, $dbname); 

//check connection 
if($conn -> connect_error){
	die("Connection Failed: ".$conn->conect_error) //concatenate with the connection error 
}

else{
	echo "Successfully Connected to the database!";
}

//Do your  db tasks here...

//example: inserting data into database 

//sql insertion 
$sql = "insert into department values('social science', 'woodland', 95000)";

//call to perform insertion (inform user of validity of insertion)
if($conn->query($sql)==TRUE){
	echo "<br/>"; //newline  
	echo "insertion successful"; 
}

else{
	echo "Error accessing the database: "$conn->error; 
}


//AFTER COMPLETION OF TASKS, TERMINATE THE CONNECETION
$conn->close(); 
?>
```
# Example
say we want to increase the budget of the math department by 5% 
```php
$sql="UPDATE department SET budget = budget * 1.05 WHERE dept_name = 'math'"

//running
if($conn->query($sql)==TRUE){
	echo "<br/>"; //newline
	echo "Sucess"
}

else {
	echo "<br/>";
	echo "Error accessing the DB: ".$conn->error; }
```

# Extracting Information From THE DB
```php
//show all rows from the department table
$sql="SELECT * FROM department"

//running (result now holds all the rows from the department table)
$result = $conn -> query($sql);

//Number of rows is an attribute of result
echo "<br/>Total rows: $result->num_rows<br/>"; 

//displaying rows individually
if($result->num_rows){
	//Display
	//output the data of each row using a loop
	while($row = $result -> fetch_assoc()) { 
		echo "Dep name: ".$row["dept_name"]." Building: ".$row["building"]." Budget: ".$row["budget"].<br/>;
	}

else{
	echo "zero results";
}

```





