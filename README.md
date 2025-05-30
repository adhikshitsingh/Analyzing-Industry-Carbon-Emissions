# Analyzing Industry Carbon Emissions

This project explores global carbon emissions using a PostgreSQL database containing Product Carbon Footprints (PCFs) for various products across companies, industries, and countries. The goal is to identify emission-heavy industries and product categories to better understand their environmental impact.

## What I Did:

- Queried the product_emissions table to calculate average carbon footprints per product, industry, and company.
- Analyzed the distribution of emissions across different stages of production: upstream, operations, and downstream.
- Identified top-emitting industries and companies by aggregating and ranking total PCFs.
- Filtered products with the highest carbon footprints per kg to spot environmental outliers.
- Cleaned and processed raw data using SQL techniques such as CAST(), GROUP BY, and ORDER BY.
- Gained insights into how industry group and geography influence product emissions.

## Tools Used:

- PostgreSQL
- SQL (Joins, Aggregations, Filtering, Casting)

## Data

This data is stored in a PostgreSQL database containing one table, product_emissions, which looks at PCFs by product as well as the stage of production that these emissions occurred. Here's a snapshot of what `product_emissions` contains in each column:

| field	                        | data type   |
| ------------------------------| ------------|
| id	                        | VARCHAR     |  
| year	                        | INT         |
| roduct_name                   | VARCHAR     | 
| company	                    | VARCHAR     |
| country	                    | VARCHAR     |
| industry_group                | VARCHAR     |
| weight_kg	                    | NUMERIC     |
| carbon_footprint_pcf          | NUMERIC     |
| upstream_percent_total_pcf    | VARCHAR     |
| operations_percent_total_pcf  | VARCHAR     |
| downstream_percent_total_pcf  | VARCHAR     |

