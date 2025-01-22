<h1>
  <span class="headline">SQL Joins</span>
  <span class="subhead">One-to-Many Relationship</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to understand the core principles of relational data and apply one-to-many relationships to model data effectively.

## Relational data

Above we started to think about our ice cream manufacturing data.

What kind of relations do we need with our ice creams?

One ice cream has many plants it is manufactured in. Due to concerns about allergies (and simplicity) Each plant can only manufacture one ice cream

We could make new columns for our plants

|    Flavor     | Pints Sold | Plant 1 | Plant 2 | Plant 3 |
| :-----------: | :--------: | :-----: | :-----: | :-----: |
|     Plain     |     18     |    A    |    B    |    C    |
|   Chocolate   |    120     |    M    |    E    |    F    |
|   Blueberry   |    674     |    G    |    S    |         |
|  Strawberry   |     88     |    J    |    Q    |         |
| Peanut Butter |    273     |    K    |         |         |
|    Vanilla    |     5      |    H    |    N    |    P    |
|   Chocolate   |    444     |    H    |    N    |    P    |

We already have at least two problems:

- as our business grows we're going to need more and more plants, will our columns expand infinitely? How would we keep them organized? What if one plant closes? Do we move the other plants in that row over?
- Where is each plant? How many pints can it generate every month? We can't add any info about our plants to this table in sensible organized way - especially when the plants can change

## One to many relationship

We can address our problems by making another table `plants` that holds information about our plants and has a `foreign key` the foreign key will be the `id` from our `ice_cream` table.

Our Angel investors gave us money to buy more plants where we haven't had a chance to figure out which ice cream we'll be making there.

Nevertheless **ONE** ice cream flavor will have **MANY** manufacting plants. Again, for simplicity of this example, each plant can only manufacture **ONE** flavor.

When we create our new plants, they'll have a city (again for simplicity, but likely you'd want more information like the full address...), how many pints made, whether it has passed a food inspection, and the `id` of the ice cream flavor that it will be manufacturing.

```sql
CREATE TABLE plants (id SERIAL PRIMARY KEY, city VARCHAR(144), pints_made INT, passed BOOLEAN, ice_cream_id INT);

INSERT INTO plants (city, pints_made, passed, ice_cream_id) VALUES
('Stamford', 100, true, 1),
('Greenwich', 20, false, 2),
('Hartford', 200, true, 3),
('Waterbury', null, null, null),
('Darien', null, null, null),
('New London', 100, true, 2),
('Bridgeport', 150, true, 2),
('Milford', null, false, null),
('Norwalk', 40, true, 3),
('Hamden', null, true, null),
('New Britain', null, false, null),
('Trumbull', null, null, null),
('Danbury', 300, true, 3),
('New Canaan', null, true, null),
('Fairfield', 400, false, 4),
('Stratford', 250, true, 1);


SELECT * FROM plants;
```

Tough to read? try toggling the extended view by using `\x`

Don't want to scroll to the bottom? press `q`
