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

## Query

### Finding Company Which Contributing Height Amount of Carbon Emission

```sql
SELECT company, Round(SUM(carbon_footprint_pcf),2) as total_carbon_footprint,
       count(*) as product_Count,Round(AVG(carbon_footprint_pcf),2) as average_carbon_footprint
FROM product_emissions 
GROUP BY company
ORDER BY average_carbon_footprint DESC
LIMIT 10
```

### Output: 

| company                            | total_carbon_footprint | product_count | average_carbon_footprint |
|------------------------------------|--------------------------|----------------|----------------------------|
| Gamesa Corporación Tecnológica, S.A. | 9778464.00              | 4              | 2444616.00                 |
| Hino Motors, Ltd.                  | 191687.00               | 1              | 191687.00                  |
| Arcelor Mittal                     | 167007.30               | 2              | 83503.65                   |
| Weg S/A                            | 160654.48               | 3              | 53551.49                   |
| Daimler AG                         | 1594300.00              | 37             | 43089.19                   |
| General Motors Company            | 137007.00               | 4              | 34251.75                   |
| Volkswagen AG                      | 655960.00               | 25             | 26238.40                   |
| Waters Corporation                 | 72486.00                | 3              | 24162.00                   |
| Daikin Industries, Ltd.           | 105600.00               | 6              | 17600.00                   |
| CJ Cheiljedang                     | 94816.80                | 6              | 15802.80                   |


