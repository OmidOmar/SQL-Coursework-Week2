# E-Commerce Database

In this homework, you are going to work with an ecommerce database. In this database, you have `products` that `consumers` can buy from different `suppliers`. Customers can create an `order` and several products can be added in one order.

## Submission

Below you will find a set of tasks for you to complete to set up a database for an e-commerce app.

To submit this homework write the correct commands for each question here:

```sql

A.1: SELECT * FROM customers WHERE country = 'United States';

A.2: SELECT * FROM customers ORDER BY name ASC;

A.3: SELECT * FROM products WHERE product_name like '%socks%';

A.4: SELECT p.id,p.product_name, unit_price, supp_id FROM product_availability pa JOIN products p ON pa.prod_id = p.id WHERE pa.unit_price > 100 ;

A.5: SELECT p.product_name, pa.unit_price FROM product_availability pa JOIN products p ON pa.prod_id = p.id ORDER BY unit_price DESC LIMIT 5;

A.6: SELECT p.product_name, pa.unit_price, s.supplier_name FROM products p JOIN product_availability pa ON p.id = pa.prod_id JOIN suppliers s ON pa.supp_id = s.id;

A.7: SELECT p.product_name, s.supplier_name FROM suppliers s JOIN product_availability pa ON s.id = pa.supp_id JOIN products p ON pa.prod_id = p.id WHERE s.country = 'United Kingdom';

A.8: SELECT o.id, o.order_reference, order_date,(oi.quantity * pa.unit_price) as Total_Cost FROM orders o JOIN order_items oi ON o.id = oi.order_id JOIN product_availability pa ON oi.product_id = pa.prod_id  WHERE customer_id = 1;

A.9: SELECT * FROM orders o JOIN order_items oi ON o.id=oi.order_id JOIN customers c ON o.customer_id = c.id WHERE c.name = 'Hope Crosby';

A.10: SELECT p.product_name, pa.unit_price, oi.quantity FROM orders o JOIN order_items oi ON o.id = oi.order_id JOIN product_availability pa ON oi.product_id = pa.prod_id JOIN products p ON pa.prod_id = p.id WHERE order_reference = 'ORD006';

A.11: SELECT c.name, o.order_date,o.order_reference,p.product_name,s.supplier_name,oi.quantity FROM products p JOIN product_availability pa on p.id=pa.prod_id JOIN suppliers s ON pa.supp_id = s.id JOIN order_items oi ON p.id = oi.product_id JOIN orders o ON oi.order_id = o.id JOIN customers c ON o.customer_id = c.id;

A.12: SELECT distinct c.name FROM order_items oi JOIN orders o ON oi.order_id = o.id JOIN customers c ON o.customer_id = c.id JOIN suppliers s on oi.supplier_id = s.id WHERE s.country = 'China';

A.13: SELECT c.name, o.order_reference, o.order_date, oi.quantity * pa.unit_price as total_amount  FROM orders o JOIN order_items oi ON o.id = oi.order_id JOIN customers c ON o.customer_id = c.id JOIN product_availability pa ON oi.product_id = pa.prod_id ORDER by total_amount DESC;

```

When you have finished all of the questions - open a pull request with your answers to the `Databases-Homework` repository.

## Setup

To prepare your environment for this homework, open a terminal and create a new database called `cyf_ecommerce`:

```sql
createdb cyf_ecommerce
```

Import the file [`cyf_ecommerce.sql`](./cyf_ecommerce.sql) in your newly created database:

```sql
psql -d cyf_ecommerce -f cyf_ecommerce.sql
```

Open the file `cyf_ecommerce.sql` in VSCode and examine the SQL code. Take a piece of paper and draw the database with the different relationships between tables (as defined by the REFERENCES keyword in the CREATE TABLE commands). Identify the foreign keys and make sure you understand the full database schema.

## Task

Once you understand the database that you are going to work with, solve the following challenge by writing SQL queries using everything you learned about SQL:

1. Retrieve all the customers' names and addresses who live in the United States
2. Retrieve all the customers in ascending name sequence
3. Retrieve all the products whose name contains the word `socks`
4. Retrieve all the products which cost more than 100 showing product id, name, unit price and supplier id.
5. Retrieve the 5 most expensive products
6. Retrieve all the products with their corresponding suppliers. The result should only contain the columns `product_name`, `unit_price` and `supplier_name`
7. Retrieve all the products sold by suppliers based in the United Kingdom. The result should only contain the columns `product_name` and `supplier_name`.
8. Retrieve all orders, including order items, from customer ID `1`. Include order id, reference, date and total cost (calculated as quantity \* unit price).
9. Retrieve all orders, including order items, from customer named `Hope Crosby`
10. Retrieve all the products in the order `ORD006`. The result should only contain the columns `product_name`, `unit_price` and `quantity`.
11. Retrieve all the products with their supplier for all orders of all customers. The result should only contain the columns `name` (from customer), `order_reference`, `order_date`, `product_name`, `supplier_name` and `quantity`.
12. Retrieve the names of all customers who bought a product from a supplier based in China.
13. List all orders giving customer name, order reference, order date and order total amount (quantity \* unit price) in descending order of total.
