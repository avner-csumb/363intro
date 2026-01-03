---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
title: "Lecture 1: Welcome"
info: CST 363
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
mdc: true
---

# Welcome to Slidev

Presentation slides for developers

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

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



# About the course

<v-clicks>

- Review syllabus
  - Texts/Readings  
  - Exercises, Homework, Exams

- This course teaches you the concepts of a database system and applies the algorithms you learned in data structures in programming assignments related to database systems.

</v-clicks>



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

- Try to do the reading early in the week
  - O'Reilly Books (<a href="https://docs.google.com/document/d/1saT8iMSDjfODRiKfCHfbSfZgvfUoMS7w_VQm6FDnHmY/edit?usp=sharing" target="_blank">link</a>)

  

---

# Purpose of Database (1 of 2)

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

# Purpose of Database (2 of 2)

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

# Terminology (cont.)

- Relation – a table in a relational database
  - Table, relational table, relation all mean the same thing.
  - Row, record, tuple all mean the same thing.
  - Column, field, attribute all mean the same thing.
    - Values of a column have the same datatype.
  - IMPORTANT: Within each row, columns are single valued.


---

# Terminology


Example of relational and  non-relational tables


![](/images/img1.png){class="w-90"}


---

# Relational Model

- All the data is stored in various tables.
  - Other data models use trees, graphs or map structures.

---

# Relational Model (cont.)

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





---
transition: fade-out
---

# Week 1 — Introduction to Database Systems
**CST 363 (16-week Undergraduate Course)**

- What a DBMS is and why we use it
- Relational model basics + core terminology
- Keys and relationships
- SQL overview and categories
- High-level DBMS architecture
- Tooling: PostgreSQL workflow

---

# Learning Objectives (Week 1)
By the end of this week, you should be able to:

- Explain what problems DBMSs solve vs file-based storage
- Define physical vs logical data independence
- Use correct relational terminology (relation/tuple/attribute)
- Identify primary keys and foreign keys (and related key types)
- Recognize major SQL categories (DDL/DML/DQL/DTL/DCL)
- Describe DBMS components at a high level
- Set up and use PostgreSQL tooling (CLI/GUI + containerized setup)


---

# Why Databases Exist

<div class="p-2">

<v-clicks>

**File-based approach limitations**
- Hard to share data safely across apps and users
- Redundancy → inconsistency (multiple copies of “truth”)
- Updates can be expensive and error-prone
- Concurrency issues (simultaneous reads/writes)
- Recovery is difficult (partial updates, crashes)
- Security is ad hoc (access control not centralized)

</v-clicks>



<v-clicks>

**DBMS value proposition**
- Centralized, shared data
- Integrity constraints enforced consistently
- Concurrency control + transactions
- Backup/recovery mechanisms
- Fine-grained authorization

</v-clicks>

</div>


---

# Data Independence (Key DBMS Benefit)
**Physical data independence**
- Change how data is stored (files, indexes, partitions)
- Applications don’t need to change

**Logical data independence**
- Change the logical schema (add attributes/tables, create views)
- Existing applications and queries can remain stable

---

# Data Models: How We Got Here
A quick evolution of modeling and querying capabilities:

- **Hierarchical (1960s):** tree navigation, rigid parent-child structure
- **Network (1970s):** graph-like pointers/links, complex navigation
- **Relational (1980s):** tables + declarative queries (SQL)
- **Object (1990s):** object concepts integrated with persistence
- **Graph (2000s):** vertex/edge model for highly connected data
- **Document (2010s):** JSON/XML, flexible schema for semi-structured data

---

# Relational Model: The Big Idea
- Represent data as **tables** (relations)
- Work with data using **set-based** operations (not pointer traversal)
- Support many “views” (queries) over the same stored data
- Enforce correctness through constraints (keys, referential integrity, etc.)

---

# Core Relational Terminology (Synonyms)
- **Table = Relation**
- **Row = Tuple = Record**
- **Column = Attribute = Field**
- **Data type = Domain**

Practical takeaway:
- Be fluent in both the academic terms and the SQL/table terms.

---

# What Makes a Table “Relational”?
Relational tables assume:
- Each column has a defined domain/type
- Each row is a tuple of single-valued attributes
- Relations can be combined via joins using keys

Contrast:
- Document/JSON can naturally embed nested objects and arrays.

---

# Keys: Why They Matter
Keys provide **identity** and **relationships**.

- **Primary key (PK):** uniquely identifies each row
- **Foreign key (FK):** references a PK in another table

Why keys matter:
- Joins become meaningful
- Integrity rules can be enforced (no “dangling” references)
- Reduces duplication and update anomalies

---

# Key Vocabulary (More Precise)
- **Superkey:** any set of columns that uniquely identifies a row
  - may contain extra attributes
- **Candidate key:** minimal superkey (no redundant columns)
- **Primary key:** chosen candidate key used as the main identifier
- **Foreign key:** attribute(s) that reference a key in another relation

---

# View-Neutral Storage (Store Once, Ask Many Questions)
A DBMS stores data in a way that supports many different outputs:

- Store transactional detail once (e.g., receipts / line items)
- Generate many views/reports:
  - monthly totals
  - top-selling products
  - sales by region
  - customer purchase history

Key point:
- Do not store data “pre-baked” into a single report format.

---

# Relational vs Document Example (Conceptual)
**Relational style**
- Normalize across tables (Customer, Order, OrderItem)
- Use joins to reassemble for queries

**Document style (JSON)**
- Nested objects (compound attributes)
- Arrays (multi-valued attributes), e.g., list of items in an order
- Flexible schema can be convenient, but integrity and querying differ

---

# SQL: Major Categories (You Must Recognize)
- **DDL (Data Definition Language):** define schema
  - `CREATE TABLE`, `ALTER TABLE`
- **DQL (Data Query Language):** query data
  - `SELECT ... FROM ... WHERE ...`
- **DML (Data Manipulation Language):** modify data
  - `INSERT`, `UPDATE`, `DELETE`
- **DTL (Data Transaction Language):** control transactions
  - `BEGIN`, `COMMIT`, `ROLLBACK`
- **DCL (Data Control Language):** permissions/security
  - `GRANT`, `REVOKE`, user/role management

---

# SQL Literacy: Basic Language Elements
Know the building blocks:

- **Keywords:** `SELECT`, `FROM`, `WHERE`
- **Identifiers:** table/column names
- **Literals:** `'text'`, `123`, `TRUE`
- **Expressions:** `price * quantity`
- **Comments:**
  - single-line: `-- comment`
  - block: `/* comment */`

---

# Common Data Types (PostgreSQL Examples)
Expect to see:

- Numeric: `INTEGER`, `REAL`, `NUMERIC`
- Text: `VARCHAR`, `TEXT`
- Time: `TIMESTAMP`
- Binary: `BYTEA`
- Semi-structured: `JSON/JSONB`, `XML`
- Extensions: `GEOMETRY` (PostGIS)

---

# DBMS Architecture (High-Level Map)
Two big subsystems:

**Query Processor**
- Parse/validate SQL
- Optimize query plan
- Execute plan

**Storage Manager**
- Manage files/pages on disk
- Buffer/cache pages in memory
- Enforce authorization and integrity
- Manage transactions (concurrency + recovery)

Also includes:
- Data dictionary (metadata)
- Indexes
- Statistics for optimization

---

# Tooling: PostgreSQL + How You’ll Work
Typical workflow options:

**CLI: `psql`**
- Fast, scriptable, good for reproducibility
- Works well with labs and automated checks

**GUI: pgAdmin**
- Helpful for browsing and visual inspection
- More setup and heavier resource usage

---

# Tooling: Containerized Setup (Conceptual)
Using Docker (conceptually):
- Start a PostgreSQL container
- Connect via `psql` (or pgAdmin)
- Create databases/tables, run SQL scripts, query results

Why containers:
- Consistent environment across student machines
- Easier resets and troubleshooting

---

# Week 1 Summary
You should now be able to:
- Explain what DBMSs provide (independence, integrity, concurrency, recovery, security)
- Use relational terminology correctly
- Identify and apply key concepts (PK/FK, candidate keys)
- Categorize SQL statements by purpose
- Describe DBMS components at a block-diagram level
- Choose and use a PostgreSQL workflow (CLI/GUI), typically via Docker

---

# Looking Ahead (Weeks 2–4 Preview)
- ER modeling and conceptual design
- Relational schema mapping
- SQL querying fundamentals (joins, grouping, constraints)
- Normalization and design quality tradeoffs

---


# What is Slidev?

Slidev is a slides maker and presenter designed for developers, consist of the following features

- 📝 **Text-based** - focus on the content with Markdown, and then style them later
- 🎨 **Themable** - themes can be shared and re-used as npm packages
- 🧑‍💻 **Developer Friendly** - code highlighting, live coding with autocompletion
- 🤹 **Interactive** - embed Vue components to enhance your expressions
- 🎥 **Recording** - built-in recording and camera view
- 📤 **Portable** - export to PDF, PPTX, PNGs, or even a hostable SPA
- 🛠 **Hackable** - virtually anything that's possible on a webpage is possible in Slidev
<br>
<br>

Read more about [Why Slidev?](https://sli.dev/guide/why)

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---
transition: slide-up
level: 2
---

# Navigation

Hover on the bottom-left corner to see the navigation's controls panel, [learn more](https://sli.dev/guide/ui#navigation-bar)

## Keyboard Shortcuts

|                                                     |                             |
| --------------------------------------------------- | --------------------------- |
| <kbd>right</kbd> / <kbd>space</kbd>                 | next animation or slide     |
| <kbd>left</kbd>  / <kbd>shift</kbd><kbd>space</kbd> | previous animation or slide |
| <kbd>up</kbd>                                       | previous slide              |
| <kbd>down</kbd>                                     | next slide                  |

<!-- https://sli.dev/guide/animations.html#click-animation -->
<img
  v-click
  class="absolute -bottom-9 -left-7 w-80 opacity-50"
  src="https://sli.dev/assets/arrow-bottom-left.svg"
  alt=""
/>
<p v-after class="absolute bottom-23 left-45 opacity-30 transform -rotate-10">Here!</p>

---
layout: two-cols
layoutClass: gap-16
---

# Table of contents

You can use the `Toc` component to generate a table of contents for your slides:

```html
<Toc minDepth="1" maxDepth="1" />
```

The title will be inferred from your slide content, or you can override it with `title` and `level` in your frontmatter.

::right::

<Toc text-sm minDepth="1" maxDepth="2" />

---
layout: image-right
image: https://cover.sli.dev
---

# Code

Use code snippets and get the highlighting directly, and even types hover!

```ts [filename-example.ts] {all|4|6|6-7|9|all} twoslash
// TwoSlash enables TypeScript hover information
// and errors in markdown code blocks
// More at https://shiki.style/packages/twoslash
import { computed, ref } from 'vue'

const count = ref(0)
const doubled = computed(() => count.value * 2)

doubled.value = 2
```

<arrow v-click="[4, 5]" x1="350" y1="310" x2="195" y2="342" color="#953" width="2" arrowSize="1" />

<!-- This allow you to embed external code blocks -->
<<< @/snippets/external.ts#snippet

<!-- Footer -->

[Learn more](https://sli.dev/features/line-highlighting)

<!-- Inline style -->
<style>
.footnotes-sep {
  @apply mt-5 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>

<!--
Notes can also sync with clicks

[click] This will be highlighted after the first click

[click] Highlighted with `count = ref(0)`

[click:3] Last click (skip two clicks)
-->

---
level: 2
---

# Shiki Magic Move

Powered by [shiki-magic-move](https://shiki-magic-move.netlify.app/), Slidev supports animations across multiple code snippets.

Add multiple code blocks and wrap them with <code>````md magic-move</code> (four backticks) to enable the magic move. For example:

````md magic-move {lines: true}
```ts {*|2|*}
// step 1
const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})
```

```ts {*|1-2|3-4|3-4,8}
// step 2
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  }
}
```

```ts
// step 3
export default {
  data: () => ({
    author: {
      name: 'John Doe',
      books: [
        'Vue 2 - Advanced Guide',
        'Vue 3 - Basic Guide',
        'Vue 4 - The Mystery'
      ]
    }
  })
}
```

Non-code blocks are ignored.

```vue
<!-- step 4 -->
<script setup>
const author = {
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
}
</script>
```
````

---

# Components

<div grid="~ cols-2 gap-4">
<div>

You can use Vue components directly inside your slides.

We have provided a few built-in components like `<Tweet/>` and `<Youtube/>` that you can use directly. And adding your custom components is also super easy.

```html
<Counter :count="10" />
```

<!-- ./components/Counter.vue -->
<Counter :count="10" m="t-4" />

Check out [the guides](https://sli.dev/builtin/components.html) for more.

</div>
<div>

```html
<Tweet id="1390115482657726468" />
```

<Tweet id="1390115482657726468" scale="0.65" />

</div>
</div>

<!--
Presenter note with **bold**, *italic*, and ~~striked~~ text.

Also, HTML elements are valid:
<div class="flex w-full">
  <span style="flex-grow: 1;">Left content</span>
  <span>Right content</span>
</div>
-->

---
class: px-20
---

# Themes

Slidev comes with powerful theming support. Themes can provide styles, layouts, components, or even configurations for tools. Switching between themes by just **one edit** in your frontmatter:

<div grid="~ cols-2 gap-2" m="t-2">

```yaml
---
theme: default
---
```

```yaml
---
theme: seriph
---
```

<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-default/01.png?raw=true" alt="">

<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-seriph/01.png?raw=true" alt="">

</div>

Read more about [How to use a theme](https://sli.dev/guide/theme-addon#use-theme) and
check out the [Awesome Themes Gallery](https://sli.dev/resources/theme-gallery).

---

# Clicks Animations

You can add `v-click` to elements to add a click animation.

<div v-click>

This shows up when you click the slide:

```html
<div v-click>This shows up when you click the slide.</div>
```

</div>

<br>

<v-click>

The <span v-mark.red="3"><code>v-mark</code> directive</span>
also allows you to add
<span v-mark.circle.orange="4">inline marks</span>
, powered by [Rough Notation](https://roughnotation.com/):

```html
<span v-mark.underline.orange>inline markers</span>
```

</v-click>

<div mt-20 v-click>

[Learn more](https://sli.dev/guide/animations#click-animation)

</div>
