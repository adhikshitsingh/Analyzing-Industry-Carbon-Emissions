# Analyzing Industry Carbon Emissions Solution

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

## Finding Company Which Contributing Height Amount of Carbon Emission

```sql
SELECT company, Round(SUM(carbon_footprint_pcf),2) as total_carbon_footprint,
       count(*) as product_Count,Round(AVG(carbon_footprint_pcf),2) as average_carbon_footprint
FROM product_emissions 
GROUP BY company
ORDER BY average_carbon_footprint DESC
LIMIT 10
```
