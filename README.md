## Databasics

Fork this repository into your own github profile.

Before closing the homework assignment issue:

- Update this README as follows:
  - [ ] For each question (just after or below the question itself) include the SQL you wrote to generate the answer
  - [ ] For each question (just after or below the question itself) include the *answer* to the question asked.

- Also:
  - [ ] Commit the updated `store.sqlite3` database file
  - [ ] Include a link to your forked repo in the comments when closing the issue.


NOTE: To run sqlite with this database: `sqlite3 store.sqlite3`

NOTE: You may want to keep a backup of the `store.sqlite3` file in case you damage the file. *OR* you can use the command `git checkout store.sqlite3` to undo any changes to the database file since the fork or your last commit.

## Explorer Mode

- [ ] How many users are there?
select * from users;
50

- [ ] What are the 5 most expensive items?
select title, price
from items order by price desc limit 5;
Small Cotton Gloves, Small Wooden Computer, Awesome Granite Pan, Sleek Wooden Hat, Ergonomic Steel Car

- [ ] What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
select title, min(price)
from items
where category like '%book%';
Ergonomic Granite Chair

- [ ] Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
select * from users, addresses
where users.id = addresses.user_id and
      addresses.street = '6439 Zetta Hills';
Corrine Little
select * from addresses where user_id = 40;
also has 54369 Wolff Forg Lake Byron CA 31587

- [ ] Correct Virginie Mitchell's address to "New York, NY, 10108".
select id
from users
where first_name = Virginie and
      last_name = Mitchell
to find her id = 39
then I found her NY address was id 41
UPDATE addresses
SET city = 'New York', zip = 10108
WHERE id = 41;

- [ ] How much would it cost to buy one of each tool?
SELECT sum(price)
FROM items
WHERE category like '%tool%';
46477

- [ ] How many total items did we sell?
SELECT sum(quantity)
FROM orders;
2125

- [ ] How much was spent on books?
SELECT sum(items.price * orders.quantity)
FROM items, orders
WHERE orders.user_id IN
 (SELECT id
 FROM items
 WHERE category like '%book%') AND
items.id = orders.user_id;
852648

- [ ] Simulate buying an item by inserting a User for yourself and an Order for that User.
INSERT INTO users
VALUES (NULL, "Alan", "Kebert", "akebert@fakemail.com");
INSERT INTO orders
VALUES(NULL,
  (SELECT id
   FROM users
   WHERE last_name = "Kebert"),
  (SELECT id
   FROM items
   ORDER BY RANDOM() LIMIT 1),
  2, "2016 08 09");

## Adventure Mode

- [ ] What item was ordered most often? Grossed the most money?
- [ ] What user spent the most?
- [ ] What were the top 3 highest grossing categories?
