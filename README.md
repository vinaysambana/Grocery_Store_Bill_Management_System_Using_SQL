 📜🛒🗂️Grocery Store Billing Management System (MySQL)📱

# Grocery_Store_Bill_Management_System_Using_SQL : 
----------------------------------------------------
A Grocery Store Billing Management System built using MySQL, includes inventory tracking, bill generation, payment status management, sales reports, stored procedures, triggers, views, and SQL queries for analyzing sales and stock levels. It demonstrates practical database design, primary and foreign key relationships and SQL concepts using sample

A MySQL-based database management project designed to manage grocery products, inventory, suppliers, customers, employees, billing transactions, and sales analysis.

📌 Project Overview : 
-----------------------

The Grocery Store Billing Management System is a relational database project developed using MySQL 8.0.16+ and MySQL Workbench. It organizes grocery store operations by maintaining product information, tracking inventory, recording bills, and analyzing sales and payment records.

The project demonstrates practical SQL concepts, including table relationships, constraints, joins, aggregate functions, indexes, views, stored procedures, triggers, and audit logging.

🎯 Project Aim : 
-------------------

To develop a structured database system that simplifies grocery store billing and inventory management while supporting sales reporting, stock monitoring, and payment analysis.

✨ Objectives : 
-----------------
Manage grocery products, categories, suppliers, customers, and employees.
Maintain billing records and individual bill items.
Track stock quantities, reorder levels, and product expiry dates.
Analyze sales by product, category, customer, and payment method.
Identify low-stock, expired, and soon-to-expire products.
Summarize paid, pending, and overdue bills.
Demonstrate database automation using stored procedures and triggers.
Maintain product price audit records.

🛠️ Technologies Used : 
------------------------
Database: MySQL 8.0.16+
Database Tool: MySQL Workbench
Language: SQL
Documentation: Markdown

🗄️ Database Information
-----------------------------
Property	Description
Database Name	grocery_billing
Core Tables	7
Additional Tables	price_audit
Database Type	Relational Database
SQL Version	MySQL 8.0.16+

📋 Database Tables : 
------------------------

The database contains seven core tables and one additional audit table.

Table	        Description
-------        ----------------
Categories	Stores product categories and descriptions.
Suppliers	Stores supplier names, contact information, and cities.
Products	Stores product prices, stock quantities, expiry dates, and related category and supplier IDs.
Customers	Stores customer contact details, cities, and loyalty points.
Employees	Stores employee information, roles, hire dates, and salaries.
Bills           Stores billing dates, payment details, discounts, taxes, and total amounts.
Bill_Items	Stores products, quantities, unit prices, and line totals for each bill.
price_audit	Records product price-related audit events.

🔗 Entity Relationships : 
----------------------------

The database uses primary keys (PKs) and foreign keys (FKs) to maintain relationships between tables.

Categories → Products: One-to-many (1:N)
Suppliers → Products: One-to-many (1:N)
Customers → Bills: One-to-many (1:N); customer ID can be NULL for walk-in sales.
Employees → Bills: One-to-many (1:N)
Bills → Bill_Items: One-to-many (1:N)
Products → Bill_Items: One-to-many (1:N)

All declared relationships between the core tables are one-to-many. The schema does not define any one-to-one relationship.


## Project overview

The database is named `grocery_billing`. The supplied SQL script creates
the schema, inserts sample records, adds indexes and reporting views,
defines stored procedures and triggers, and includes a query bank for
common billing and inventory reports.

## Main entities : 
------------------------------------------------------------------------------------

     Table                   Purpose                 Primary key
  
1) `Categories`            Product category names  `category_id`
                          and descriptions        

2) `Suppliers`             Supplier contact and    `supplier_id`
                          location details        

3) `Products`              Product prices, stock,  `product_id`
                          expiry, and             
                          category/supplier links 

4) `Customers`             Customer contact        `customer_id`
                          details and loyalty     
                          points                  

5) `Employees`             Cashiers, managers, and `employee_id`
                          other store employees   

6) `Bills`                 Billing, payment,       `bill_id`
                          discounts, tax, and     
                           totals                  

7) `Bill_Items`            Products and quantities `item_id`
                          recorded on each bill   

8) `price_audit`           Product price audit     `audit_id`
                          events created by       
                          triggers                


## Relationships and cardinality : 
------------------------------------------

-   One `Categories` record can classify many `Products`; each product
    references one category (**1:N**).
-   One `Suppliers` record can supply many `Products`; each product
    references one supplier (**1:N**).
-   One `Customers` record can be linked to many `Bills`; a bill may
    have no customer for a walk-in sale (**1:N, optional on the bill
    side**).
-   One `Employees` record can be associated with many `Bills`; each
    bill references one employee (**1:N**).
-   One `Bills` record can contain many `Bill_Items`; each bill item
    belongs to one bill (**1:N**).
-   One `Products` record can appear in many `Bill_Items`; each bill
    item references one product (**1:N**).
-   The schema does not declare any **1:1** relationship. The supplied
    relationships are 1:N. `price_audit.product_id` is not declared as a
    foreign key in the provided SQL.

## Features in the supplied SQL : 
------------------------------------------------------------------------

-   **Constraints:** primary keys, foreign keys, unique values, `CHECK`
    constraints, defaults, and enumerated payment fields.
-   **Indexes:** product category/supplier/expiry, bill
    customer/date/date/payment status, and bill-item bill/product
    indexes.
-   **Views:** `view_bill_overview`, `view_sales_details`,
    `view_product_stock_status`, and `view_category_sales_summary`.
-   **Stored procedures:** `sp_bills_by_customer`,
    `sp_product_sales_summary`, and `sp_add_bill_item`.
-   **Triggers:** bill-item quantity/stock validation, stock reduction
    after a sale, and product price audit events.
-   **Query bank:** customer and bill lookups, payment summaries,
    category/product sales, stock and expiry checks, customer-city
    sales, and overall KPIs.


📊 Main SQL Analysis : 

The project includes SQL queries for the following analyses:

Identify products whose stock is below the reorder level.
Summarize bills by payment method and payment status.
Find best-selling products based on units sold.
Calculate sales and revenue by product category.
Retrieve bill details along with customer and employee information.
Identify expired and soon-to-expire products.
Compare product cost prices and selling prices to explore potential profit margins.
Analyze pending and overdue bills.
Calculate sales totals and average billing amounts.
Review inventory levels and product performance.

⚙️ Database Objects Views : 
----------------------------------------
View	Purpose

view_bill_overview	Summarizes bill, customer or walk-in, cashier, payment, and total details.

view_sales_details	Combines bill items with product and category information.

view_product_stock_status	Displays product stock and expiry status.

view_category_sales_summary	Summarizes units sold and revenue by category.

Stored Procedures : 
--------------------------

Procedure                        Purpose
----------                     --------------

'sp_bills_by_customer'          Retrieves bills for a specified customer.

'sp_product_sales_summary'    	Summarizes sales and current stock for a specified product.

'sp_add_bill_item'	            Adds a product to a bill and recalculates bill totals using the documented 5% tax calculation.


Triggers : 
----------------

The project includes triggers to:

Validate bill-item quantities and available stock.
Reduce product stock after a bill item is inserted.
Record product price-related audit events when products are inserted, updated, or deleted.

🚀 How to Run the Project Prerequisites : 
------------------------------------------------------

Install the following software:

MySQL Server 8.0.16 or later
MySQL Workbench (or a compatible MySQL client)
Step 1: Clone the Repository
bash
git clone <your-repository-url> cd <your-repository-folder>

## Setup : 
==========================================================================

1.  Open MySQL Workbench or connect using the MySQL command-line client.
2.  Run the supplied SQL script (`Pasted text.txt`) in a
    development/test database.
3.  The script creates and selects `grocery_billing`, then creates
    tables and database objects and inserts sample data.

Example command after saving/renaming the SQL file to
`grocery_billing.sql`:

``` bash
mysql -u your_username -p < grocery_billing.sql
```
Replace the placeholders with your actual GitHub repository URL and folder name.
Replace `your_username` with your local MySQL account. Review the script
before running it in any shared or production database.

## Example queries

``` sql queries

-- Products with low stock
SELECT product_id, product_name, stock_quantity, reorder_level
FROM Products
WHERE stock_quantity < reorder_level;

-- Bills by payment method
SELECT payment_method, COUNT(*) AS total_bills,
       SUM(total_amount) AS total_amount
FROM Bills
GROUP BY payment_method
ORDER BY total_bills DESC;

-- Best-selling products
SELECT p.product_name, SUM(bi.quantity) AS units_sold
FROM Products p
JOIN Bill_Items bi ON bi.product_id = p.product_id
GROUP BY p.product_id, p.product_name
ORDER BY units_sold DESC
LIMIT 5;
```
 
Step 2: Open the SQL Script

Open MySQL Workbench and connect to your MySQL server.

Open the project SQL file, for example:

text
grocery_billing.sql

Step 3: Execute the SQL Script

Execute the script in order on a fresh development or test database. The script should create the database, tables, constraints, indexes, database objects, and sample records.

Step 4: Verify the Database

Run the following commands:

sql
USE grocery_billing;

SHOW TABLES;


To inspect the product table:

sql
SELECT * FROM Products;


To inspect billing records:

sql
SELECT * FROM Bills;


To inspect individual bill items:

sql
SELECT * FROM Bill_Items;

Step 5: Run the Analysis Queries

Execute the provided SQL analysis queries to review sales performance, inventory levels, payment statuses, and product expiry information.

Alternative: Run from the Terminal
If the SQL script is saved as grocery_billing.sql, execute:

bash
mysql -u your_username -p < grocery_billing.sql
Replace your_username with your local MySQL username. Enter your password when prompted.

💡 SQL Concepts Demonstrated : 
---------------------------------------

CREATE DATABASE and CREATE TABLE
Primary keys and foreign keys
UNIQUE and CHECK constraints
SELECT, WHERE, ORDER BY, and LIMIT
JOIN and LEFT JOIN
GROUP BY and HAVING
Aggregate functions such as COUNT(), SUM(), and AVG()
Indexes for query optimization
Views for reusable reporting
Stored procedures for reusable database operations
Triggers for stock validation, stock updates, and audit logging
Relational database design and referential integrity

⚠️ Limitations : 
-------------------

Sample records are illustrative and may not represent actual grocery store transactions.
Query results depend on the records available in the database.
The project focuses on database implementation rather than a complete graphical billing application.
The stock-reduction trigger executes when a bill item is inserted. Re-running sample inserts may cause duplicate-key errors or reduce stock again.
The stored procedure sp_add_bill_item uses the documented 5% tax calculation, which should be reviewed before real-world use.
The price_audit.product_id column is not defined as a foreign key in the supplied schema.
The database is intended as an educational project and requires additional testing and security review before production deployment.

🔮 Future Enhancements : 
---------------------------

Develop a web or desktop billing application connected to the database.
Add a user interface for checkout, inventory updates, and bill printing.
Implement stronger transaction handling for billing and inventory updates.
Introduce role-based access controls for cashiers and managers.
Build dashboards for sales, stock levels, expiry alerts, and payment summaries.
Add monthly revenue reports, supplier performance analysis, and product profitability reports.
Implement automated database backup and recovery.
Add database testing and validation procedures.

## Important notes : 
----------------------

-   The SQL file includes sample records and query output for
    demonstration.
-   The supplied trigger reduces `Products.stock_quantity` when a
    `Bill_Items` row is inserted. Re-running the sample inserts against
    an already populated database may cause duplicate-key errors or
    alter stock again; use a clean test database when rerunning.
-   `sp_add_bill_item` recalculates totals using a 5% tax calculation,
    as described in the SQL comments.
-   Review sample billing totals and query text before using this script
    as a production system. The README describes the provided
    implementation rather than claiming additional application
    functionality.

## Deliverables : 
--------------------

-   `README.md` --- project setup and database documentation.
-   `Grocery_Store_Billing_ER_Diagram.png` --- conceptual ER diagram
    with entity rectangles, relationship diamonds, and attribute ovals.
    PK/FK labels are shown inside attribute ovals.
-   `grocery_store_billing_management.txt` ----> excutable sql queries for the database    
-   `grocery_store_billing_management` --- presentation-ready
    project overview and ER diagram.


🎓 Project Purpose : 
-------------------------

This project is suitable for learning and demonstrating relational database design, SQL querying, inventory management, billing workflows, and database automation. It can be used as an academic DBMS mini-project or as a foundation for a more complete grocery store management application.


✨Conclusion : 
----------------
The Grocery Store Billing Management System successfully demonstrates the use of MySQL to manage grocery store operations, including product management, inventory tracking, customer records, supplier information, employee details, and billing transactions. The project uses relational database concepts such as primary keys, foreign keys, constraints, joins, indexes, views, stored procedures, and triggers to maintain data consistency and automate essential operations. It also enables sales analysis, payment status monitoring, low-stock identification, and product expiry tracking through SQL queries. Overall, this project provides a practical understanding of database design and SQL implementation for grocery store management while serving as a foundation for future enhancements, such as a graphical user interface, advanced reporting, improved transaction handling, and role-based access control.

👨‍💻 vinaysambana : https://github.com/vinaysambana
