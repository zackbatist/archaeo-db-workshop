# Section 1: About this workshop

## About this workshop

This two-hour workshop will focus on fundamental aspects of database design

If all goes according to plan, you will understand:

* what a database is, and
* how it relates to archaeological workflows

In practical terms, you will:

* understand how to design and maintain effective data structures
* understand how to input, modify and retrieve data
* begin creating your own database for your own purposes
* become a somewhat profficient user of the command line and develop practical computing skills

This is intended to be an active and participatory session

As an introductory overview, no prior knowledge or experience is expected

However things will get technical, **please ask questions if you have them!**

## Workshop Structure / Logistics
+ This is the general schedule that I hope to keep

+ We'll be weaving in and out of lecture-style explanations and more active work, where you will be gradually applying your skills to meet your own particular needs
+ Some of these skills develop through repeated use, but I'd be glad to extend this into other sessions depending on the outcome of today
+ Everything is on a little website I made, including slides, notes, datasets, etc

## About me
So a little about me and my experiences working with databases before we begin:

+ I have a background doing network analysis and GIS work during my MA thesis
+ I like lithics
+ I like using R to code cool things relating to lithics
+ My current research is about the different ways in which archaeologists manage data and make it useful in a variety of ways
+ However, this workshop is largely based on my experiences managing the databases for the Stelida Naxos Archaeological Project, which I've been doing for the past 3.5 years
  + It's a gradual process of learning on the job, a patchwork of experiences

## About you

+ You maintain or plan on maintaining an extensive amount of tabular data
+ You want to learn how to manage this data more effectively
+ You're keen to hone your digital skillset and/or develop more structured digital workflows

# Section 2: What is a database?

+ So let's get started by addressing the very basics:

## What is a database?
Wikipedia says:

> A database is an organized collection of data, generally stored and accessed electronically from a computer system

## More specifically, a system comprising three main components:
- Database Management System [DBMS]
- Database Schema
- Data

## Database Management System

The database management system -- or DBMS for short -- is the software that interacts with end users, applications, and the database itself to capture and analyze the data

It has 4 main functions:

- **Data definition** – Creation and modification of the database schema, which frames how the data is organized
- **Update** – Insertion, modification, and deletion of the actual data, in ways that conform with the database schema
- **Retrieval** – Obtaining data from the database through a system of machine-readable commands
- **Administration** – Registering and monitoring users, enforcing security, monitoring performance, maintaining data integrity, dealing with concurrency control, and recovering corrupted information, etc

## Database Schema
The explicitly defined set of rules that structure the data and enable it to be input and retrieved in a systematic manner

Also sometimes referred to as architecture, structure, framework, etc

A few models exist, but **relational databases** are most prevalent in archaeology

### Relational Databases
- Organizes data into a series of thematically-arranged tables, each consisting of intersecting columns and rows

- Rows are also called records

  - Columns are also called variables or attributes



    ==next slide==

  - Some columns contain values that are the same as the values in other tables, which helps us search across various tables

      - For instance, we may want to retrieve all artefacts excavated by a particular excavator, but this information is not in the Artefacts table, so we use the common Context field to join together the different tables


    ==next slide==

- Certain columns designate unique aspects of the each record

  - Fields like AR#, Trench, Context and LU are indexes, which I like to think of as independent variables, in relation to Location, Blank, Mod, Excavator and Soil Texture, which are dependent variables

## Data
- The contents of the database
- Must 'fit' the schema (overall architecture of the database)

==next slide==

+ Here's how the example schema would look filled in

## Questions?



# Section 3: Setting up our DBMS
## Comparison of some DBMSs
- **MariaDB / MySQL:** situated on a server, multi-user support, open source, DIY user interfaces
- **Microsoft Access / Apple FileMaker / LibreOffice Base:** serverless, built-in user interface, 'easy' form generation, proprietary/platform-dependent software, obscure variant of SQL/VisualBasic
- **SQLite:** serverless, is built into many common apps, open source
- **PostgreSQL / PostGIS:** emphasis on standards compliance, data preservation, etc
- **Neo4j:** graph database, extremely flexible, open source?

## MariaDB Server setup
- Database is on a *server*, which is accessed by multiple *clients*
- The separation of server and client is what enables multi-user access
- Data is centralized and unified, therefore also consistent among users
- Server could be out on the internet, on a local network, or even on the same machine as the client
- Mine is hosted on a cloud platform that offers an educational discount, located at St. Lawrence Market, I host other things on it too
[image of the stack]

## Using the command line
- We will be using the command line - *don't panic!*
- Every action you make can be expressed as a text-based command inputted into the command line
- This is the actual functionality that underlies the action of clicking on an icon
- However graphical interfaces tend to bundle things up in ways we don't always want them to be
  - e.g. it's like getting access to the breakfast buffet instead of ordering off the fixed menu
- Every action is intentional, direct, logged, and self-contained

### Bash
```bash
cp -R ~/files ~/files-backup
```



- Command
- Flags
- Values
- Directories and files
- Common symbols and conventions
  - avoid spaces in file names
  - no need for file names to have an extension
  - @ indicates specific users at a particular networked location
  - .. is like going up one directory
  - ~ is home directory
  - * is wild card
  - capitalization matters
  - up arrow key cycles through your most recent command

### SQL
- Stands for Structured Query Language
- Basically, self-contained logical statements that include all parameters needed to do a particular action
- There are various dialects, but the one used by MySQL and MariaDB is most commonly used
- Capitalizing SQL commands and variables is not required, but is conventional
- Semicolons indicate the end of a command
- If something doesn’t add up, the terminal will spit out an error and nothing will happen 
- Cheat sheets available at [url]

## Accessing our database server
- Using the command line:
  1. Access the remote computer via SSH
  ```
  ssh pi@<ip address>
  ```

  2. Access the MariaDB database server
  ```
  mysql -u MY_USERNAME -p
  ```

- Using a graphical client (for comparison)
[screenshot of it all filled in]

### Creating a database on the server
```
CREATE DATABASE odate1;
```

### Creating users and setting permissions
```
CREATE USER 'lara'@'localhost' IDENTIFIED BY 'croft';
GRANT ALL PRIVILEGES ON odate1.* TO 'lara'@'%' IDENTIFIED BY 'croft';
FLUSH PRIVILEGES;
```

# Section 4: Structuring the database
## Scoping tables
- Each table represents one kind of entity
- Rows represent instances of the entity
- Each instance has the same kinds of attributes, but different variations thereof
- Columns are assigned a *data type*
  - VARCHAR (variable-length string)
  - CHAR (fixed-length string)
  - INT (integer)
  - DEC (decimal number)
  - TEXT (long string of text)
  - BLOB (binary object up to a certain size)
  - DATE/TIME/YEAR (date/time/year)

## Delimiting indexes
- Indexes indicate an independent variable or set of variables, in relation to their attributes
- Sometimes referred to as keys
- Can be set to require that each instance be unique
- Each table has a primary index, which must be unique
**Pro Tip:** to ensure unique values, user *sequential integers* or *time stamps* since each 'step' is guaranteed to be unique!

## Defining relationships
- Relationships indicate that the values in one index are equivalent to the values in another index
  - i.e. the records in each index relate to each other via their indexes
- Records must relate variables of the same data type

## Importing data from spreadsheets
- Data must conform to data types specified when creating the table
- Most effort is wrangling the data in excel
- Export data to csv (comma separated values) from excel

## Now do it!
### Creating tables:
```
CREATE TABLE `odate1`.`contexts` (
`id` INT(11) UNSIGNED NOT NULL AUTO_INCREMENT,
`Context` VARCHAR(255) DEFAULT '',
`Trench` VARCHAR(255) DEFAULT '',
`ContextDescription` VARCHAR(255) DEFAULT '',
`Munsell` VARCHAR(255) DEFAULT '',
`SedimentColour` VARCHAR(255) DEFAULT '',
`NumberOfBuckets` INT(11) DEFAULT 0,
PRIMARY KEY (`id`)
);
```

### Defining indexes:
```
CREATE INDEX index_name
ON table_name (column1, column2, ...); 
```

OR

```
CREATE UNIQUE INDEX index_name
ON table_name (column1, column2, ...); 
```

### Defining relationships:
```
ALTER TABLE `odate1`.`contexts` ADD CONSTRAINT `FK_contexts_Trench` FOREIGN KEY (`Trench`) REFERENCES `odate1`.`contexts` (`Trench`) ON DELETE CASCADE ON UPDATE CASCADE;
```

# Break / questions

# Section 5: INSERT, UPDATE and SELECT queries
- Everything you do is expressed as a self-contained logical statement
- There are 3 fundamental commands: INSERT, UPDATE and SELECT

## INSERT
- Inserts records into a table
```
INSERT INTO `odate1`.`contexts` (Context, Trench, ContextDescription, Munsell, SedimentColour, NumberOfBuckets)
VALUES (0001, 001, "The first context of the season. Loamy sand, very herbaceous, characteristic of a typical surface layer.","5YR 3/3",NULL,3);
```

## UPDATE
- Modifies cells within a table
```
UPDATE `odate1`.`contexts`
SET `SedimentColour` = "Dark Brown"
WHERE `Munsell` = "5YR 3/3";
```

## SELECT
- Retrieves data from a table
```
SELECT `Context`, `Munsell`, `SedimentColour`
FROM `contexts`
WHERE `contexts`.`Trench` = 001;
```

## DELETE
- Deletes a record
```
DELETE FROM `contexts`
WHERE `Context` = "0005";
```

## JOIN
- Used as optional component of SELECT queries when you want to retrieve related data that spans multiple tables
- Four varieties of joins:
  - (INNER) JOIN: Returns records that have matching values in both tables
  - LEFT (OUTER) JOIN: Return all records from the left table, and the matched records from the right table
  - RIGHT (OUTER) JOIN: Return all records from the right table, and the matched records from the left table
  - FULL (OUTER) JOIN: Return all records when there is a match in either left or right table
[JOIN venn diagrams]

```
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```

