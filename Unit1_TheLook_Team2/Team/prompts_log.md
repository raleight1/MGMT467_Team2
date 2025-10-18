# Prompt Log

This file documents all unique AI prompts used during this project and includes two examples showing an initial failed prompt and how it was improved (“fail then fix”).

---

## 🧠 Unique Prompts
List each unique prompt you used (for coding, analysis, writing, etc.).
Example format:

1. “You are an analytics co‑pilot. Propose 5 high‑value, testable business questions about the Citi Bike dataset (tripduration, stations, user types, time-of-day/week). Return as bullets with suggested SQL hints.”
2. “Write a BigQuery SQL query to find the most popular start and end stations in the \`bigquery-public-data.new_york_citibike.citibike_trips\` table. The query should also show how the popularity varies by time of day (morning, afternoon, evening, night) and user type (Customer, Subscriber). Use CTEs and include a window function to rank stations.”
3. “Write a BigQuery SQL query to analyze how trip duration varies by user type (customer vs. subscriber) and time of day/week...”
4. “Write a BigQuery SQL query to analyze the monthly trends in total trips and average trip duration over time...”


---

## ⚙️ Fail Then Fix Examples

### Example 1
**Fail Prompt:**
“Write a BigQuery SQL query to find the most popular start and end stations... show how the popularity varies by time of day... for July 2019.”

**Issue:**
The query returned no results, potentially due to filtering on a specific month (July 2019) where data might have been sparse or the time of day categorization was not capturing data as expected for that period.

**Fixed Prompt:**
“Are there specific stations that experience significantly longer or shorter trip durations on average? Write a BigQuery SQL query to calculate the average trip duration for each start station and compare it to the overall average using a window function.”

**Result:**
Successfully identified stations with significantly different average trip durations, providing valuable insights into potential outliers or popular long-trip starting points.

---

### Example 2
**Fail Prompt:**
"Generate Python code to predict Citi Bike demand."

**Issue:**
The prompt was too broad and lacked necessary details about the data to be used for prediction, the desired model, or the specific prediction task (e.g., predicting demand at a specific station, overall demand, etc.).

**Fixed Prompt:**
"Generate Python code using scikit-learn to build a time series model to predict daily total Citi Bike trips based on the historical data in the `df_hyp_c` DataFrame."

**Result:**
Produced a relevant Python code snippet that utilizes the available data and specifies a common machine learning library and task, providing a workable starting point for demand prediction.
