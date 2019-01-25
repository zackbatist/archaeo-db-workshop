# archaeo-db-workshop notes

## Section 1 - About this workshop [10 minutes]
This two-hour workshop will focus on fundamental aspects of database design

If all goes according to plan, you will understand:

* what a database is, and
* how it relates to archaeological workflows

In practical terms, you will:

* understand how to design and maintain effective data structures
* understand how to input, modify and retrieve data
* begin creating your own database for your own purposes
* become a somewhat profficient user of the command line and develop practical computing skills

As an introductory overview, no prior knowledge or experience is expected.

However things will also get technical, so **please ask questions if you have them!**

This is my first time doing such a workshop, so please let me know if you need me to slow down, or if some concepts need to be explained in more depth.

I will do my best to accomodate, though there is a lot of material to cover in only 2 hours.

That being said, there will be opportunities to provide feedback about my performance after the session.

### Workshop Structure / Logistics
We'll be weaving in and out of lecture-style explanations and more active work, where you will be gradually applying your skills to meet your own particular needs

Some of these skills develop through repeated use, but I'd be glad to extend this into other sessions depending on the outcome of today

I've made a little website, where you can find these slides, my notes and links to other helpful resources

There is also a link to an etherpad, which is like a shared notepad that we will be using later on in this session

### About me
So a little about me and my experiences working with databases before we begin:

+ I have a background doing network analysis and GIS work during my MA thesis
+ I like lithics
+ I like using R to code cool things relating to lithics
+ My current research is about the different ways in which archaeologists manage data and make it useful in a variety of ways
+ However, this workshop is largely based on my experiences managing the databases for the Stelida Naxos Archaeological Project, which I've been doing for the past 3.5 years
  + It's a gradual process of learning on the job, a patchwork of experiences

### About you
+ You maintain or plan on maintaining an extensive amount of tabular data
+ You want to learn how to manage this data more effectively
+ You're keen to hone your digital skillset and/or develop more structured digital workflows


## Section 2 - What is a database? [10-15 minutes]
### What is a database?
Wikipedia says:
> A database is an organized collection of data, generally stored and accessed electronically from a computer system

More specifically, a system comprising three main components:
- Database Management System [DBMS]
- Database Schema
- Data

### Database Management System
The database management system -- or DBMS for short -- is the software that interacts with end users, applications, and the database itself to capture and analyze the data

It has 4 main functions:
- **Data definition** – Creation and modification of the database schema, which frames how the data is organized
- **Update** – Insertion, modification, and deletion of the actual data, in ways that conform with the database schema
- **Retrieval** – Obtaining data from the database through a system of machine-readable commands
- **Administration** – Registering and monitoring users, enforcing security, monitoring performance, maintaining data integrity, dealing with concurrency control, and recovering corrupted information, etc

### Database Schema
The explicitly defined set of rules that structure the data and enable it to be input and retrieved in a systematic manner

Also sometimes referred to as architecture, structure, framework, etc

A few models exist, but **relational databases** are most prevalent in archaeology

#### Relational Databases
- Organizes data into a series of thematically-arranged tables, each consisting of intersecting columns and rows

- Rows are also called records

- Columns are also called variables or attributes

- Some columns contain values that are the same as the values in other tables, which helps us search across various tables

- For instance, we may want to retrieve all artefacts excavated by a particular excavator, but this information is not in the Artefacts table, so we use the common Context field to join together the different tables

- Certain columns designate unique aspects of the each record

- Fields like AR#, Trench, Context and LU are indexes, which I like to think of as independent variables, in relation to Location, Blank, Mod, Excavator and Soil Texture, which are dependent variables

### Data
- The contents of the database
- Must 'fit' the schema (overall architecture of the database)

### Questions?
This might be a good time to address some questions that you might have

## Section 3 - Setting up our DBMS
### Comparison of some DBMSs
These are some common database management systems. Each have pros and cons.

- **MariaDB / MySQL:** situated on a server, multi-user support, open source, DIY user interfaces
- **Microsoft Access / Apple FileMaker / LibreOffice Base:** serverless, built-in user interface, 'easy' form generation, proprietary/platform-dependent software, obscure variant of SQL/VisualBasic
- **SQLite:** serverless, is built into many common apps, open source
- **PostgreSQL / PostGIS:** emphasis on standards compliance, data preservation, etc
- **Neo4j:** graph database, extremely flexible, open source?

We will be using MariaDB/SQL. It is an extremely versatile system, with a very active user community and very good documentation available.

Like all professional software, there is a learning curve involved.

MariaDB may seem intimidating at first, especially compared with Microsoft Access, but I assure you that you will be better off this way.

All of these systems are actually very similar, however Microsoft Access obfuscates many of the fundamental components of database design and maintenance

If you want to learn transferable skills, and have the capability to extend your computational skillsets in the future, you need to know what is going on under the hood, and be able to describe what's going on in more broadly-understood terms

That being said, this may be a bit of a technical jump for some people. Please feel free to ask questions as we move along.

### MariaDB Server setup
Database is on a *server*, which is accessed by multiple *clients*

A server is a specialized computer that processes information and 'serves' it to and from various connected clients

The separation of server and client is what enables multi-user access

Data is centralized and unified, therefore also consistent among users

Microsoft Access and SQLite are also centralized databases, but are not located on an external server which inhibits multi-user access

Server could be out on the internet, on a local network, or even on the same machine as the client (though the latter tends to be for testing purposes only, not for 'live' use)

Mine is hosted on a cloud platform that offers an educational discount, located at St. Lawrence Market, I host other things on it too

[image of the stack]

To access the a database located on that remote server, we must engage in a two-step process:

1. we must access the remote computer, and login to it using the computer's login name and password
2. we must access the database management system, using a username and password that is specific to that program

It's a bit like entering your house, which requires one set of keys, and then opening up a cookie jar in your kitchen, which is locked using a different set of keys.

We could do all of this in a single process using a graphical client, or using the command line.

Whenever you press a button on a graphical user interface, you are actually issuing a command or series of commands to a computer. These commands can also be expressed as text, and this format allows the user to have more control over what they are asking the computer to do.

It's a bit like getting access to a breakfast buffet, rather than ordering off a fixed menu. Every action is deliberate, direct and self-contained.

It can seem intimidating at first, but you will find that it is actually a great way to interface with your computer.

#### Bash

Issuing commands requires that you provide 

Everything you do on your computer can be expressed on the command line. Usually when you press a button to do something, a series of commands are strung together into a bundled action.

Using the command line ensures that each action you make is intential, direct and self-contained, rather than bundled and opaque.

It's like getting access to the breakfast buffet rather than ordering off a fixed menu.

I'm only going to be doing a very basic overview, but there are fantastic resources out there where you can learn more.

Each command has a series of components: the command itself, flags/options, and arguments.

The command is usually a short abbreviation for the activity you want to perform, in this case `cp` stands for copy.

Flags are optional parameters that can be toggled to allow for slight variations in the command's functionality

Arguments are the entities or objects that are processed by the command.

Some flags must be paired with an argument, or require that arguments be formatted in certain ways.

The parameters for each command are documented, and are available on the fly by issuing the `man` command, which is short for manual.

In this case, we issue the command `cp` to copy files from one folder to another folder. The `-R` flag stands for recursive, and dictates that all files within the folder should be copied over, not just the folder itself.

There are some common conventions when using the command line, which we can go over more in-depth some other time.

#### SQL

Another command-oriented language i SQL, which stands for Structured Query Language.

SQL is used to interact with a relational database.

Each line of SQL is a self-contained logical statement that includes all parameters to do a particular action.

The end of the statement is indicated by a semicolon, and like bash, the computer will simply reject the command and do nothing if the command does not make logical sense.

SQL follows a very detailed syntax, or set of rules, that must be followed in order for a statement to make logical sense.

This will make more sense once we jump in, so let's try out a series of basic SQL statements, and compare them with GUI equivalents.

[show off a series of commands]

Now you guys can actually issue a command to create your own database. Follow the syntax on the screen, and hit shift+enter to run the command. Be sure to include the semicolon at the end of the statement.

Next let's go ahead and make a table in our own databases. First make sure that you're working within your own database by issueing the command `USE <databasename>;`

Then, follow the syntax displayed on the slides to create a sample table. You will have to come up with the names and data type for each column. We will be going into more depth later on in this workshop concerning specific parameters when creating tables.

Feel free to take notes or copy from a template that I've made up on our shared notepad: https://etherpad.wikimedia.org/p/archaeo-db-workshop

Verify that your work is being done properly by either running SQL commands or by using the GUI.