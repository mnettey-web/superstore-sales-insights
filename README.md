# Superstore Sales Insights

<img width="1125" height="978" alt="image" src="https://github.com/user-attachments/assets/4b1742a2-17e2-4284-abef-d2c5dd76255a" />

A comprehensive retail data pipeline: SQL for extraction, Python for preprocessing, and Power BI for executive-level business intelligence


## Introduction
Data is only as valuable as the decisions it inspires. In this project, I took the Global Superstore dataset a massive collection consisting of 51,290 international retail transactions with a set of attributes describing orders, customers, products, geography, and financial metrics and treated it as a real-world business intelligence engagement.

Rather than just cleaning rows and columns, I focused on the "so what?". I transformed messy, multinational data into a strategic roadmap designed to help executives answer three critical questions: 

  - Where is our growth hidden? (Revenue)
  - Where are we losing money? (Margins)
  - How can we work smarter? (Operations)

Source: Kaggle




## Business Problem
Global Superstore generates strong revenue but experiences inconsistent profitability across regions and product categories. Leadership seeks to understand key profit drivers and evaluate the impact of discounting strategies on financial performance.
This project analyzes sales, profit, discount behavior, and customer segmentation to identify improvement opportunities and deliver actionable recommendations.



## Data Understanding & Preparation
The dataset contains transactional order-level data, where each row represents a product line item within an order. The dataset includes sales, profit, discount, customer segment, product category, and regional information.
- Initial exploration revealed:
  - The data spans multiple years.
  - Several transactions contain negative profit values.
  - Discounts vary significantly, suggesting potential impact on margins.
  - No critical missing values were identified in financial columns.

Additional derived metrics such as Profit Margin and Shipping Duration were created to support deeper analysis.




## Data Dictionary 
#### Orders Table
| Column Name | Description | Typical Data Type | Sample Value |
| :--- | :--- | :--- | :--- |
| **Row ID** | Surrogate unique identifier for each row/transaction record. | Integer / Unique ID | `32298` |
| **Order ID** | Identifier for an order (can span multiple line items). | String / Text | `CA-2022-152156` |
| **Order Date** | Date the order was placed. | Date | `2022-11-08` |
| **Ship Date** | Date the order was shipped. | Date | `2022-11-11` |
| **Ship Mode** | Shipping method used (e.g., Standard Class, Second Class). | Categorical | `Second Class` |
| **Customer ID** | Unique identifier for the customer placing the order. | String | `CG-12520` |
| **Customer Name** | Full name of the customer. | Text | `Claire Gute` |
| **Segment** | Customer segment (e.g., Consumer, Corporate, Home Office). | Categorical | `Consumer` |
| **Country** | Country where the order originated/delivered. | Categorical | `United States` |
| **City** | City of the delivery location. | Categorical | `Henderson` |
| **State** | State/Province of delivery. | Categorical | `Kentucky` |
| **Postal Code** | ZIP/postal code for geographic grouping. | Numeric / Text | `42420` |
| **Market** | Geographic market or trading region grouping. | Categorical | `US` |
| **Region** | Broader region grouping of the market (e.g., West, South). | Categorical | `South` |
| **Product ID** | Unique identifier for each product/SKU. | String | `FUR-CH-10000454` |
| **Category** | High-level product category (e.g., Furniture, Technology). | Categorical | `Furniture` |
| **Sub-Category** | More detailed product classification under Category. | Categorical | `Chairs` |
| **Product Name** | Descriptive name of the product. | Text | `Hon Deluxe Fabric Upholstered Stacking Chairs` |
| **Sales** | Total sales revenue for that transaction line. | Numeric (currency) | `731.94` |
| **Quantity** | Number of units sold in that order line. | Integer | `3` |
| **Discount** | Discount applied to the sale (proportion). | Numeric | `0.0` |
| **Profit** | Profit amount realized on the sale (could be negative). | Numeric | `219.58` |
| **Shipping Cost** | Cost incurred to ship the order. | Numeric | `32.50` |
| **Order Priority** | Priority level of the order (e.g., High, Medium, Low). | Categorical | `Medium` |



#### Returns Table
| Column Name | Description | Typical Data Type | Sample Value |
| :--- | :--- | :--- | :--- |
| **Returned** | Indicates if a customer has sent back an item. | Boolean / Cattegorical | `Yes` |
| **Order ID** | Identifier for an order (can span multiple line items). | String / Text | `CA-2022-152156` |
| **Market** | Geographic market or trading region grouping. | Categorical | `US` |




#### Sales Rep Table
| Column Name | Description | Typical Data Type | Sample Value |
| :--- | :--- | :--- | :--- |
| **People** | Full name of the sales reporesentative. | Text | `Anna Andreadi` |
| **Region** | Broader region grouping of the market (e.g., West, South). | Categorical | `South` |



#### Sample Order Sheet
<img width="1211" height="559" alt="image" src="https://github.com/user-attachments/assets/232ff466-f6a0-42d3-97fa-f17a1752181d" />



### Create staging tables to load data 
<img width="805" height="735" alt="image" src="https://github.com/user-attachments/assets/fe2352af-0c54-4f45-bdd1-3759e5905365" /> 


### Checking Data types using SQL and Python
 <img width="975" height="468" alt="image" src="https://github.com/user-attachments/assets/8eb79460-6a3b-41ad-b2cb-4c6d0bf6d3fb" />
 <img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/621fe9b7-af10-4605-b612-8441f4698dc4" />


 
	
## Data Cleaning & Transformation
