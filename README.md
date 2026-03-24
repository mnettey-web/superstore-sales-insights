# Global Superstore Profitability & Strategic Analysis

#### Turning 51,000+ International Transactions into a Strategic Growth Roadmap

<img width="1125" height="978" alt="image" src="https://github.com/user-attachments/assets/4b1742a2-17e2-4284-abef-d2c5dd76255a" />

A comprehensive retail data pipeline: SQL for extraction, Python for preprocessing, and Power BI for executive-level business intelligence


# Introduction
Data is only as valuable as the decisions it inspires. In this project, I took the Global Superstore dataset a massive collection consisting of 51,290 international retail transactions with a set of attributes describing orders, customers, products, geography, and financial metrics and treated it as a real-world business intelligence engagement.

Rather than just cleaning rows and columns, I focused on the "so what?". I transformed messy, multinational data into a strategic roadmap designed to help executives answer three critical questions: 

  - Where is our growth hidden? (Revenue)
  - Where are we losing money? (Margins)
  - How can we work smarter? (Operations)

Source: Kaggle


# Business Problem
Global Superstore generates strong revenue but experiences inconsistent profitability across regions and product categories. Leadership seeks to understand key profit drivers and evaluate the impact of discounting strategies on financial performance.

The core problem is leadership lacks visibility on company’s profit landscape, high performing regions were masking losses in underperforming sectors, and aggressive discounts intended to win customers were quietly destroying margins. Without insights into which product categories, customer segments and regions are driving value, strategic investments were made in the dark. 

To address this business problem, this project analyzes sales, profit, discount behavior, and customer segmentation to identify areas of opportunities and deliver recommendations aimed at improving revenue and identify markets requiring marketing efforts.

*Insight: I discovered that in some regions, a 20% discount actually led to a 40% drop in net profit a dynamic that was invisible before this analysis*


# Business Objectives & Scope
This project analyzes sales, profit, discount behavior, and customer segmentation to identify improvement opportunities and deliver actionable recommendations to improve financial performance. As such, this analysis will focus on;
- Sales performance
- Analysis of profit drivers
- Evaluating impacrt of discount
- Customer segment performance
- Comparing regional profits
- Product category and sub-category performance


# Hypotheses
Before diving into the data, I am testing the following business assumptions:
- ***Hypotheses A:*** Higher discounts are negatively correlated with profit margins.
- ***Hypotheses B:*** Some categories generate high revenue but low profitability due to heavy discounting (e.g. Furniture category).
- ***Hypotheses C:*** Consumer customers have highest profit as compared to Corporate customers.
- ***Hypotheses D:*** Certain regions are unprofitable regardless of sales volume


# Dataset Overview
The dataset contains order-level transactional data, where each row represents a single item from a customer’s order.

**Total Records:** 51,290 across 147 countries 

**Scope:** Multi-year, multinational retail transactions ranging from 2017-2020
| Data Category | Key Variables | Business Significance |
| :--- | :--- | :--- |
| **Temporal** | Order Date, Ship Date | Measures shipping performance and spot seasonal demand and track delivery delays. |
| **Geographic** | Market, Region, Country, State | Essential for identifying areas where sales are high and areas where costs are hurting the bottom line. |
| **Product** | Category, Sub-Category, Product Name | Help identify items being sold and separate high-volume items from items with the best profit margins. |
| **Financial** | Sales, Quantity, Discount, Profit, Shipping Cost | The core metrics used to calculate the return on investment (ROI). |
| **Customer** | Segment (Consumer, Corporate, Home Office) | Allows for easy identification on the types of customers that are profitable. |



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



# Data Understanding & Preparation
The dataset contains transactional order-level data, where each row represents a product line item within an order. The dataset includes sales, profit, discount, customer segment, product category, and regional information.
- Initial exploration revealed:
  - The data spans multiple years.
  - Several transactions contain negative profit values.
  - Discounts vary significantly, suggesting potential impact on margins.
  - No critical missing values were identified in financial columns.

Additional derived metrics such as Profit Margin and Shipping Duration were created to support deeper analysis.



## Data Engineering Process
Before conducting the analysis, the dataset was structured and validated to ensure the insights generated were reliable.


### Data Staging & Data Loading
The raw dataset was first loaded into SQL staging tables to fix any formatting issues. This step ensured that the structure of the messy raw dataset, including column formats and data types was separate from cleaned data.

#### Create staging tables to load data 
<img width="805" height="735" alt="image" src="https://github.com/user-attachments/assets/fe2352af-0c54-4f45-bdd1-3759e5905365" /> 


#### Data Validation 
The dataset was reviewed using SQL and Python to check financial records for missing or incomplete records that could affect analysis and have a better understanding of the timeframe for transactions.
<img width="676" height="522" alt="image" src="https://github.com/user-attachments/assets/9e6d68b6-fcce-4bdf-a611-5fbdaaadb496" />
<img width="769" height="366" alt="image" src="https://github.com/user-attachments/assets/0364b234-c0b0-4682-8667-04e48662fc7f" />



#### Checking Data types using SQL and Python
<img width="708" height="477" alt="image" src="https://github.com/user-attachments/assets/8074ffa7-1783-4e4e-a5a5-5a243058ad19" />



	
## Data Cleaning & Transformation
The dataset was then refined to improve analytical accuracy. 
- Duplicate order-product combinations were removed.
- Null or missing discount values were standardized to zero to maintain consistency in calculations.
- Financial fields were validated to prevent calculation errors and review transactions with negative profit values.
- Derived metrics such as Profit Margin and Shipping Duration were created.
- Time-based features (Year, Quarter, Month) were generated to support trend analysis.
A clean analytical view was created to streamline dashboard development and ensure consistent KPI calculations.
<img width="716" height="709" alt="image" src="https://github.com/user-attachments/assets/54ba79c7-11df-4a6f-b67f-958231674cad" />
<img width="778" height="365" alt="image" src="https://github.com/user-attachments/assets/c53977ab-08f6-4f24-88d7-808ea9a4ef7b" />
<img width="868" height="700" alt="image" src="https://github.com/user-attachments/assets/97ecddf0-102d-4d51-9621-1e0e91ee0cc7" />
<img width="883" height="211" alt="image" src="https://github.com/user-attachments/assets/4d3b7f1d-c036-4647-b99c-ab3785cb84b6" />




## Feature Engineering
To support deeper business analysis, several derived fields were created:
- Profit Margin to track performance at the bottom line against revenue.
- Shipping Duration to measure the time from when an order is received until it is handed to the carrier.
- Time-based attributes such as Year, Quarter, and Month to enable trend and seasonal analysis.

<img width="868" height="450" alt="image" src="https://github.com/user-attachments/assets/4d4a71e1-3adb-41d1-a085-6fc94add6a7d" />




# Exploratory Data Analysis
The exploratory analysis centered on identifying key profit drivers by region, product category, and customer segment.
Key findings include:
- Certain regions generate strong sales but weak margins.
- The Furniture category shows high revenue but inconsistent profitability.
- Profit margins decline significantly when discounts exceed 30%.
- Corporate customers demonstrate higher average profit per order.
These insights validate the initial hypotheses and highlight opportunities for strategic improvement.

**Note:**
Prior to performing EDA on the dataset, the clean data set will be used to ensure the data is accurate and consistent, to extract meaningful insights and prepare for advanced modeling
<img width="997" height="654" alt="image" src="https://github.com/user-attachments/assets/1c32e5d3-4ab2-4149-b5ea-5eddb63e9950" />





## ***Hypotheses A:*** Higher discounts are negatively correlated with profit margins 
The insights below support the assumptions that the profit margins decline significantly when discounts are high or exceed 30%. First, we will review profit margins by discount range to identify the primary cause of profit loss. To dive deeper, we will evaluate impact of discounts on sales and profits. To conclude, a correlation between discount and profit will reveal how heavy discounts impact the bottom line. 

***Note: Profit Margin calculation***      <img width="451" height="72" alt="image" src="https://github.com/user-attachments/assets/dd580f53-1a51-48b2-a350-d9c8afc26567" />



### Profit Margin by Discount Range
<img width="851" height="710" alt="image" src="https://github.com/user-attachments/assets/054b962d-6671-4b76-9dbf-a1b4a776e6cc" />




### Correlation between discount and profit
<img width="820" height="524" alt="image" src="https://github.com/user-attachments/assets/89457715-8dc3-4ffb-9c23-11c6bd869f8c" />






## ***Hypotheses B:*** Some categories generate high revenue but low profitability due to heavy discounts (e.g. Furniture category).
<img width="882" height="620" alt="image" src="https://github.com/user-attachments/assets/6e79d7ed-3622-4f6b-b476-d8b2157199bc" />


<img width="888" height="737" alt="image" src="https://github.com/user-attachments/assets/b8ae7e6a-cc65-410c-92d4-4abaf90bf63c" />





## ***Hypotheses C:*** Consumer customers have higher profit per order compared to corporate customers.

***Note: Revenue calculation***      <img width="416" height="93" alt="image" src="https://github.com/user-attachments/assets/5fe2785e-8839-4ec5-93e6-fae94cb5e3e0" />

<img width="863" height="759" alt="image" src="https://github.com/user-attachments/assets/20514ee6-789d-49e5-a5f6-c0c8ec7e6137" />

<img width="867" height="525" alt="image" src="https://github.com/user-attachments/assets/d4820f94-8ede-4433-bbb1-fa434391c610" />





## ***Hypotheses D:*** Certain regions are unprofitable regardless of sales volume.
<img width="823" height="395" alt="image" src="https://github.com/user-attachments/assets/1ca0d51c-d944-473a-bda8-4219ecc3e1c2" />

<img width="847" height="720" alt="image" src="https://github.com/user-attachments/assets/4e71b349-d316-4499-85ee-7133fc418f3a" />

<img width="824" height="265" alt="image" src="https://github.com/user-attachments/assets/727d3583-5bab-4648-83ce-acc6c9cdc31f" />



