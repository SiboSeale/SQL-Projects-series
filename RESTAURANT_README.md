# Restaurant Orders and Menu Analysis

## 📌 Project Overview

This project explores a restaurant's menu and order data using SQL queries. The analysis is divided into three sections:

Menu Items Analysis - Examining menu structure, pricing, and categorization.

Order Details Analysis - Understanding order volume, frequency, and high-volume orders.

Menu & Order Details Combination - Integrating menu data with order records to extract business insights.

## 📂 Datasets Used

The project uses three tables:

menu_items: Contains information about dishes, their prices, and categories.

order_details: Records details of customer orders.

menu_items JOIN order_details: A combined dataset for deeper analysis.

## 🔍 SQL Queries & Objectives

### 1️⃣ Menu Items Analysis

Objectives:

View all menu items.

Count the number of menu items.

Identify the least and most expensive dishes.

Analyze Italian dishes.

Count dishes per category.

Determine the average price per category.

Key Queries:

-- View the menu_items table
SELECT * FROM menu_items;

-- Count the number of items on the menu
SELECT COUNT(*) FROM menu_items;

-- Find the least and most expensive items
SELECT * FROM menu_items ORDER BY price DESC;

-- Count Italian dishes
SELECT COUNT(*) FROM menu_items WHERE category='Italian';

-- Least and most expensive Italian dishes
SELECT * FROM menu_items WHERE category='Italian' ORDER BY price DESC;

-- Count dishes per category
SELECT category, COUNT(menu_item_id) AS num_dishes FROM menu_items GROUP BY category;

-- Average price per category
SELECT category, AVG(price) AS avg_price FROM menu_items GROUP BY category;

### 2️⃣ Order Details Analysis

Objectives:

View order details.

Determine the date range.

Count the number of orders and items.

Identify orders with the most items.

Find orders exceeding 12 items.

Key Queries:

-- View the order_details table
SELECT * FROM order_details;

-- Find date range of orders
SELECT MIN(order_date), MAX(order_date) FROM order_details;

-- Count total orders
SELECT COUNT(DISTINCT order_id) FROM order_details;

-- Count total items ordered
SELECT COUNT(*) FROM order_details;

-- Identify orders with the most items
SELECT order_id, COUNT(item_id) AS num_items FROM order_details GROUP BY order_id ORDER BY num_items DESC;

-- Count orders with more than 12 items
SELECT COUNT(*) FROM (
    SELECT order_id, COUNT(item_id) AS num_items
    FROM order_details
    GROUP BY order_id
    HAVING num_items > 12
) AS num_orders;

### 3️⃣ Menu & Order Details Combination

Objectives:

Join menu_items with order_details for comprehensive analysis.

Identify the most and least ordered items.

Find the highest-spending orders.

Examine category details of top orders.

Key Queries:

-- Join menu_items with order_details
SELECT * FROM order_details od LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id;

-- Find the least and most ordered items
SELECT item_name, category, COUNT(order_details_id) AS num_purchases
FROM order_details od
LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id
GROUP BY item_name, category
ORDER BY num_purchases DESC;

-- Find the top 5 highest spending orders
SELECT order_id, SUM(price) AS total_spend
FROM order_details od
LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id
GROUP BY order_id
ORDER BY total_spend DESC
LIMIT 5;

-- View category breakdown for the highest spend order (Order ID: 440)
SELECT category, COUNT(item_id) AS num_items
FROM order_details od
LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id
WHERE order_id = 440
GROUP BY category;

-- Analyze top 5 highest spending orders
SELECT order_id, category, COUNT(item_id) AS num_items
FROM order_details od
LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id
WHERE order_id IN (440, 2075, 1957, 330, 2675)
GROUP BY order_id, category;

## 🏆 Key Insights

The restaurant offers a variety of dishes, with Italian cuisine making up a significant portion.

Price variations exist across categories, with some dishes being significantly more expensive than others.

High-volume orders indicate peak demand periods and preferred menu items.

The most frequently ordered items belong to certain categories, which could help in menu optimization.

The highest-spending orders provide insights into customer preferences and potential upselling opportunities.

## 📌 Next Steps

Perform trend analysis on order frequency by date.

Identify seasonal demand for specific dishes.

Suggest menu adjustments based on customer preferences.

Optimize pricing strategy using the average price per category.

## 📧 Contact & Feedback

If you have any suggestions or questions, feel free to reach out!

# 📌 Author: Sibongile Seale
