## Demo SQL Data: 


This SQL script creates a small e-commerce database with three related tables: users, products, and orders.

It is useful for practicing PostgreSQL SQL queries, joins, indexes, aggregation, and database performance testing.



### Database structure:

```
users: Stores customer information.
- user_id — Primary key
- username — Customer username
- email — Customer email
- created_at — Account creation timestamp


products: Stores product and inventory information.
- product_id — Primary key
- product_name — Product name
- category — Product category
- price — Unit price
- stock_quantity — Available inventory


orders: Connects customers with purchased products.
- order_id — Primary key
- user_id — Foreign key to users
- product_id — Foreign key to products
- quantity — Units ordered
- total_amount — Total order price
- order_date — Order timestamp


The relationships are (Both are one-to-many relationships):
- users.user_id → orders.user_id
- products.product_id → orders.product_id
```



### Create the tables: 

```sql
-- 1. Create Users Table
CREATE TABLE users (
    user_id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```


```sql
-- 2. Create Products Table
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    category VARCHAR(50),
    price NUMERIC(10, 2) NOT NULL,
    stock_quantity INT DEFAULT 0
);
```


```sql
-- 3. Create Orders Table
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(user_id),
    product_id INT REFERENCES products(product_id),
    quantity INT NOT NULL,
    total_amount NUMERIC(10, 2) NOT NULL,
    order_date TIMESTAMP
);
```


### Generate 1,000 mock users:

```sql
-- Generate 1,000 Mock Users
INSERT INTO users (username, email, created_at)
SELECT
    'user_' || seq AS username,
    'user_' || seq || '@example.com' AS email,
    NOW() - (random() * INTERVAL '365 days') AS created_at
FROM generate_series(1, 1000) AS seq;
```


### Generate 50 mock products: 

```sql
-- Generate 50 Mock Products across 5 categories
INSERT INTO products (product_name, category, price, stock_quantity)
SELECT
    'Product ' || seq AS product_name,
    (ARRAY['Electronics', 'Clothing', 'Home & Kitchen', 'Books', 'Sports'])[floor(random() * 5) + 1] AS category,
    ROUND((random() * 490 + 10)::numeric, 2) AS price, -- Price between $10.00 and $500.00
    floor(random() * 200 + 10)::int AS stock_quantity
FROM generate_series(1, 50) AS seq;
```


### Generate 5,000 mock orders: 

```sql
-- Generate 5,000 Mock Orders matching existing users and products
INSERT INTO orders (user_id, product_id, quantity, total_amount, order_date)
SELECT
    floor(random() * 1000 + 1)::int AS user_id, -- Picks a random user ID between 1 and 1000
    floor(random() * 50 + 1)::int AS product_id,  -- Picks a random product ID between 1 and 50
    floor(random() * 5 + 1)::int AS quantity,     -- Quantity between 1 and 5
    0.00 AS total_amount,                         -- Temporarily 0, we will update it based on product price next
    NOW() - (random() * INTERVAL '90 days') AS order_date
FROM generate_series(1, 5000) AS seq;
```


### Calculate each order's total amount:

```sql
-- Update the orders total_amount to reflect accurate product prices
UPDATE orders o
SET total_amount = o.quantity * p.price
FROM products p
WHERE o.product_id = p.product_id;
```


### Verify:

```sql
select * from users;
select * from products;
select * from orders;
```


```sql
SELECT COUNT(*) FROM users;
SELECT COUNT(*) FROM products;
SELECT COUNT(*) FROM orders;
```


```sql
SELECT 'users', COUNT(*) AS row_count FROM users;
SELECT 'products', COUNT(*) FROM products;
SELECT 'orders', COUNT(*) FROM orders;
```


---
---

