# Group 2 MIST4610 Group Project 2

## Team Name:
21484 Group A2

## Team Members: 
1. Roshni Chaudhury - Group Leader
2. Malia Bender - Conceptual Modeler
3. Alexander Davidow - Database Designer
4. Justin Rather - Data Wrangler
5. Samira Gulyamov - SQL Writer

## Case Summary:
Northline Outfitters is a small, online retail company that sells lifestyle and tech accessories to customers in the United States and Canada. The company purchases products from external vendors and currently stores much of its operational data in Excel rather than in a structured database. 

Because of this, the data contains several issues, including inconsistent formatting, duplicate records, and unorganized fields such as customer information stored in a single column. These problems make it difficult to analyze data and limit the company's ability to generate accurate insights. 

The goal of this project is to clean and standardize the data, design a relational database model, and use SQL queries to answer key business questions. This process demonstrates how proper data organization improves accuracy, reduces redundancy, and supports better decision-making. 

## Conceptual Model:
<img width="1047" height="990" alt="image" src="https://github.com/user-attachments/assets/1a8a916a-e880-4549-a135-f04f717d489c" />




The conceptual model represents the Northline Outfitters order management system composed of several key entities and their relationships. The central entity is Orders, which captures each transaction and is linked to both Customers and Employees, reflecting that each order is placed by one customer and processed by an employee. Each employee and customer can be associated with many orders through a one-to-many relationshop. Each order consists of one or more Order_Line records, representing the individual products within the order, which is shown through the one-to-many relationship between Orders and Order_Line. The Product entity stores information about items available for sale and is connected to Order_Line, as each item refrences a single product, while each product can appear in many order lines. Products are futher categorized in the entity Categories, where each product belongs to one category and each category contains multiple products. Products are also connected to Vendors through the Product_Vender associative entity, which represents a many-to-many relationship between products and vendors. Additionally, employees are organized under Managers in a hiearchical relationship. Overall, this model structures customer, product, order, and organizational data in a way that supports effective and efficient analysis. 

## Data Quality Assessment:
The original dataset we were given contained several data quality isssues that made it unsuitable for analysis and modeling. One of the main issues was the presence of non-atomic data, particularly in the shipping location field, where city and state were combined (e.g., Toronto,ON) and sometimes replaced with non-standard entries like "Same as billing" and "Dorm pickup". This created inconsistences and violated normalization principles. There were also inconsistences with numerical formats in fields like discounts and tax, where values were represented as both percents and decimal numbers. Additionally, there were more inconsistencies in the data with text formatting, such as product descriptions appearing in different cases which led to duplicate and mismatch records. The dataset also included mixed units of measurement in fields such as size and weight which made comparisons difficult. Missing or incomplete values were present throughout the data, including tax and line total fields, which would result in possible incorrect calculations. Finally, some columns such as notes contained unstructured data that varied in format and meaning. These issues, along with others documented in the cleaning log, reduced the overall accuracy and reliability of the dataset prior to cleaning. 

## Data Cleaning Process:
To address the data quality issues identified above, a series of cleaning and transformation steps were preformed within the dataset and documented in the cleaning log. First, non-atomic fields were corrected by splitting the combined shipping location into separate attributes, ship_city and ship_state. Invalid or non-standard entries were removed and replaced with null values. The shipping country field was also standardized into a separate attribute to support analysis. Additionally, we also split customer names into first and last name attributes. All of these steps were taken to make sure the data did not violate normalization.

Next, inconsistencies in numeric fonts were fixed. Fields like discount and tax, which were originally recorded using a mix of percentage values and decimals, were standardized into consistent decimal values. Numeric fields including unit price, tax, and line total were corrected to ensure proper formatting. 

Text fields were also standardized to improve consistency. Product descriptions were formatted uniformly to elimate duplicates caused by spelling or capitalization inconsistency. Additionally, categorical fields such as return flags were standardized. 

Finally, the cleaned data was reorganized to align with the database model. Data was prepared for import into separate tables, ensuring reduced redundancy. These steps are all logged in our data cleaning log and overall improved accurancy and consistency. 
## Queries:

1.	Which products generated the highest total sales revenue, by country?

<img width="1353" height="523" alt="image" src="https://github.com/user-attachments/assets/6e301048-1408-4920-9c01-4c9549583580" />



Business Justification: 
The reason this could be important for Northline Outfitters is because it allows them to focus their marketing efforts into certain countries that perform better than others and/or leave certain markets if they are severely underperforming.

2.	Which employees handled the largest number of orders, and how do their results compare with other employees under the same manager?

<img width="1366" height="608" alt="image" src="https://github.com/user-attachments/assets/7221e8f7-fd26-4d10-8f22-636faf1215c1" />

Business Justification: 
The reason this could be important for Northline  Outfitters is because it shows higher levels of management how different employees are doing at the selling level which could be important for performance evaluations or figuring out root causes in case revenue is dropping.

3.	Which vendors supply products that appear in more than one category?

<img width="1334" height="519" alt="image" src="https://github.com/user-attachments/assets/7e70c37d-1b8a-450c-afdb-8ed84d6fbf1a" />


Business Justification:


4.	Which customers generate the most total revenue?

<img width="1365" height="522" alt="image" src="https://github.com/user-attachments/assets/94768084-bb19-4149-b97b-7b2e80cfa3d3" />


Business Justification:


5.	Which products are sold the most in terms of quantity?

<img width="1335" height="522" alt="image" src="https://github.com/user-attachments/assets/edeeabfc-f59c-4cee-bbda-dc4cda6c9b0d" />


Business Justification:


6.	Which product categories generate the most revenue?

SELECT 
    cat.Category_name,
    SUM(ol.line_total) AS total_revenue
FROM Category cat
JOIN Product p 
    ON cat.Category_ID = p.Category_Category_ID
JOIN Order_Line ol 
    ON p.Product_sku = ol.Product_Product_sku
GROUP BY 
    cat.Category_name
ORDER BY total_revenue DESC;

Business Justification:
