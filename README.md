# Coffee Sales Analysis 

In this project, I developed an interactive Excel dashboard to analyze and visualize coffee sales data across different markets. The dashboard aims to achieve three main objectives:   

- Monitor sales performance over time across different coffee types (Arabica, Excelsa, Liberica, and Robusta) to identify sales trends and patterns 

- Analyze sales distribution across geographic markets (United States, Ireland, and United Kingdom) to understand market performance 

- Track customer buying behavior through top customer analysis and loyalty card data to inform customer relationship management strategies 

## Data Overview

The data is the [Coffee Beans Sales](https://www.kaggle.com/datasets/saadharoon27/coffee-bean-sales-raw-dataset), already downloaded from [Kaggle](https://www.kaggle.com). The dataset consists of three data tables: 
| **Table Name**     	            | **Column Names**     |**Function**|
|-------------------	        |------------------	       |------------------	       |
| **Orders**     	                | Order ID (Primary Key)<br>Order Date<br>Customer ID<br>Product ID<br>Quantity                                                            |Contains transaction details|
| **Customers**    	              | Customer ID (Primary Key)<br>Customer Name<br>Email<br>Phone Number<br>Address Line 1<br>City<br>Country<br>Postcode<br>Loyalty Card         |Stores customer information|
| **Products**               	    | Product ID (Primary Key)<br>Coffee Type<br>Roast Type<br>Size<br>Unit Price<br>Price Per 100g<br>Profit 	                                     |Contains product details|

Data quality assessment revealed no duplicate entries across all columns, ensuring data integrity for analysis.

## Data Transformation

**Data Integration**

With data initially distributed across three tables, efficient analysis was hindered by the need for constant cross-referencing. By consolidating relevant information from _Customers_ and _Products_ tables into the _Orders_ table, we created a single source of truth that streamlines analysis, simplifies the creation of pivot tables and visualization, and minimizes potential lookup errors. 

- Customer data retrieval: I implemented **XLOOKUP** function to retrieve customer information (Customer Name, Email, Country, and Loyal Card) from the _Customers_ table. This formula was chosen due to its ability to look up values in both directions. 

- Product data retrieval: I utilized **INDEX MATCH** combination to retrieve Coffee Type, Roast Type, Size, and Unit Price from the _Products_ table. This approach allowed us to write a single dynamic formula that could be applied across all product-related columns, offering better flexibility and performance than multiple individual lookups. 

- Sales Calculation: Created _Sales_ column by multiplying _Quantity_ with _Unit Price_. 

**Data Cleanup and Standardization**

_**Email Data Management:**_  

- Challenge: Missing values in _Email_ column appeared as zeros in lookup results. 

- Solution: Implemented **IF** statement with **XLOOKUP** to convert zeros to blank cells.

_**Product Name and Roast Type Enhancement:**_

- Challenge: _Coffee Type_ column and _Roast Type_ column contain abbreviations. 

- Solution: Created _Coffee Type Name_ column using **nested IF** statements to convert the abbreviations to their respective full names ("Rob" to "Robusta", "Ara" to "Arabica", "Exc" to "Excelsa", and "Lib" to "Liberica"). Similarly, _Roast Type Name_ column was added to transform "M" to "Medium", "L" to "Light", and "D" to "Dark". This would enhance the comprehensibility of the data.

_**Numerical and Date Formatting:**_

- Standardized _Order Date_ to "DD-MMM-YYYY" format to avoid potential confusion between different date formats, especially between European and American date formats. 

- As the _Size_ column lacked the metric, I added "kg" unit to Size values (e.g., "0.5" → "0.5 kg"). 

- Applied USD currency format ($) to _Unit Price_ and _Sales_ columns.

_**Data Structure Optimization:**_

The data range was converted to a table format named _"Orders"_. This enables automatic expansion for new data entries and maintains dynamic connections with pivot tables and graphs, eliminating manual refresh requirements and reducing potential analysis errors. 

## Dashboard Development

The dashboard was constructed using Pivot tables and charts for data aggregation and visualization. 

![Dashboard](https://github.com/Satori-NgN/Coffee-Sales-Analysis/blob/9f41b2c5cfcd3b09a1611d6751b2779ed708afda/Coffee%20Sales%20Dashboard.png)

[Interactive Dashboard](https://studentcbs-my.sharepoint.com/personal/hong23ac_student_cbs_dk/_layouts/15/Doc.aspx?sourcedoc={3b8bc96e-b39f-47a9-9246-3f7a1887ba93}&action=embedview&AllowTyping=True&wdHideGridlines=True&wdHideHeaders=True&wdDownloadButton=True&wdInConfigurator=True&wdInConfigurator=True) can be found here!

**Interactive Controls**

- Timeline filter (2019-2022) for temporal analysis 

- Three integrated slicers:  

  - Roast type (Dark/Medium/Light) 

  - Package size (0.2kg/0.5kg/1.0kg/2.5kg) 

  - Loyalty card status (Yes/No) 

- Synchronized filtering across all visualizations.

**Key visualizations**

1. Total Sales Over Time:  

- Line chart tracking sales trends by coffee type (Arabica, Excelsa, Liberica, Robusta) 

- Color-coded for easy coffee type differentiation 

2. Sales by Country:  

- Bar chart showing sales distribution across the US, Ireland, and UK 

- Hierarchical arrangement by sales volume 

3. Top 5 Customers Analysis:  

- Bar chart highlighting highest-value customers 

- Hierarchical arrangement by sales volume

All three charts are responsive to timeline and slicer selections.

## Key Insights

**Key Insights**

_**Market Performance:**_

- United States dominates sales volume, followed by Ireland and the UK, showing strong North American presence 

- Notable shift in market dynamics from 2020 onwards, with increased volatility compared to stable 2019 patterns 

- 2022 shows intense peaks followed by declining trends, suggesting a changing market environment

_**Product Performance:**_

- All coffee types show high volatility, with peaks reaching 800+ USD and troughs around 100 USD, highlighting the need for robust inventory management 

- Arabica and Liberica reached peak sales (800+ USD) in late 2021 and early 2022 respectively, while Robusta maintains more moderate but stable levels, indicating different market positioning 

- Coffee types typically peak at different times, with one product's rise often coinciding with others' decline, indicating product substitution behavior 

- Light roast dominates sales over Medium and Dark, revealing a clear market preference for milder coffee flavors. This suggests potential for targeted marketing and inventory optimization focused on light roast products.

_**Customer Behavior:**_

- Strong preference for bulk packaging with 2.5kg and 1kg leading sales, suggesting a significant wholesale or B2B customer base 

- Smaller packages (0.5kg and 0.2kg) show notably lower sales, indicating retail is not the primary market 

- Balanced distribution between non-loyalty and loyalty card holders shows effective program engagement with potential for expansion.

