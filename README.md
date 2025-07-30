# Tuw-DataBaseIntro
```sql
DROP DATABASE store;
CREATE DATABASE IF NOT EXISTS store;
USE store;

CREATE TABLE IF NOT EXISTS countries(
    code INT PRIMARY KEY,
    name VARCHAR(20) UNIQUE,
    continent_name VARCHAR(20) NOT NULL
);


CREATE TABLE IF NOT EXISTS users(
    id INT PRIMARY KEY,
    full_name VARCHAR(20),
    email VARCHAR(20) UNIQUE,
    gender CHAR(1) CHECK (gender IN ('m', 'f')),
    date_of_birth DATETIME,
    country_code INT,
    FOREIGN KEY (country_code) REFERENCES countries (code)
);

CREATE TABLE IF NOT EXISTS orders(
    id INT PRIMARY KEY,
    user_id INT,
    status VARCHAR(6) CHECK (status IN ('start', 'finish')),
    created_at DATETIME,
    FOREIGN KEY (user_id) REFERENCES users (id)
);

CREATE TABLE IF NOT EXISTS products(
    id INT PRIMARY KEY,
    name VARCHAR(20) NOT NULL,
    price INT DEFAULT 0,
    status VARCHAR(10) CHECK (status IN ('valid', 'expired')),
    created_at DATETIME
);

CREATE TABLE IF NOT EXISTS order_products(
    order_id INT,
    product_id INT,
    quantity INT DEFAULT 0,
    FOREIGN KEY (order_id) REFERENCES orders (id),
    FOREIGN KEY (product_id) REFERENCES products (id)
);

# countries
INSERT INTO countries (code, name, continent_name) VALUES (1, 'Saudi Arabia', 'Asia');
INSERT INTO countries (code, name, continent_name) VALUES (2, 'United Arab Emirates', 'Asia');
INSERT INTO countries (code, name, continent_name) VALUES (3, 'Kuwait', 'Asia');
INSERT INTO countries (code, name, continent_name) VALUES (4, 'Qatar', 'Asia');
INSERT INTO countries (code, name, continent_name) VALUES (5, 'Oman', 'Asia');

#users
INSERT INTO users (id, full_name, email, gender, date_of_birth, country_code) VALUES (1, 'Hussam Alghamdi', 'hussam@sa.com', 'm', '1998-04-12', 1);
INSERT INTO users (id, full_name, email, gender, date_of_birth, country_code) VALUES (2, 'Rana Alharbi', 'rana@uae.com', 'f', '1995-11-03', 2);
INSERT INTO users (id, full_name, email, gender, date_of_birth, country_code) VALUES (3, 'Salman Alsubaie', 'salman@kw.com', 'm', '1990-07-27', 3);
INSERT INTO users (id, full_name, email, gender, date_of_birth, country_code) VALUES (4, 'Noura Alotaibi', 'noura@qa.com', 'f', '1999-02-19', 4);
INSERT INTO users (id, full_name, email, gender, date_of_birth, country_code) VALUES (5, 'Fahad Alzahrani', 'fahad@om.com', 'm', '1993-09-08', 5);

#orders
INSERT INTO orders (id, user_id, status, created_at) VALUES (1, 1, 'start', NOW());
INSERT INTO orders (id, user_id, status, created_at) VALUES (2, 2, 'finish', NOW());
INSERT INTO orders (id, user_id, status, created_at) VALUES (3, 3, 'start', NOW());
INSERT INTO orders (id, user_id, status, created_at) VALUES (4, 4, 'finish', NOW());
INSERT INTO orders (id, user_id, status, created_at) VALUES (5, 5, 'start', NOW());

#products
INSERT INTO products (id, name, price, status, created_at) VALUES (1, 'Dates Box', 80, 'valid', NOW());
INSERT INTO products (id, name, price, status, created_at) VALUES (2, 'Saudi Coffee', 120, 'valid', NOW());
INSERT INTO products (id, name, price, status, created_at) VALUES (3, 'Abaya', 300, 'expired', NOW());
INSERT INTO products (id, name, price, status, created_at) VALUES (4, 'Oud Perfume', 500, 'valid', NOW());
INSERT INTO products (id, name, price, status, created_at) VALUES (5, 'Miswak', 10, 'expired', NOW());

# order_products
INSERT INTO order_products (order_id, product_id, quantity) VALUES (1, 1, 2);
INSERT INTO order_products (order_id, product_id, quantity) VALUES (2, 2, 1);
INSERT INTO order_products (order_id, product_id, quantity) VALUES (3, 3, 1);
INSERT INTO order_products (order_id, product_id, quantity) VALUES (4, 4, 2);
INSERT INTO order_products (order_id, product_id, quantity) VALUES (5, 5, 3);

#cheack tables before update or delete something
SELECT * FROM countries;
SELECT * FROM users;
SELECT * FROM orders;
SELECT * FROM products;
SELECT * FROM order_products;


#before: 'Saudi Arabia', 'Asia'
UPDATE countries
SET name = 'Kingdom of Saudi Arabia'
WHERE code = 1;
SELECT * FROM countries WHERE code = 1;

#before: 'Hussam Alghamdi', 'hussam@sa.com'
UPDATE users
SET full_name = 'Hussam Al-Ghamdi', email = 'hussam.alghamdi@ksa.com'
WHERE id = 1;
SELECT * FROM users WHERE id = 1;

#before: 'start'
UPDATE orders
SET status = 'finish'
WHERE id = 1;
SELECT * FROM orders WHERE id = 1;

#before: 80, 'valid'
UPDATE products
SET price = 100, status = 'expired'
WHERE id = 1;
SELECT * FROM products WHERE id = 1;

#before: 2
UPDATE order_products
SET quantity = 10
WHERE order_id = 1 AND product_id = 1;
SELECT * FROM order_products WHERE order_id = 1 AND product_id = 1;


# this the flow to delete one country
DELETE FROM order_products
WHERE order_id = 1 && product_id = 1;

# now I can delete order 1, product 1
DELETE FROM orders
WHERE id = 1;

DELETE FROM products
WHERE id = 1;

DELETE FROM users
WHERE id = 1;

#now I can delete country,
DELETE FROM countries
WHERE code = 1;


SELECT * FROM countries;
SELECT * FROM users;
SELECT * FROM orders;
SELECT * FROM products;
SELECT * FROM order_products;


```
