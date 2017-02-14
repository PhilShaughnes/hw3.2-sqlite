***HW 3.2 SQL Practice***

**Explorer Mode**

1.1) How many users are there?
> SELECT COUNT(\*) FROM users;

1.2) What are the 5 most expensive items?

COMMAND:
>SELECT * FROM items ORDER BY price DESC LIMIT 5;

RESULT:

>25|Small Cotton Gloves|Automotive, Shoes & Beauty|Multi-layered modular service-desk|9984

>83|Small Wooden Computer|Health|Re-engineered fault-tolerant adapter|9859

>100|Awesome Granite Pants|Toys & Books|Upgradable 24/7 access|9790

>40|Sleek Wooden Hat|Music & Baby|Quality-focused heuristic info-mediaries|9390

>60|Ergonomic Steel Car|Books & Outdoors|Enterprise-wide secondary firmware|9341

1.3) What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

COMMAND:
>SELECT * FROM items WHERE category='Book' ORDER BY price ASC LIMIT 1;

RESULT:
>  

COMMAND:
>SELECT * FROM items WHERE category LIKE '%Books%' ORDER BY price ASC LIMIT 1;

RESULT:
>76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496


1.4a) Who lives at "6439 Zetta Hills, Willmouth, WY"?*

COMMAND:
> SELECT users.first_name, addresses.street, addresses.city, addresses.state, addresses.zip FROM addresses INNER JOIN users ON addresses.user_id=users.id WHERE street LIKE '%Zetta Hills%';

RESULT:
>Corrine|6439 Zetta Hills|Willmouth|WY|15029

1.4b) Do they have another address?

COMMAND:
>SELECT * FROM addresses WHERE user_id=(SELECT user_id FROM addresses WHERE street LIKE '%Zetta Hills%');

RESULT:
>id|user_id|street|city|state|zip

>43|40|6439 Zetta Hills|Willmouth|WY|15029

>44|40|54369 Wolff Forges|Lake Bryon|CA|31587

1.5) Correct Virginie Mitchell's address to "New York, NY, 10108".

COMMAND:
>UPDATE addresses SET city='New York', state='NY', zip='10108' WHERE user_id=(SELECT id FROM users WHERE first_name LIKE '%Virginie%') AND state='NY';

RESULT:

>

1.6) How much would it cost to buy one of each tool?

COMMAND:
>SELECT SUM(price) FROM items WHERE category LIKE '%tool%';

RESULT:
>SUM(price)
46477

1.7) How many total items did we sell?

COMMAND:
>SELECT SUM(quantity) FROM orders

RESULT:
>SUM(quantity)
2125

1.8) How much was spent on books?

COMMAND:
>SELECT SUM(items.price*orders.quantity) FROM items JOIN orders ON items.id=orders.item_id WHERE items.category LIKE '%Books%';

RESULT:
>SUM(price)
1081352

1.9) Simulate buying an item by inserting a User for yourself and an Order for that User.

COMMAND:
> INSERT INTO users (first_name, last_name, email) VALUES ('Phil', 'Shaughnessy', 'philipshaughnessy@gmail.com');

> INSERT INTO orders (user_id, item_id, quantity, created_at) VALUES ((SELECT id FROM users WHERE last_name='Shaughnessy'), 34, 6, CURRENT_TIMESTAMP);

RESULT: (using SELECT * FROM users JOIN orders ON users.id=orders.user_id WHERE users.last_name='Shaughnessy';)
> id|first_name|last_name|email|id|user_id|item_id|quantity|created_at
>51|Phil|Shaughnessy|philipshaughnessy@gmail.com|378|51|34|6|2017-02-14 21:12:49



**Adventure Mode**

2.1) What item was ordered most often?


COMMAND:
> SELECT items.title, SUM(orders.quantity) FROM orders JOIN items ON orders.item_id=items.id GROUP BY orders.item_id ORDER BY SUM(orders.quantity) DESC LIMIT 1;



RESULT:
> title|SUM(orders.quantity)

>Incredible Granite Car|72

2.2) Grossed the most money?


COMMAND:

> SELECT items.title, SUM(items.price*orders.quantity) FROM orders JOIN items ON orders.item_id=items.id GROUP BY orders.item_id ORDER BY SUM(items.price*orders.quantity) DESC LIMIT 1;

RESULT:
> title|SUM(items.price*orders.quantity)

> Incredible Granite Car|525240

2.3) What user spent the most?

COMMAND:
> SELECT users.first_name, users.last_name, SUM(orders.quantity*items.price) FROM users INNER JOIN orders ON users.id=orders.user_id INNER JOIN items ON orders.item_id=items.id GROUP BY users.id ORDER BY SUM(orders.quantity*items.price) DESC;

RESULT:
> first_name|last_name|SUM(orders.quantity*items.price)

> Hassan|Runte|639386

2.4) What were the top 3 highest grossing categories?

COMMAND:
> SELECT items.category, SUM(items.price*orders.quantity) FROM items JOIN orders ON items.id=orders.item_id GROUP BY items.category ORDER BY SUM(items.price*orders.quantity) DESC LIMIT 3;

RESULT:
> category|SUM(items.price*orders.quantity)

> Music, Sports & Clothing|525240

> Beauty, Toys & Sports|449496

> Sports|448410

**Epic Mode**

Complete the exercises on sqlteaching.com as well and add a screenshot of the final screen showing all exercises completed to your README.
