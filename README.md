#### How many users are there?
##### Answer: 50
##### SQL Commands:
```
select count(*) from users;
```
___
#### What are the 5 most expensive items?
##### Answer:
id | title | category | description | price
--- | --- | --- | --- | ---
25 | Small Cotton Gloves | Automotive, Shoes & Beauty  | Multi-layered modular service-desk | 9984      
83 | Small Wooden Computer | Health | Re-engineered fault-tolerant adapter | 9859      
100 | Awesome Granite Pants | Toys & Books | Upgradable 24/7 access | 9790      
40  |  Sleek Wooden Hat  | Music & Baby | Quality-focused heuristic info-mediaries |  9390      
60  | Ergonomic Steel Car | Books & Outdoors | Enterprise-wide secondary firmware | 9341
##### SQL Commands:
```
select * from items order by price desc limit 5;
```
___

#### What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
##### Answer:
Category is exactly 'Books':

id | title | category | description | price
--- | --- | --- | --- | ---
76 | Ergonomic Granite Chair | Books | De-engineered bi-directional portal | 1496

Category contains 'Books' :

Answer doesn't change

id | title | category | description | price
--- | --- | --- | --- | ---
76 | Ergonomic Granite Chair | Books | De-engineered bi-directional portal | 1496
##### SQL Commands:
Category is exactly 'Books':
```
select * from items where category='Books' order by price limit 1;
```
Category contains 'Books':
```
select * from items where category like '%Books%' order by price limit 1;
```
___

#### Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
##### Answer:
Corrine Little

Other address: 54369 Wolff Forges, Lake Bryon, CA 31587
##### SQL Commands:
```
select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state, addresses.zip from addresses inner join users on addresses.user_id = users.id where addresses.street='6439 Zetta Hills';

select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state, addresses.zip from addresses inner join users on addresses.user_id = users.id where users.first_name='Corrine';
```
___

#### Correct Virginie Mitchell's address to "New York, NY, 10108".
##### SQL Commands:
```
select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state, addresses.zip, addresses.id from addresses inner join users on addresses.user_id = users.id where users.first_name='Virginie';

update addresses set city='New York', zip='10108' where id=41;
```
___

#### How much would it cost to buy one of each tool?
##### Answer: 46477
##### SQL Commands:
```
select sum(price) from items where category like '%tool%';
```
___

#### How many total items did we sell?
##### Answer: 2125
##### SQL Commands:
```
select sum(orders.quantity) from orders inner join items on items.id=orders.item_id;
```
___

#### How much was spent on books?
##### Answer: 420566
##### SQL Commands:
```
select sum(items.price * orders.quantity) from items inner join orders on items.id=orders.item_id where category='Books';
```
___

#### Simulate buying an item by inserting a User for yourself and an Order for that User.
##### SQL Commands:
```
insert into users (first_name, last_name, email) values ('Whitney', 'Weir', 'whitneyweir36@gmail.com');

select * from users where first_name='Whitney'; // to find user id = 51

insert into orders (user_id, item_id, quantity, created_at) values (51, 10, 2, datetime());
```
___

#### What item was ordered most often? Grossed the most money?
##### Answer:
Ordered most often:

id | title | sum(orders.quantity)
--- | --- | ---
65 | Incredible Granite Car | 72

Grossed the most money:

id | title | sum(orders.quantity * items.price)
--- | --- | ---
65 | Incredible Granite Car | 525240
##### SQL Commands:
```
select items.id, items.title, sum(orders.quantity) from items inner join orders on items.id=orders.item_id group by items.id order by sum(orders.quantity) desc limit 1;

select items.id, items.title, sum(orders.quantity * items.price) from items inner join orders on items.id=orders.item_id group by items.id order by sum(orders.quantity* items.price) desc limit 1;
```
___

#### What user spent the most?
##### Answer
id | first_name | last_name | sum(items.price * orders.quantity)
--- | --- | --- | ---
19 | Hassan | Runte | 639386
##### SQL Commands:
```
select users.id, users.first_name, users.last_name, sum(items.price * orders.quantity) from users inner join orders on users.id=orders.user_id inner join items on orders.item_id=items.id group by users.id order by sum(items.price * orders.quantity) desc limit 1;
```
___

#### What were the top 3 highest grossing categories?
##### Answer:
category | sum(items.price * orders.quantity)
--- | ---
Music, Sports & Clothing | 525240
Beauty, Toys & Sports | 449496
Sports | 448410
##### SQL Commands:
```
select items.category, sum(items.price * orders.quantity) from items inner join orders on items.id=orders.item_id group by items.category order by sum(items.price * orders.quantity) desc limit 3;
```
___

#### Completed sqlteaching.com exercises
[screenshot]: ./sqlteaching-exercises.png
![screenshot]
