# online-store-sql-project
Beginner SQL project using MySQL for sales analysis

# 🛒 Online Store Sales Analysis (SQL Project)

 Project Overview
This beginner-friendly SQL project analyzes online store sales data using MySQL.  
It focuses on understanding customers, orders, revenue, and top-selling products.

 Objectives
- Analyze total orders
- Calculate revenue per order
- Identify top-selling products
- Practice SQL joins and aggregations

 Database Used
- MySQL

-- customers
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    city VARCHAR(50),
    join_date DATE
);

-- products
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2)
);

-- orders
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

-- order_details
CREATE TABLE order_details (
    order_detail_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);

-- Insert Sample Data
INSERT INTO customers VALUES
(1,'Amit','Delhi','2023-01-10'),
(2,'Sara','Mumbai','2023-02-15'),
(3,'John','Bangalore','2023-03-05');

-- SQL Analysis Queries
 -- Total Orders
 SELECT COUNT(*) AS total_orders FROM orders;

-- Revenue Per Order
SELECT o.order_id,
SUM(p.price * od.quantity) AS revenue
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
JOIN products p ON od.product_id = p.product_id
GROUP BY o.order_id;

-- Top-Selling Products
SELECT p.product_name,
SUM(od.quantity) AS total_sold
FROM order_details od
JOIN products p ON od.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sold DESC;


