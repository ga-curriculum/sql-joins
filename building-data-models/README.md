<h1>
  <span class="headline">SQL Joins</span>
  <span class="subhead">Building Data Models</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to design and implement database schemas using table normalization techniques.

## Data modeling

In a real-world application, it's unusual to have just one table for your data. Typically, we use multiple tables to represent data in a meaningful and useful way. This practice helps in organizing data efficiently, ensuring data integrity, and making data retrieval easier.

### Designing a "simple" system

To explore this idea, let's imagine we're designing a system to manage ice cream production. What kinds of data would we need to keep track of?

We’ll start with just one flavor: **Plain**.

'Plain' ice cream is made with:

- milk
- sugar
- cream

And it's usually sold in the quantity of a **pint**.

### What is a pint?

A **pint** is a unit of volume commonly used in recipes and food production. In this lesson, we’ll treat 1 pint as about **480 milliliters (ml)** — roughly **half a liter** or **two cups**.

This helps standardize ingredient amounts and makes it easier to work with our ice cream data.

### Ingredients per pint

We need to know how much of each ingredient is required to make one pint of ice cream. This is important for both production and inventory tracking. For 'Plain' ice cream, let’s assume the following amounts:

| Milk  | Sugar | Cream |
| :---: | :---: | :---: |
| 480ml | 143g  | 240ml |

Since we're producing large quantities of ice cream, it’s also helpful to know how much of each ingredient we currently have in stock:

| Milk | Sugar  | Cream |
| :--: | :----: | :---: |
| 500l | 14000g |  20l  |

We want to keep track of how many pints we've sold:

| Flavor | Pints Sold |
| :----: | :--------: |
| Plain  |    543     |

And how many Pints we have on hand:

| Flavor | Pints in Storage |
| :----: | :--------------: |
| Plain  |       5500       |

We'd also want to keep track of how much money we're making and how much money we're spending to keep operations going...

Having separate tables is useful. But also being able to join our tables together and look at our data in order to analyze it would be really useful as well.

We might want to look at:

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

(SERIAL is a pseudo datatype, which is 4 bytes and ranges from 1 to 2,147,283,647) and increments [more info](https://neon.tech/postgresql/postgresql-tutorial/postgresql-serial).

Primary Key adds constraints (like checking that the number is unique and not null)

If you don't have `psql` open: Then in your terminal type:

```bash
createdb sql_ice_cream
psql sql_ice_cream
```

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
