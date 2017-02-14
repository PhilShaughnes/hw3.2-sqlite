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


1.4) Who lives at "6439 Zetta Hills, Willmouth, WY"?*

COMMAND:
> SELECT users.first_name, addresses.street, addresses.city, addresses.state, addresses.zip FROM addresses INNER JOIN users ON addresses.user_id=users.id WHERE street LIKE '%Zetta Hills%';

RESULT:
>Corrine|6439 Zetta Hills|Willmouth|WY|15029

1.5) Do they have another address?

COMMAND:
>SELECT * FROM addresses WHERE user_id=(SELECT user_id FROM addresses WHERE street LIKE '%Zetta Hills%');

RESULT:
>id|user_id|street|city|state|zip

>43|40|6439 Zetta Hills|Willmouth|WY|15029

>44|40|54369 Wolff Forges|Lake Bryon|CA|31587

1.6) Correct Virginie Mitchell's address to "New York, NY, 10108".

COMMAND:
>UPDATE addresses SET city='New York', state='NY', zip='10108' WHERE user_id=(SELECT id FROM users WHERE first_name LIKE '%Virginie%') AND state='NY';

RESULT:

>

1.7) How much would it cost to buy one of each tool?

COMMAND:
>sqlite> SELECT * FROM items WHERE category='Books' ORDER BY price ASC LIMIT 1;

RESULT:
>76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496

1.8) How many total items did we sell?
How much was spent on books?

COMMAND:
>sqlite> SELECT * FROM items WHERE category='Books' ORDER BY price ASC LIMIT 1;

RESULT:
>76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496

1.9) Simulate buying an item by inserting a User for yourself and an Order for that User.

COMMAND:
>sqlite> SELECT * FROM items WHERE category='Books' ORDER BY price ASC LIMIT 1;

RESULT:
>76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496

**Adventure Mode**

2.1) What item was ordered most often?

COMMAND:
>sqlite> SELECT * FROM items WHERE category='Books' ORDER BY price ASC LIMIT 1;

RESULT:
>76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496

2.2) Grossed the most money?

COMMAND:
>sqlite> SELECT * FROM items WHERE category='Books' ORDER BY price ASC LIMIT 1;

RESULT:
>76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496

2.3) What user spent the most?

COMMAND:
>sqlite> SELECT * FROM items WHERE category='Books' ORDER BY price ASC LIMIT 1;

RESULT:
>76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496

2.4) What were the top 3 highest grossing categories?

COMMAND:
>sqlite> SELECT * FROM items WHERE category='Books' ORDER BY price ASC LIMIT 1;

RESULT:
>76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496

**Epic Mode**

Complete the exercises on sqlteaching.com as well and add a screenshot of the final screen showing all exercises completed to your README.
