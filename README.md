# KMS-Inventory-Analysis
## **Case Scenario I**

#### **Question 1: Which product category had the highest sales?**
- **SQL Query:**
  ``` SQL
  select top 1
    product_Category,
  Sum(sales) as Total_Sales
  from DSA_Capstone_Project
  group by Product_Category
  order by product_Category desc
  ```
- **Insight/Interpretation:** The analysis reveals that "**Technology**" is the leading product category in terms of sales, generating a significant total revenue of **₦5,984,248.18 **(assuming Nigerian Naira currency). This indicates a strong market demand for technology products within Kultra Mega Stores' operations during the 2009-2012 period. Management should consider leveraging this strength, perhaps through targeted promotions or expanding product lines within this category.

#### **Question 2: what are the top 3 and bottom 3 regions in terms of sales?**
- **SQL Query (Top 3 Region):**
  ``` SQL
  select top 3
  	region,
  	sum(Sales) as Total_Sales
  from DSA_Capstone_Project
  group by Region
  order by Total_Sales desc 	
  ```
- **SQL Query (Bottom 3 Region):**
    ``` SQL
    select top 3
    	region,
    	sum(Sales) as Total_Sales
    from DSA_Capstone_Project
    group by Region
    order by Total_Sales asc
    ```
- **Insight/Interpretation:** The sales analysis by region highlights significant disparities in revenue generation across different geographical areas. The "**West**", "**Ontario**", and "**Prarie**" regions are clearly the top performers, contributing the most to overall sales. This suggests strong market presence and customer base in these areas.

Conversely, "**Nunavut**," "**Northwest Territories**," and "**Yukon**" represent the bottom three regions in terms of sales. Their significantly lower sales figures indicate either a weaker market penetration, lower population density, or specific logistical/economic challenges. KMS management should investigate the reasons behind the low performance in these regions to identify potential areas for growth or, alternatively, to optimize resource allocation if market potential is genuinely limited.

#### **Question 3: What were the total sales of appliances in Ontario?**
- **SQL Query:**
  ``` SQL
  select
  	region,
  	sum(sales) [Sales in Ontario]
  from DSA_Capstone_Project
  where Region = 'Ontario' and Product_Sub_Category = 'Appliances'
  group by region
  ```
- **Insight/Interpretation:** The total sales of **Appliances** specifically within the Ontario province amount to **₦202,346.84.** This provides a granular view of category performance in a particular region. While "Technology" is the overall highest-selling category, this figure allows KMS management to assess regional demand for specific product types and potentially tailor marketing or inventory strategies for Appliances in Ontario.

#### **Question 4: Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers.**
- **SQL Query:**
  ``` SQL
  select top 10
  	Customer_Name,
  	sum(Sales) as total_revenue
  from DSA_Capstone_Project
  group by Customer_Name
  order by total_revenue asc
  ```
- **Advice to Management:** To increase revenue from customers like **Jeremy Farry**, **Natalie DeCherney**, and others on this list, KMS should consider a targeted approach focusing on engagement and value proposition:
1. **Re-evaluate Customer Segment Alignment:** *Action:* For each of these customers, confirm their **customer_segment** (Consumer, Retail, Corporate). **Consideration:** If they are small businesses or corporate clients, perhaps they were one-off purchases or their needs have changed. A targeted sales call might be appropriate for higher-potential segments.
2. **Personalized "Re-engagement" Campaigns:** *Action:* Send personalized emails or SMS messages. **Content:** Offer small, exclusive discounts (e.g., **5-10%** off their next purchase), a special bundle tailored to their past (minimal) purchases, or a "**we love you**" offer with a limited-time validity. The goal is to entice them back to make another purchase.
3. **Feedback Collection (Surveys):** *Action:* Reach out to a sample of these customers with a short, incentivized survey (e.g., "Complete this 2-minute survey and get a small discount on your next order"). **Goal:** Understand *why* their spending is low. Is it pricing? Product availability? Customer service experience? Lack of awareness of the full product range? This direct feedback can provide invaluable insights.
4. **Introduce or Highlight Loyalty Programs/Benefits:** *Action:* Clearly communicate the benefits of any KMS loyalty program or highlight advantages of being a regular customer (e.g., free shipping thresholds, exclusive early access to sales). **Goal:** Provide an incentive for repeat purchases and increased spending.
By understanding the "**why**" behind their low spending and offering tailored incentives, KMS can potentially convert these low-revenue customers into more valuable, recurring clients.

#### **Question 5: KMS incurred the most shipping cost using which shipping method?**
- **SQL Query:**
  ``` SQL
  select top 1
  	ship_mode,
  	sum(shipping_cost) as [Total shipping cost]
  from DSA_Capstone_Project
  group by Ship_Mode
  order by [Total shipping cost] desc
  ```
- **Insight/Interpretation:** The analysis shows that "Delivery Truck" is the shipping method with the highest total incurred cost for KMS, amounting to **₦51,971.94.** This is an important finding, especially when considering operational efficiency and profitability. While delivery trucks might be preferred for certain types of goods or routes, their cumulative cost suggests they are a significant expense. Management should further investigate the factors contributing to this high cost, such as fuel efficiency, route optimization, maintenance, or labor costs associated with truck deliveries, to identify potential areas for cost reduction.

## **Case Scenario 2**
#### **Question 6: Who are the most valuable customers, and what products or services do they typically purchase?**
- **SQL Query:**
  ``` SQL
  select top 5
  	Customer_Name,
  	Product_Category,
  	sum(order_quantity * unit_price) Total_Spent
  from DSA_Capstone_Project
  group by customer_name,
  product_category
  order by Total_Spent desc
    ```
- **Insight/Interpretation:** The most valuable customers for Kultra Mega Stores are **Emily Phan**, **Deborah Brumfield**, **Dennis Kane**, **Jasper Cacioppo**, and **Clytie Kelty**, based on their significant total sales contributions.
  
  Their purchasing patterns shows:
    - **Technology Dominance:** **Emily Phan**, **Deborah Brumfield**, **Dennis Kane**, **Jasper Cacioppo**, **Clytie Kelty**, heavily favor Technology products, accounting for a large portion of their overall spending.
  
  **Recommendations for the Management:**
    - **Tailored Offers:** For the top 5 customers like **Emily Phan** and **Deborah Brumfield** etc, KMS should continue to push new technology products, accessories, and upgrades.

#### **Question 7: Which small business customer had the highest sales?**
- **SQL Query:**
    ``` SQL
    select top 1
    	customer_name,
    	sum(sales) as TotalSales
    from DSA_Capstone_Project
    where Customer_Segment = 'Small Business'
    group by customer_name
    order by TotalSales desc
    ```
- **Insight/Interpretation:** **Dennis Kane** is identified as the small business customer with the highest sales, contributing **₦75,967.59** to KMS revenue. This customer is a key asset within the small business segment. Management could consider reaching out to Dennis Kane directly to understand their needs better, offer personalized bulk discounts, or explore opportunities for upselling/cross-selling to further solidify this valuable relationship and potentially use them as a case study for attracting similar high-value small business clients.

#### **Question 8:  Which Corporate Customer placed the most number of orders in 2009 – 2012?**
- **SQL Query:**
  ``` SQL
  select top 1
  	customer_name,
  	count(Order_Quantity) as TotalOrders
  from DSA_Capstone_Project
  where Order_Date >= '2009-01-01' and Order_Date <='2012-12-31' and
  customer_segment = 'Corporate'
  group by Customer_Name
  order by TotalOrders desc
  ```
- **Insight/Interpretation:** **Adam Hart** is identified as the Corporate Customer who placed the highest number of orders **(27)** between 2009 and 2012. This indicates Adam Hart is a highly engaged and consistent corporate client for KMS. Management should recognize this customer as a key relationship and explore opportunities for deepened engagement, perhaps through dedicated account management, exclusive previews of new corporate solutions, or loyalty incentives to maintain their high order frequency.

#### **Question 9: Which consumer customer was the most profitable one?**
- **SQL Query:**
  ``` SQL
  select  top 1
  	Customer_Name,
  	sum(profit) as Total_Profit
  from DSA_Capstone_Project
  where Customer_Segment = 'Consumer'
  group by Customer_Name 
  order by Total_Profit desc
  ```
- **Insight/Interpretation:** **Emily Phan** emerges as the most profitable consumer customer for KMS, generating a total profit of ₦34,005.44. It's noteworthy that Emily Phan also appeared as one of the overall most valuable customers by sales (from Question 6), reinforcing her importance to the business. This indicates a customer who not only purchases frequently but also tends to buy items with higher profit margins. KMS should prioritize retaining and nurturing this relationship, potentially through exclusive offers on high-margin products or personalized communication, to maximize long-term profitability.

#### **Question 10: Which customer returned items, and what segment do they belong to?
- **SQL Query:**
  ``` SQL
  /* I used the anti-left join in my query, where
  the DSA_Capstone_Project table is the primary table and
  the Order_Status table is the secondary table. For the
  WHERE Clause I used the Order_Status table order ID and set its value to
  "Not NULL" */
  select distinct 
	C.Order_ID,
	C.Customer_Name,
	C.Customer_Segment,
	O.Status
  from DSA_Capstone_Project as C
  left join Order_Status as O
  on C.Order_ID = O.Order_ID
  where O.Order_ID is not null
  ```
- Result: The query returned 419 unique customers who have returned items. These customers belong to various segments including:

  - Home Office
  - Corporate
  - Small Business
  - Consumer
- **Insight/Interpretation:** A good number of customers, totaling **419 individuals/entities**, have returned items to KMS. These returns are not isolated to a single customer segment but are observed across **Home Office**, **Corporate**, **Small Business**, and **Consumer segments**. This indicates a widespread issue or characteristic behavior rather than a segment-specific problem.

  **Recommendations for Management:**
  - **Segment-Specific Strategies:** While returns are broad, specific strategies might be needed per segment. For instance, Home Office clients might value clear product descriptions, while Corporate clients might need more accurate bulk order fulfillment.
  - **Investigate Root Causes:** KMS should delve deeper into the reasons for these returns. Is it due to product quality issues, incorrect orders, late deliveries, product not meeting expectations, or complex return policies? Analyzing product_id and reason (if available in another table) for returned orders could provide more specific insights.
  - **Return Policy Review:** Evaluate the existing return policy to ensure it is clear, fair, and not inadvertently encouraging returns.
 
#### **Question 11: f the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer.**
- **SQL Query:**
  ``` SQL
  select 
  	Order_Priority,
  	Ship_Mode,
  	count(*) Total_Orders,
  	sum(shipping_cost) Total_Shipping_Cost,
  	avg(shipping_cost) Avg_Shipping_Cost
  from DSA_Capstone_Project
  group by Order_Priority, Ship_Mode
  order by Order_Priority, Total_Shipping_Cost desc 
  ```
- **Insight/Explanation:** Based on the analysis, it appears that KMS is **NOT optimally** or appropriately spending shipping costs based on **Order Priority**, particularly for high-priority orders.

  **Key Observations:** 
  1. **Mismatch for High and Critical Priorities:** For both "**Critical**" and "**High" priority orders**, the **Delivery Truck** (described as the slowest and most economical method) consistently incurs the highest total shipping cost. This is counter-intuitive for urgent orders, where speed should theoretically outweigh cost-per-shipment considerations. * The fastest and most expensive method, Express Air, consistently has the lowest total shipping cost and the lowest number of orders across all priority levels, including "**Critical**" and "**High**". This strongly suggests it is being underutilized for urgent shipments, where its speed would be most beneficial, despite its higher individual cost.
  2. **Appropriate for Low/Medium/Not Specified:** For "**Low**", "**Medium**", and "**Not Specified**" priorities, the higher usage and total cost for "Delivery Truck" and "Regular Air" are more justifiable, as these orders are less time-sensitive, and cost efficiency would be a higher priority.
  3.  **Reliance on Regular Air:** "**Regular Air**" appears to be the workhorse for all priority levels, handling the vast majority of orders. While this might be a balanced approach for medium to low priorities, its heavy use for "Critical" and "High" orders (despite Delivery Truck having higher total cost) still implies that the fastest option (Express Air) is not being chosen when urgency is paramount.
     
   **Conclusion and Recommendations:** The current spending pattern indicates a potential disconnect between stated order priority and the chosen shipping method. KMS might be sacrificing delivery speed for urgent orders to save on per-shipment costs, which could negatively impact customer satisfaction for critical deliveries.

    **The Management should:**
  - **Cost-Benefit Analysis for Urgency:** Conduct a detailed cost-benefit analysis comparing the increased shipping cost of "**Express Air**" for critical orders against the potential loss of customer satisfaction, repeat business, or contractual penalties due to slow delivery.   
  - **Optimize Delivery Truck Use:** While economical, if "**Delivery Truck**" has the highest total cost for urgent orders, it may indicate inefficiencies in routing, capacity utilization, or a need to shift some of these urgent orders to faster, albeit pricier, modes.

## **Key Findings & Recommendations**
This sales and order analysis for Kultra Mega Stores (KMS) from **2009 to 2012** provides critical insights into sales performance, customer behavior, and operational efficiency across various segments and regions.

#### **Key Findings:**
- **Dominant Product Category:** Technology emerged as the highest-selling product category, indicating strong market demand and a core revenue driver for KMS.
- **Regional Performance Disparities:** Sales are highly concentrated, with "West**", "**Ontario**", and "**Prarie**" being the top-performing regions, while "**Nunavut**", "**Northwest Territories**", and "**Yukon**" significantly lag behind, highlighting uneven market penetration.
- **High-Value Customer Profiles**
- **Dominant Product Category:** Technology emerged as the highest-selling product category, indicating strong market demand and a core revenue driver for KMS.
- **Customer Retention Opportunity (Bottom Performers):** A defined group of bottom 10 customers contributes minimally to revenue, suggesting potential for targeted re-engagement.
- **Significant Returns Activity:** A considerable number of customers (419 unique customers) across all segments (Consumer, Corporate, Small Business, Home Office) have returned items, indicating a potentially widespread issue in product satisfaction or fulfillment.
- **uboptimal Shipping Cost Management:** Despite "Delivery Truck" being the slowest and most economical, it incurs the highest total shipping costs for "**Critical**" and "**High**" priority orders. Conversely, "Express Air" (fastest, most expensive) is significantly underutilized for these urgent shipments. This suggests a disconnect between order priority and shipping method selection.

#### **Overall Recommendations:**
1. **Capitalize on Strengths:** **Invest in Technology Segment:** Continue to prioritize inventory, marketing, and new product introductions within the Technology category, leveraging its high demand and profitability.
2. **Deepen Engagement with Top Customers:** Implement personalized loyalty programs, exclusive offers, and dedicated account management for high-value customers like Emily Phan, Deborah Brumfield, Dennis Kane, and Adam Hart, tailored to their specific purchasing behaviors.
3. **Address Underperforming Areas:** Regional Strategy Review: Investigate the reasons for low sales in regions like "**Nunavut**", "**Northwest Territories**", and "**Yukon**". This might involve market research, targeted marketing campaigns, or re-evaluation of logistical feasibility.
4. **Bottom Customer Re-engagement:** Develop specific re-engagement campaigns (e.g., targeted discounts, personalized recommendations, feedback surveys) to encourage repeat purchases from low-revenue customers.
5. **Optimize Operations & Customer Satisfaction:** Investigate Return Root Causes: Conduct a comprehensive analysis of returned items to identify underlying issues (e.g., product quality, inaccurate descriptions, fulfillment errors) and develop strategies to reduce return rates across all customer segments.
6. **Refine Shipping Strategy:** Re-evaluate the shipping method selection process, particularly for high-priority orders. Ensure that faster, more appropriate shipping methods (like Express Air) are utilized for "Critical" and "High" priority orders, even if individual costs are higher, to maintain customer satisfaction and service level agreements. A detailed cost-benefit analysis comparing expedited shipping with customer retention and satisfaction should be performed.
7. **Data-Driven Decision Making:** Continuously monitor key performance indicators (KPIs) related to sales, customer segments, shipping costs, and returns to ensure ongoing strategic alignment and identify new opportunities or challenges.
