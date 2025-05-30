# Analyzing Industry Carbon Emissions Solution

---
This report contains the solution of the SQL Project 'Analyzing Industry Carbon Emissions' available on DataCamp. [Click here](https://projects.datacamp.com/projects/1593) to access the complete project.

# Introduction
When factoring heat generation required for the manufacturing and transportation of products, Greenhouse gas emissions attributable to products, from food to sneakers to appliances, make up more than 75% of global emissions.

Our data, which is publicly available on [nature.com](https://www.nature.com/articles/s41597-022-01178-9), contains product carbon footprints (PCFs) for various companies. PCFs are the greenhouse gas emissions attributable to a given product, measured in CO2 (carbon dioxide equivalent).

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
