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
<img width="1800" height="1169" alt="image" src="https://github.com/user-attachments/assets/0e6b3f80-0d2e-4a3f-afba-6511c2a8ef3a" />

The conceptual model (seen above) represents the main entities and relationships in the Northline Outfitters database. The primary entities include Customers, Orders, Order_Line, Products, Vendors, Employees, Managers, Categories, and Country. Customers place orders, and each order is handled by an employee. Each employee has an manager. Each order can contain multiple order lines, where each line represents a specific product and includes details like quantity, pricing, discounts, and taxes. Products are grouped by categories and may include parent-child relationships to represent variations. Vendors supply products, and this relationship is modeled as a many-to-many relationship through the Product_Vendor table. Additionally, orders are linked to a country to track where each purchase is made. These relationships allow the data to be organized and support meaningful analysis across sales, products, employees, and vendors. 

## Data Quality Assessment:
After looking at the datasets, we noticed several quality issues that made it unsuitable to use for data analysis. First, many fields had inconsistent formats, including dates stored in multiple formats and discounts being stored in different ways such as percentages, text, and numeric values. In addition, the customer_info field combined multiple pieces of information, such as customer names and notes, into a singular column, making it difficult to analyze customer data. 

There were also inconsistencies with the product data, including the presence of alternate SKUs, parent SKUs, and slightly different product descriptions for what seemed to be the same item. Location data was also inconsistent, with variations in country names and shipping information sometimes recorded as notes such as "Same as billing" or "Dorm pickup".

Finally, some fields contained missing or incomplete values, and category names were not always standardized across the dataset. These issues created redundancy, reduced accuracy, and made it necessary to clean the data before building the database and running queries.

## Data Cleaning Process:

## Queries:
