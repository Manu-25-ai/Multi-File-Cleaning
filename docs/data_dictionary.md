=> Data Dictionary — E-Commerce Consolidated Dataset

This document describes the structure and meaning of all fields included in the final cleaned and consolidated dataset:
data_clean/master_dataset.csv

-> The dataset combines four original sources:
- customers.csv
- products.csv
- orders.csv
- payments.csv

-> Column Definitions

Column Name	   Data Type	  Source Table	  Description
order_id	     string	      orders	        Unique identifier for each order.
customer_id	   string	      customers	      Unique identifier linking customer to an order.
customer_name	 string     	customers	      Full name or business name of the customer.
email	         string	      customers	      Customer email address. Placeholder added if missing.
city	         string	      customers	      City-level location of the customer.
segment	       category	    customers	      Customer type (e.g., B2B / B2C). Missing values inferred logically.
product_id	   string	      products	      Unique product identifier.
product_name	 string	      products	      Name of the product ordered.
category	     category	    products	      Product category (Electronics, Furniture, etc.).
unit_price	   float	      products	      Cleaned and standardized unit price of the product. Missing values filled using median logic.
quantity	     integer	    orders	        Number of units ordered. Invalid values removed.
order_date	   datetime	    orders	        Standardized purchase date in YYYY-MM-DD format.
payment_method category	    payments	      Mode of payment (UPI, Credit Card, Cash, etc.).
payment_status category	    payments	      Final payment state. Only successful payments included in core analysis.
amount	       float	      payments	      Actual paid amount recorded in payment logs. Missing or mismatched values flagged.

-> Engineered Fields
These fields did not exist in the raw datasets — added during cleaning for business analysis.

Column Name        	Type	     Meaning
expected_amount	    float	     quantity × unit_price — ideal cost of the transaction before checking payment logs.
payment_difference	float	     expected_amount - amount; helps identify under- or over-paid transactions.
payment_issue	      boolean	   True if expected and paid amounts do not match.
order_month	        integer	   Extracted month (1–12) from order_date. Useful for seasonality patterns.
order_year	        integer	   Extracted year from order_date. Useful for trend analysis.

-> Data Quality Flags
These fields help track inconsistencies or incomplete information.

Column	           Meaning
missing_customer	 Indicates whether customer details were missing in original data.
missing_product    Indicates missing product metadata.
missing_payment	   Indicates missing payment information for a placed order.

-> Notes & Assumptions
- Missing emails were replaced with a default placeholder: unknown@example.com.
- Customer segment was inferred as B2B if business keywords like “Ltd”, “Enterprise”, “Corp” existed in customer name.
- Only successful payments were included in revenue logic — failed or pending payments retained only for audit flags.
- Pricing inconsistencies (e.g., commas, currency formatting, missing values) were resolved using median values per product category.

-> How to Use
- Clone or download the project.
- Install required packages: pip install -r requirements.txt.
- Open the notebook: notebook/ecommerce_data_cleaning.ipynb.
- Run all cells from top to bottom.
- Final cleaned files will be generated automatically in data_clean/.
- Use the file master_dataset.csv for reporting, dashboards, or analysis.
