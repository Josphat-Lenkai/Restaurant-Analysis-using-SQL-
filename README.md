# Restaurant SQL Analysis

## Introduction
This project involves SQL queries to analyze a restaurant's menu items and orders. The analysis includes retrieving details about menu items, such as the number of items, prices, categories, and frequency of orders. Additionally, the data in the `order_details` table is examined to determine order frequency, popular items, and spending patterns.

## Project Structure
The project includes the following SQL queries:
- **Menu Items Analysis**: Extracts insights from the `menu_items` table, such as the number of items, least and most expensive dishes, and dish categories.
- **Order Details Analysis**: Investigates order frequency, the date range of orders, and items ordered.
- **Combining Menu and Order Details**: Joins the `menu_items` and `order_details` tables to analyze the correlation between menu items and orders.

## Objectives
- Find the number of items on the menu.
- Identify the least and most expensive menu items.
- Analyze Italian dishes and their pricing.
- Examine dish categories and their average prices.
- Analyze the order details for frequency and spending patterns.
- Identify the least and most ordered items and categories.

## Queries

### Menu Items Analysis
- **Number of items on the menu**:
  ```sql
  SELECT COUNT(item_name) AS Number_of_items_Menu FROM menu_items;

- **Least and most expensive items**:
  ```sql
  SELECT TOP 5 * FROM menu_items ORDER BY price DESC;
  SELECT TOP 5 * FROM menu_items ORDER BY price ASC;
  
- **Italian dishes analysis:**:
   ```sql
   SELECT COUNT(category) AS number_of_italian_dishes FROM menu_items WHERE category = 'Italian';
   SELECT * FROM menu_items WHERE category = 'Italian' ORDER BY price DESC;

- **Dishes and categories:**:
   ```sql
   SELECT category, COUNT(item_name) AS dishes_in_category, AVG(price) AS Average_price FROM menu_items GROUP BY category;

### Order Details Analysis
- **Date range of orders:**:
   ```sql
   SELECT MIN(order_date) AS min_order_date, MAX(order_date) AS max_order_date FROM order_details;

- **Total orders and items ordered:**:
   ```sql
   SELECT COUNT(DISTINCT order_id) AS total_orders FROM order_details;
   SELECT COUNT(item_id) AS total_items_ordered FROM order_details;

- **Orders with most items:**:
   ```sql
   SELECT order_id, COUNT(item_id) AS number_of_items FROM order_details GROUP BY order_id ORDER BY number_of_items DESC;
### Combining Menu and Order Details
- **Join tables to analyze order and menu data:**:
   ```sql
   SELECT * FROM menu_items AS mi INNER JOIN order_details AS od ON mi.menu_item_id = od.item_id;

- **Least and most ordered items:**:
   ```sql
   SELECT item_name, COUNT(order_details_id) AS num_of_orders FROM menu_items AS mi INNER JOIN order_details AS od ON mi.menu_item_id = od.item_id GROUP BY item_name ORDER BY num_of_orders DESC;

- **Least and most ordered items:**:
   ```sql
   SELECT TOP 5 order_id, SUM(price) AS total_price FROM menu_items AS mi INNER JOIN order_details AS od ON mi.menu_item_id = od.item_id GROUP BY order_id ORDER BY total_price DESC;

## Results
### Key Insights

- The most expensive items and least expensive items on the menu provide insights into pricing strategy.
- Italian dishes were analyzed in terms of pricing and popularity.
- Orders with the highest spending reveal customer preferences.
- Categories with the most orders help in menu optimization.

## Conclusion
This SQL analysis uncovers key insights into menu pricing, item popularity, and customer spending. It highlights top-performing dishes and categories, providing data-driven guidance for optimizing the menu, pricing strategy, and inventory management to meet customer preferences efficiently.
