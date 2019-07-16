# Introduction to Data Modeling 

Data modeling is a game of abstraction.

## A good data model:
- captures all the data the system needs.
- captures ONLY the data the system needs.
- reflects reality.
- is flexible, and can evolve with the system.
- guarantee data integrity without sacrificing performance.
- is driven by the way we access data in the system.
- optimize last once you have a solid structure.

## Components:
- entities: the nouns, resources in REST terminology.
- properties: information we need to track about the entity.
- relationships: how they relate to each other.

## Workflow
- identify entities 
    * tables
- indentify properties for each entity 
    * columns
- identify relationships between two entities at a time 
    * foreign keys

Ideally you want to get to the JNF (third normal form).

Third normal form (3NF) is the third step in normalizing a database and it builds on the first and second normal forms, 1NF and 2NF.

3NF states that all column reference in referenced data that are not dependent on the primary key should be removed. Another way of putting this is that only foreign key columns should be used to reference another table, and no other columns from the parent table should exist in the referenced table.

----------------------------------------------------------------------

When building a database, what type of approach would you take?
In relationship terms, how would the entities look like? 
Look at the types of relationships below:

## Types of Relationships:
- one to one
- one to many <-- this is it
- many to many <-- a trick, smoke and mirrors

-----------------------------------------------------------------------

Now let's brainstorm an app that tracks your immunization.

For this, model your DB with this app:
[https://www.dbdesigner.net/]

## Immunization tracker:

- patient and staff point of view
- patient input info and not change it
- staff access all change some information
- track children imm.... records (parents, schools, doctor's office)

## Entities
- patient (any user will be a patient)
    * basic contact information
    * dependents
- immunization 
    * transactional (event occurs in time between two entities)
- vaccine
- appointments

- employees
- clinics

 Several employees work at the same clinic:
 - a clinic has several employees
 - the same employee can work in different clinics

-----------------------------------------------------------------------

## MANTRAS:
- every table has one and only one primary key
    * it could be made up of more than one column, called composite keys
- for one to many relationships, there are FK involved
- the FK goes in the many side
- for a many to many relationship we need a third table
- a many to many table can have extra information

## COMPOSITE KEYS:

A composite key is a combination of two or more columns in a table that can be used to uniquely identify each row in the table. When the columns are combined, uniqueness is guaranteed, but when it taken individually it does not guarantee uniqueness.

For example, here are three different tables:

The tracks table would have subjects like:
- Web Development
- iOS Development
- Android Development
- UX Development


        |      TRACKS         | 
        -----------------------
        ID (PK)  | INTEGER
        name     | VARCHAR(255)

The cohorts table would have subjects like:
- WEB19
- iOS11
- AND2
- UX7

        |         COHORTS         | 
        ---------------------------
        ID (PK)      | INTEGER
        name         | VARCHAR(255)
        track_id (FK)| INTEGER 

The students table would be like:

        |         STUDENTS         | 
        ---------------------------
        ID (PK)       | INTEGER
        name          | VARCHAR(255)
        cohort_id (FK)| INTEGER 

So it would flow like this:

Web Development --> WEB19 --> Mylynh Nguyen

But how can you guarantee uniqueness when one student changes cohorts? 
Or if they have multiple cohorts?

You would create a composite key, and remove the FK from students. With this method, you can also create multiple fields. This composite key connects each cohort with the unique students that you draw from. This would be between the students and cohort.


In the following table, date is optional (because you may be an accepted student but have yet to know your start date). This is called a junction table (usually used in many to many) that may have transactional data.
    
    |      COHORT_STUDENTS      | 
    -----------------------------
    ID (PK)        |    INTEGER
    cohort_id (FK) |    INTEGER
    student_id (FK)|    INTEGER
    start_date     |    DATE 
    finish_date    |    DATE 

Master and Transaction tables are needed in the database schema specially in the verticals of sales.

## [Master Data]: 

Data which seldom changes. For example, if a company has a list of 5 customer then they will maintain a customer master table having the name and address of the customers alongwith other data which will remain permanent and is less likely to change.

## [Transaction Data]: 
Data which frequently changes. For example, the company is selling some materials to one of the customer.So they will prepare a sales order for the customer. When they will generate a sales order means they are doing some sales transactions.Those transactional data will be stored in Transactional table.

This is really required to maintain database normalization.

Overall, once adding the transaction data, data flow would be like this:


Web Development --> WEB19 --> [Mylynh Nguyen, WEB19, 3/16/19, 10/31/19]

One --> Many --> Many 

------------------------------------------------------------------------

## Data Modeling

Several methods are provided which assist in building joins.

### JOIN STRUCTURE:
     .join(table, first, [operator], second)

For example, below we're joining the contacts and user table where the user_id would match the user.id. Then we're fetching the id and phone number.

    knex('users')
    .join('contacts', 'users.id', '=', 'contacts.user_id')
    .select('users.id', 'contacts.phone')

Outputs in SQL:

    SELECT users.id, contacts.phone
    FROM users 
    INNER JOIN contacts
    ON users.id = contacts.user_id



