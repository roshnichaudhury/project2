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
<img width="2575" height="2013" alt="IMG_8575" src="https://github.com/user-attachments/assets/44b37a25-551e-48a2-bdcc-f6708d3fc350" />



## Data Quality Assessment:

## Data Cleaning Process:

## Queries:

1.	Which products generated the highest total sales revenue, by country?

SELECT 
//    c.Country_name,
    p.Product_sku,
    p.Product_description,
    SUM(ol.line_total) AS total_revenue
FROM Orders o
JOIN Country c 
    ON o.Country_code = c.Country_code
JOIN Order_Line ol 
    ON o.Order_ID = ol.Orders_Line_ID
JOIN Product p 
    ON ol.Product_Product_sku = p.Product_sku
GROUP BY 
    c.Country_name,
    p.Product_sku,
    p.Product_description
ORDER BY 
    c.Country_name,
    total_revenue DESC;

Business Justification: 
The reason this could be important for Northline Outfitters is because it allows them to focus their marketing efforts into certain countries that perform better than others and/or leave certain markets if they are severely underperforming.

2.	Which employees handled the largest number of orders, and how do their results compare with other employees under the same manager?

SELECT 
    e.Employee_ID,
    e.Manager_Manager_ID,
    COUNT(o.Order_ID) AS total_orders
FROM Employee e
LEFT JOIN Orders o 
    ON e.Employee_ID = o.Employee_ID
GROUP BY 
    e.Employee_ID,
    e.Manager_Manager_ID
ORDER BY 
    e.Manager_Manager_ID,
    total_orders DESC;

Business Justification: 
The reason this could be important for Northline  Outfitters is because it shows higher levels of management how different employees are doing at the selling level which could be important for performance evaluations or figuring out root causes in case revenue is dropping.

3.	Which vendors supply products that appear in more than one category?

SELECT 
    v.Vendor_ID,
    v.Vendor_name,
    COUNT(DISTINCT p.Category_Category_ID) AS category_count
FROM Vendor v
JOIN Product_vendor pv 
    ON v.Vendor_ID = pv.Vendor_Vendor_ID
JOIN Product p 
    ON pv.Product_Product_sku = p.Product_sku
GROUP BY 
    v.Vendor_ID,
    v.Vendor_name
HAVING COUNT(DISTINCT p.Category_Category_ID) > 1;

Business Justification:


4.	Which customers generate the most total revenue?

SELECT 
    c.Customer_ID,
    c.Customer_F_name,
    c.Customer_L_name,
    SUM(ol.line_total) AS total_spent
FROM Customers c
JOIN Orders o 
    ON c.Customer_ID = o.Customer_ID
JOIN Order_Line ol 
    ON o.Order_ID = ol.Orders_Line_ID
GROUP BY 
    c.Customer_ID,
    c.Customer_F_name,
    c.Customer_L_name
ORDER BY total_spent DESC;

Business Justification:


5.	Which products are sold the most in terms of quantity?

SELECT 
    p.Product_sku,
    p.Product_description,
    SUM(ol.Quantity) AS total_quantity_sold
FROM Product p
JOIN Order_Line ol 
    ON p.Product_sku = ol.Product_Product_sku
GROUP BY 
    p.Product_sku,
    p.Product_description
ORDER BY total_quantity_sold DESC;

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
