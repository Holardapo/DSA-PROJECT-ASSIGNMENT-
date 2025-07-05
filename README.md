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
### Question 4: Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers.
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
- Advice to Management:Personalized Re-engagement Campaigns,Targeted Product Recommendations,Introduce or Highlight Loyalty Programs/Benefits

  ### Question 5: KMS incurred the most shipping cost using which shipping method?
``` SQL Query:

SELECT
    ship_mode,
    SUM(shipping_cost) AS total_shipping_cost_incurred
FROM
    public.orders
GROUP BY
    ship_mode
ORDER BY
    total_shipping_cost_incurred DESC
LIMIT 1;
```
- Result:
ship_mode   | DeliveryTruck
total_shipping cost incurred|51971.94
-Recommendations:Management should further investigate the factors contributing to this high cost, such as fuel efficiency, route optimization, maintenance, or labor costs associated with truck deliveries, to identify potential areas for cost reduction.
### Question 6: Who are the most valuable customers, and what products or services do they typically purchase?
To identify the most valuable customers, we focused on those with the highest total sales. Then, we analyzed their purchasing patterns.

``` SQL Query
- (Most Valuable Customers by Sales):

SELECT
    customer_name,
    SUM(sales) AS total_customer_sales
FROM
    public.orders
GROUP BY
    customer_name
ORDER BY
    total_customer_sales DESC
LIMIT 5;
```
```SQL Query 
- (Typical Purchases for Top Customers):

SELECT
    customer_name,
    product_category,
    SUM(sales) AS total_category_sales_for_customer,
    COUNT(*) AS number_of_orders_in_category
FROM
    public.orders
WHERE
    customer_name IN ('Emily Phan', 'Deborah Brumfield', 'Roy Skaria', 'Sylvia Foulston', 'Grant Carroll')
GROUP BY
    customer_name,
    product_category
ORDER BY
    customer_name,
    total_category_sales_for_customer DESC;
```
- Insight/Interpretation: The most valuable customers for Kultra Mega Stores are Emily Phan, Deborah Brumfield, Roy Skaria, Sylvia Foulston, and Grant Carroll, based on their different total sales contributions.
Their purchasing patterns show differs choices:
Technology Dominance: Emily Phan and Deborah Brumfield heavily favor Technology products, accounting for a large portion of their overall spending.
Furniture & Office Supplies: Grant Carroll shows a strong preference for Office Supplies and Furniture. Roy Skaria and Sylvia Foulston also make substantial purchases in Furniture and Technology, with Office Supplies being their third preference.
### Question 7: Which small business customer had the highest sales?
```SQL Query:

SELECT
    customer_name,
    SUM(sales) AS total_customer_sales
FROM
    public.orders
WHERE
    customer_segment = 'Small Business'
GROUP BY
    customer_name
ORDER BY
    total_customer_sales DESC
LIMIT 1;
```
- Result:
customer_name | Dennis Kane
total customer sales | 75967.59
- Insights/recommendations: Management should consider reaching out to Dennis Kane  to understand their needs better, offer personalized bulk discounts, or explore opportunities for upselling/cross-selling to further solidify this  relationship
### Question 8: Which Corporate Customer placed the most number of orders in 2009 – 2012?
``` SQL Query:

SELECT
    customer_name,
    COUNT(order_id) AS total_orders_placed
FROM
    public.orders
WHERE
    customer_segment = 'Corporate'
    AND order_date BETWEEN '2009-01-01' AND '2012-12-31'
GROUP BY
    customer_name
ORDER BY
    total_orders_placed DESC
LIMIT 1;
```
- Result:
customer name |Adam Hart total orders place | 27
-Recommendations:Management should recognize this customer as a vital relationship and create opportunities for deepened engagement, through dedicated account management or exclusive previews of new corporate solutions.
### Question 9: Which consumer customer was the most profitable one?
``` SQL Query:

SELECT
    customer_name,
    SUM(profit) AS total_customer_profit
FROM
    public.orders
WHERE
    customer_segment = 'Consumer'
GROUP BY
    customer_name
ORDER BY
    total_customer_profit DESC
LIMIT 1;
```
- Result:
customer name | Emily    Phantotalbcustomer profit| 34005.44
### Question 10: Which customer returned items, and what segment do they belong to?
``` SQL Query:

SELECT DISTINCT
    o.customer_name,
    o.customer_segment
FROM
    public.orders AS o
JOIN
    public.order_status AS os ON o.order_id = os.order_id
WHERE
    os.status = 'Returned';
```
- Result: The query returned 419 unique customers who have returned items. These customers belong to various segments including:
     - Home Office
     - Corporate
     - Small Business
     - Consumer
  - Recommendations for Management:
       - Investigate  Causes: KMS should  delve deeper into the reasons for these returns. Is it due to product quality issues,late deliveries, or product not meeting expectations?
       - Segment-Specific Strategies: While returns are broad, specific strategies might be needed per segment.
### Question 11: If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer.
``` SQL Query for Analysis:

SELECT
    order_priority,
    ship_mode,
    SUM(shipping_cost) AS total_shipping_cost_for_priority,
    COUNT(order_id) AS number_of_orders_for_priority_ship_mode
FROM
    public.orders
GROUP BY
    order_priority,
    ship_mode
ORDER BY
    order_priority ASC,   total_shipping_cost_for_priority DESC;
```
- Insight/Explanation: Based on the analysis, it shows that KMS is not appropriately spending shipping costs on Order Priority, particularly for high-priority orders.
- Key Observations: a.For both "Critical" and "High" priority orders, the Delivery Truck consistently incurs the highest total shipping cost. This is counter-intuitive for urgent orders, where speed should  outweigh cost-per-shipment considerations. The fastest and most expensive method, Express Air, consistently has the lowest total shipping cost and the lowest number of orders across all priority levels, including "Critical" and "High". This strongly suggests it is not being utilized for urgent shipments, where its speed would be most beneficial, despite its higher individual cost. b. Reliance on Regular Air: "Regular Air" appears to be the powerhorse for all priority levels, handling the most majority of orders. While this might be a balanced approach for medium to low priorities, its heavy use for "Critical" and "High" orders still implies that the fastest option (Express Air) is not being chosen when urgency is paramount.
  ### Key findings
- Dominant Product Category: Technology was the highest-selling product category, indicating strong market demand and a core revenue driver for KMS.
- Regional Performance Disparities: Sales were highly concentrated, with "West," "Ontario," and "Prarie" being the top-performing regions, while "Nunavut," "Northwest Territories," and "Yukon" significantly lag behind, highlighting uneven market penetration.
- High-Value Customer Profiles:
Emily Phan stands out as both the most valuable overall customer by sales and the most profitable consumer customer, making her a crucial asset. Her primary purchases are in Technology.
- Deborah Brumfield (Technology) is another top valuable customer.
Grant Carroll primarily drives sales in Office Supplies and Furniture.
- Dennis Kane is the top-performing customer within the Small Business segment.
- Adam Hart placed the most orders among Corporate customers, demonstrating consistent engagement.
- Customer Retention Opportunity (Bottom Performers): A defined group of bottom 10 customers contributes minimally to revenue, suggesting potential for targeted re-engagement.
- Significant Returns Activity: A considerable number of customers (419 unique customers) across all segments (Consumer, Corporate, Small Business, Home Office) have returned items, indicating a potentially widespread issue in product satisfaction or fulfillment.
  ### General recommendation
 -  a. Capitalize on Strengths: * Investment in Technology : Continue to prioritize inventory, marketing, and new product introductions within the Technology category, leveraging its high demand and profitability. 
- b. Address Underperforming Areas: Regional Strategy Review: Evaluate the reasons for low sales in regions like Nunavut, Northwest Territories, and Yukon. This might involve market research, targeted marketing customer.Bottom Customer Re-engagement: Develop specific re-engagement campaigns (e.g., targeted discounts, personalized recommendations, feedback surveys) to encourage repeat purchases from low-revenue customers.
- c. Maximize Operations & Customer Satisfaction:  Investigate Return Root Causes: Conduct a comprehensive analysis of returned items to identify underlying issues (e.g., product quality, inaccurate descriptions, fulfillment errors) and develop strategies to reduce return rates across all customer segments. Data-Driven Decision Making: Continuously monitor key performance indicators (KPIs) related to sales, customer segments, shipping costs, and returns to ensure ongoing strategic alignment and identify new opportunities or challenges.
