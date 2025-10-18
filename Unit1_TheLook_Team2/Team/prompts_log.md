# Prompt Log

This file documents all unique AI prompts used during this project and includes two examples showing an initial failed prompt and how it was improved (“fail then fix”).

---

## 🧠 Unique Prompts
List each unique prompt you used (for coding, analysis, writing, etc.).
Example format:

1. “You are an analytics co‑pilot. Propose 5 high‑value, testable business questions about the E-Commerce dataset (distribution_centers events inventory_items order_items orders products thelook_ecommerce-table users). Return as bullets with suggested SQL hints.”
2. “Write and execute a BigQuery SQL query to analyze trends in order volume and revenue over time for the first hypothesis, store the result in a DataFrame, then write and execute a BigQuery SQL query to find the most popular and profitable product categories for the second hypothesis, storing the result in a DataFrame, and finally write and execute a BigQuery SQL query to analyze customer behavior across different user segments for the third hypothesis, storing the result in a DataFrame.”
3. "Write a BigQuery SQL query to find the most popular and profitable product categories in the \`bigquery-public-data.thelook_ecommerce.order_items\` and \`bigquery-public-data.thelook_ecommerce.products\` tables. The query should calculate the total number of order items and total revenue for each category. Use a window function to rank categories by popularity and profitability."
4. "Write a BigQuery SQL query to analyze customer behavior across different user segments (e.g., new vs. returning users) using the \`bigquery-public-data.thelook_ecommerce.orders\` and \`bigquery-public-data.thelook_ecommerce.order_items\` tables. Calculate metrics like the number of users, average order value, and average purchase frequency for each segment. Define user segments based on the number of orders."


---

## ⚙️ Fail Then Fix Examples

### Example 1
**Fail Prompt:**
"Write a BigQuery SQL query to find the top 10 best-selling products."

**Issue:**
The prompt was too simple and didn't specify how to define "best-selling" (by quantity or revenue) or which tables to use in the e-commerce dataset, leading to an ambiguous or incorrect initial query.

**Fixed Prompt:**
"Write a BigQuery SQL query using the \`order_items\` and \`products\` tables to find the top 10 product categories by total revenue, including the category name and the calculated total revenue, and order the results in descending order of revenue."

**Result:**
Produced a precise SQL query that correctly joins the necessary tables, aggregates data by category, calculates total revenue, and provides the top 10 categories ranked by profitability.

---

### Example 2
**Fail Prompt:**
"Show me the sales data."

**Issue:**
Extremely vague, didn't specify which aspects of sales data were needed (e.g., trends, categories, customer segments), the time frame, or the desired output format.

**Fixed Prompt:**
"Write a BigQuery SQL query to analyze the monthly trends in total order volume and total revenue over the last two years from the \`orders\` and \`order_items\` tables in the e-commerce dataset, grouping the results by month and calculating the total number of orders and the sum of sale price for each month."

**Result:**
Generated a focused SQL query that provides a clear time-series view of sales performance, allowing for the identification of trends and seasonality.

---
