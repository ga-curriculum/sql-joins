# ![SQL Joins - Building Data Models](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to design and implement database schemas using table normalization techniques and perform queries that leverage joins to retrieve data from multiple tables.

## Data modeling

It's unusual to have just one table. Typically, there are many tables to represent data in a meaningful and useful way.


Let's image we are designing an ice cream manufacturing management system.

We can start by thinking of the logistics of making one type of ice cream. What kind of data would we need?

First, just the name of the ice cream: 'Plain'

'Plain' ice cream is made up of
- milk
- sugar
- cream

We then have to think of how much of each ingredient goes into a pint

|Milk|Sugar| Cream|
|:-:|:-:|:-:|
|480ml|143g| 240ml |


Since we're manufacturing lots of ice cream. It would be useful to also have data on how much of these ingredients we have on hand

|Milk|Sugar| Cream|
|:-:|:-:|:-:|
|500l|14000g| 20l |


We want to keep track of how many pints we've sold


|Flavor| Pints Sold |
|:-:|:-:|
|Plain | 543 |

And how many Pints we have on hand

|Flavor| Pints in Storage |
|:-:|:-:|
|Plain | 5500 |

We'd also want to keep track of how much money we're making and how much money we're spending to keep operations going...

Having separate tables is useful. But also being able to join our tables together and look at our data in order to analyze it would be really useful as well.

We might want to look at
- how many pints we have in storage vs sold to determine if we are making too much or too little

- do we want to branch out to more flavors and keep track of how much of each ingredient we have and if we have enough for each flavor?

- We might want to look at sales from one quarter to another

- Compare sales in different states/cities

If we're just a small company we can probably get away with using excel spreadsheets. But there is a tipping point where excel just isn't powerful/useful enough.

Splitting data across multiple tables often referred to as normalization.

## Our first table

Let's make a table that holds important information about our ice cream.

Let's say we're ready to branch out to 5 more flavors (we are currently advertising for a marketing person to assist with better ice cream names)
- plain
- coffee
- strawberry
- peanut butter
- vanilla
- chocolate

What other info is useful? For now let's list how many pints we have in storage and whether or not the ice cream has nuts in it.


We also will add a `SERIAL PRIMARY KEY`, this means that each entry will get a unique key

(SERIAL is a pseudo datatype, which is 4 bytes and ranges from 1 to 2,147,283,647) and increments [more info](http://www.postgresqltutorial.com/postgresql-serial/).

Primary Key adds constraints (like checking that the number is unique and not null)


If you don't have `psql` open: Then in bash type 
 - `createdb sql_ice_cream`
 - `psql sql_ice_cream`

If you already have psql open:

```sql
CREATE DATABASE sql_ice_cream;
\c sql_ice_cream
```

Everyone now:

```sql
CREATE TABLE ice_creams (id SERIAL PRIMARY KEY, name VARCHAR(144), pints INT, has_nuts BOOLEAN DEFAULT false);

INSERT INTO ice_creams (name, pints, has_nuts) VALUES
('Plain', 554, false),
('Blueberry', 821, false ),
('Strawberry', 932, false),
('Peanut Butter', 22, true),
('Vanilla', 404, false),
('Chocolate', 203, false);
SELECT * FROM ice_creams;
```

