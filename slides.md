---
theme: default
background: https://cover.sli.dev
title: "Lecture 1: Welcome"
info: CST 363
class: text-center
drawings:
  persist: false
mdc: true
---

# Introduction to Database Systems

CST 363


---

## About CST 363

<div class="p-2">


<v-clicks>

- An intensive, hands-on introduction to database systems blending theory, design, and implementation.

- Topics include the relational model, conceptual modeling (ER), SQL from basics to advanced analytics, and the internals of storage, indexing, and transactions

- Also covered: distributed and non-relational systems (MongoDB, Redis), geospatial data (PostGIS/MongoDB), and abstraction layers (ORM)

</v-clicks>

</div>

---



## About the course

<div class="p-2">


<v-clicks>

- Review syllabus
  - Texts/Readings  
  - Exercises, Homework, Exams

- This course teaches you the concepts of a database system and applies the algorithms you learned in data structures in programming assignments related to database systems.

</v-clicks>

</div>



---

# Database Model Evolution

<div class="p-2">


<v-clicks>

- A story of how humans wanted to **represent** and **query** information more *naturally*, *flexibly*, and *efficiently* over time 

- Early databases were very rigid and/or difficult to navigate
  - one record ("child") could only have one parent → duplicate records
  - hierarchy had to be traversed in order
  - lack of declarative queries

</v-clicks>

</div>



---


# About required readings

<div class="p-2">


- Try to do the reading early in the week
  - O'Reilly Books (<a href="https://docs.google.com/document/d/1saT8iMSDjfODRiKfCHfbSfZgvfUoMS7w_VQm6FDnHmY/edit?usp=sharing" target="_blank">link</a>)

  
</div>

---

# Purpose of a Database (1 of 2)

<div class="p-2">


<v-clicks depth="2">


- Physical Data Independence – can change how data is physically stored without affecting the applications that use the database
- Logical Data Independence
  - Add new data elements without breaking existing applications.
  - File based systems (pre-DBMS) tightly coupled to file formats
- Allows you to retrieve the same data in different ways

</v-clicks>

</div>


---

# Purpose of a Database (2 of 2)

<div class="p-2">

<v-clicks depth="2">

- Other benefits 
  - Shared, centralized data instead of isolated program files
  - Reduced data redundancy and inconsistency
  - Data integrity is enforced by database and is consistent across programs

</v-clicks>


<v-clicks depth="2">

- Update file records in place without rewriting the entire file
  - record size may change
- Recovery from failure and partial update
- Concurrent access by multiple programs
- Security – provide access to some, but not all, the data



</v-clicks>

</div>

---


# Terminology


<div class="p-2">

<v-clicks depth="3">

- Data Model
  - Defines how data is structured, stored, and manipulated in a DBMS
  - Examples
    - Hierarchical / Network: Lists, Trees, Graphs
    - Object-oriented: Records, Objects
  - Relational Data Model  (main course focus)
    - Data is stored as rows and columns in tables. Based on mathematical set theory.

</v-clicks>

</div>

---

## Terminology (cont.)

<div class="p-2">

<v-clicks depth="3">


- Relation – a table in a relational database
  - Table, relational table, relation all mean the same thing.
  - Row, record, tuple all mean the same thing.
  - Column, field, attribute all mean the same thing.
    - Values of a column have the same datatype.
  - IMPORTANT: Within each row, columns are single valued.

</v-clicks>

</div>

---

## Terminology


Example of relational and  non-relational tables


![](/images/img1.png){class="w-90"}


---

## Relational Model


<div class="p-2">

- All the data is stored in various tables.
  - Other data models use trees, graphs or map structures.

</div>

---

## Relational Model (cont.)

Example of tabular data in the relational model


![](/images/img2.png){class="w-90"}


---

## How to identify a row in relation — Keys

<div class="p-2">

<v-clicks depth="2">

- **primary key** – a minimal set of columns that uniquely identify a row
  - Example:  `department.dept_name`
- **foreign key** – a column (or set of columns) that refers to a row in another table using the primary
  - key of the target row
  - Example: `course.dept_name` → references `department.dept_name`

</v-clicks>

</div>

---

## Other Keys


<div class="p-2">

<v-clicks depth="2">

- **Super keys** - column or columns that identify a row
  - Any column(s) that uniquely identify a row
  - May include extra, unnecessary attributes
  - Every primary key is a super key (but not vice versa)


- **Candidate keys** - an alternate minimal set of columns that identify a row
  - Example:  `student_email`
  - From the set of Candidate Keys, one is chosen as the Primary Key

</v-clicks>

</div>

---

## Data in the real world


![](/images/img3.png){class="w-90"}


---


- A column such as `customerid` in the SalesTransaction table is  the "primary key" value of another row and serves as a link to that row. 
- The `customerid` column in SalesTransaction is a "foreign key".


<div class="grid grid-cols-2 gap-4">
  <div>

`customer`
![](/images/customer.png){class="w-50"}


`sales_transaction`
![](/images/sales_transaction.png){class="w-50"}

`product`
![](/images/product.png){class="w-50"}
  
  </div>
  <div>


`includes`
![](/images/includes.png){class="w-50"}


</div>
</div>


---
layout: image
image: /images/connections.png
backgroundSize: 30em
---



---

## An alternate view of the same data

Rather than storing data according to a particular view, data is stored in a “view neutral” format.  Data can be combined into many different views depending on the needs of the user.


![](/images/monthly.png){class="w-90"}



---

## Non-relational Model

MongoDB uses JSON as a Data Model

```json
{
   "tid": "T444",
   "customer": {
     "first": "Pam",
     "last": "Paterson"
   },
   "date": "2020-01-01",
   "total": 230.00,
   "items": [
     {
       "item": "Easy Boot", "sku": "2x2", "qty": 2, "unit": 70
     },
     {
       "item": "Dura Boot", "sku": "1x1", "qty": 1, "unit": 90
     }
   ]
 }

```

---
layout: image
image: /images/more_json.png
backgroundSize: 30em
---


## HW: In-memory tables to optimized data retrieval

- Five part homework series which uses Python to build foundation understanding of database systems.
- HW1–HW2 → Data dictionary + tuples (DDL/Schema & rows)
- HW3 → Query evaluation engine (predicates & joins)
- HW4 → Storage manager (file & buffer notions) + disk layout
- HW5 → Indices (ordered access path) + faster lookups





---

## Database Architecture


![](/images/storage.png){class="w-90"}

---

## About PostgreSQL

- Open source and no corporate overlord
- ACID compliance – data integrity with robust transactional support
- Closely follows SQL standard
- Supports JSON and JSONB for semi-structured data 
- Battle-tested with strong community support
- Extensibility with Python
  - Supports server-side programming through PL/Python extension,


---


## PostgreSQL Demo

- Run PostgreSQL in a Docker container
  - Instal Docker (if you don’t already have it)
    - Easiest way is with Docker Desktop (scroll down on page) – can skip “Sign In”
  - From terminal emulator (Terminal app on Mac/Linux, PowerShell on Windows):

```bash
docker run --name cst363-postgres 
-e POSTGRES_PASSWORD=ott3r 
-p 5431:5432 
-d postgres
```

---

## PostgreSQL Command Line Interface

<div class="p-2">

<v-clicks depth="2">

- Text-Based Interface: Operates entirely from the command line, suitable for scripting and automation.
- Lightweight: No GUI overhead, making it fast and resource-efficient.
- Advanced Querying: Allows users to write and execute SQL queries directly.
- Script-Friendly: Ideal for running SQL scripts and batch operations.
- Default PostgreSQL Tool: Installed with PostgreSQL, no additional setup required.

</v-clicks>


</div>


---

## pgAdmin GUI


- https://www.pgadmin.org/download/
- Graphical Interface: User-friendly GUI for database management and querying.
  - Visual Schema Management: Provides tools for visualizing and editing database schemas, tables, and relationships.
  - Cross-Platform: Available as a desktop app or web app, accessible on various operating systems.
- Less Script-Friendly: Not as efficient for automation or batch operations.
- Resource-Intensive: Requires more system resources compared to psql.
- Additional Setup: Requires separate installation and configuration.


