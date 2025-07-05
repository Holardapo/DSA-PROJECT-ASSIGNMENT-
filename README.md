# DSA-PROJECT-ASSIGNMENT-
This marks my journey into the data analysis space and how this can be a stepping stone for success.A detailed analysis of sales and order data for a retail company, focusing operational efficiencies using SQL.
## Case 1
Question 1: Which product category had the highest sales?
``` SQL Query:

SELECT
    product_category,
    SUM(sales) AS total_sales
FROM
    public.orders
GROUP BY
    product_category
ORDER BY
    total_sales DESC
LIMIT 1;
```
- Result:
  1. Total sales 5984248.18 

 

Question 2: What are the Top 3 and Bottom 3 regions in terms of sales?
``` SQL Query (Top 3 Regions):

SELECT
    region,
    SUM(sales) AS total_sales
FROM
    public.orders
GROUP BY
    region
ORDER BY
    total_sales DESC
LIMIT 3;
```
Result (Top 3 Regions):

region             | total_sales

West:              3597549.2755
Ontario:           3063212.4795
Prarie:           2837304.6015
``` SQL Query (Bottom 3 Regions):

SELECT
    region,
    SUM(sales) AS total_sales
FROM
    public.orders
GROUP BY
    region
ORDER BY
    total_sales ASC
LIMIT 3;
```
Result (Bottom 3 Regions):

region                  | total_sales
------------------------+--------------
Nunavut                 | 116376.4835
Northwest Territories   | 800847.3295
Yukon                   | 975867.3710
Question 3: What were the total sales of appliances in Ontario?
```SQL Query:
SELECT
    SUM(sales) AS total_sales_appliances_ontario
FROM
    public.orders
WHERE
    product_category = 'Appliances' -- Ensure this matches the exact casing/spelling in your data
    AND province = 'Ontario';       -- Ensure this matches the exact casing/spelling in your data
```
  - Result:

total sales appliances ontario
------------------------------
                   202346.84
Question 4: Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers.
```SQL Query (to identify customers):

SELECT
    customer_name,
    SUM(sales) AS total_customer_sales
FROM
    public.orders
GROUP BY
    customer_name
ORDER BY
    total_customer_sales ASC
LIMIT 10;
```
  - Result (Bottom 10 Customer List):

"Jeremy Farry"      | 85.72
"Natalie DeCherney" | 125.90
"Nicole Fjeld"      | 153.03
"Katrina Edelman"   | 180.76
"Dorothy Dickinson" | 198.08
"Christine Kargatis"| 293.22
"Eric Murdock"      | 343.328
"Chris McAfee"      | 350.18
"Rick Huthwaite"    | 415.82
"Mark Hamilton"     | 450.99
