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


### Finding Out Which Product Contribute most carobon footprint in Gamesa Corporacion

```sql
SELECT product_name,carbon_footprint_pcf
FROM  product_emissions
WHERE company LIKE 'Gamesa Corporación Tecnológica%'
```

### Output:

| product_name                  | carbon_footprint_pcf |
|------------------------------|-----------------------|
| Wind Turbine G90 2 Megawats  | 1251625.0             |
| Wind Turbine G114 2 Megawats | 1532608.0             |
| Wind Turbine G128 5 Megawats | 3718044.0             |
| Wind Turbine G132 5 Megawats | 3276187.0             |


### Which country has the highest average carbon footprint (PCF) per product?

```sql
SELECT country, Round(AVG(carbon_footprint_pcf),2) as average_carbon_footprint
FROM product_emissions
GROUP BY country
ORDER BY average_carbon_footprint DESC
LIMIT 5
```

### Output:

| country      | average_carbon_footprint |
|--------------|---------------------------|
| Spain        | 752778.94                 |
| Luxembourg   | 83503.65                  |
| Germany      | 33600.37                  |
| Brazil       | 9858.10                   |
| South Korea  | 6408.82                   |


### What is the trend in carbon footprints (PCFs) over the years?

```sql
SELECT product_emissions.year ,ROUND(AVG(carbon_footprint_pcf),2) as Avergae_Total_Emission,
       ROUND(SUM(carbon_footprint_pcf),2) as Total_Emission
FROM product_emissions
GROUP BY product_emissions.year 
ORDER BY year ASC
```

### Output:

| year | avergae_total_emission | total_emission |
|------|-------------------------|----------------|
| 2013 | 2771.39                 | 496078.13      |
| 2014 | 2885.43                 | 548232.60      |
| 2015 | 49817.55                | 10810407.60    |
| 2016 | 7397.97                 | 1612756.55     |
| 2017 | 3685.95                 | 228528.83      |


### Which company has the highest total carbon footprint (PCF) across all _products?

```sql
SELECT company , ROUND(AVG(carbon_footprint_pcf),2) as Avergae_Total_Emission,
       count(*) AS product_count
FROM product_emissions
GROUP BY company
ORDER BY Avergae_Total_Emission DESC
```

### Output:

| company                            | avergae_total_emission | product_count |
|------------------------------------|-------------------------|----------------|
| Gamesa Corporación Tecnológica, S.A. | 2444616.00             | 4              |
| Hino Motors, Ltd.                  | 191687.00               | 1              |
| Arcelor Mittal                     | 83503.65                | 2              |
| Weg S/A                            | 53551.49                | 3              |
| Daimler AG                         | 43089.19                | 37             |
| ...                                | ...                     | ...            |
| Times Microwave Systems           | 0.03                    | 3              |
| TETRA PAK                          | 0.02                    | 16             |
| Martin Bauer GmbH                 | 0.02                    | 2              |
| Retal                              | 0.01                    | 1              |
| Fabrica de Tapas Bavaria           | 0.00                    | 2              |


### Are there any correlations between the weight of a product and its carbon footprint (PCF)?

```sql
SELECT
   CORR (weight_kg, carbon_footprint_pcf) AS correlation_coefficient
FROM
  product_emissions;
```

### Output:

| correlation_coefficient |
|--------------------------|
| 0.97316                  |

Since correlation is close to 1, it indicates a strong positive correlation between weight and carbon footprint, suggesting that heavier products tend to have higher emissions.

### What is the average carbon footprint (PCF) for each product?

```sql
SELECT  product_name, AVG(carbon_footprint_pcf) as Average_Emission
FROM product_emissions
GROUP BY product_name
ORDER BY  Average_Emission DESC
LIMIT 5
```

### Output:

| product_name                        | average_emission |
|------------------------------------|------------------|
| Wind Turbine G128 5 Megawats       | 3718044.0        |
| Wind Turbine G132 5 Megawats       | 3276187.0        |
| Wind Turbine G114 2 Megawats       | 1532608.0        |
| Wind Turbine G90 2 Megawats        | 1251625.0        |
| Land Cruiser Prado. FJ Cruiser...  | 191687.0         |


### Which industry group has shown the most significant reduction in carbon footprints (PCFs) over the years?

```sql
SELECT year ,industry_group, ROUND(SUM(carbon_footprint_pcf),2) as Total_Emission
FROM product_emissions
GROUP BY year ,industry_group
ORDER BY industry_group ,year ASC ,Total_Emission ASC
```

### Output:

| year | industry_group                                 | total_emission |
|------|------------------------------------------------|----------------|
| 2013 | Automobiles & Components                       | 130189.00      |
| 2014 | Automobiles & Components                       | 230014.42      |
| 2015 | Automobiles & Components                       | 817227.00      |
| 2016 | Automobiles & Components                       | 1404833.00     |
| 2013 | Capital Goods                                  | 60116.69       |
| ...  | ...                                            | ...            |
| 2015 | Tires                                          | 2021.68        |
| 2015 | Tobacco                                        | 0.70           |
| 2015 | Trading Companies & Distributors and Commercia... | 238.47      |
| 2013 | Utilities                                      | 60.58          |
| 2016 | Utilities                                      | 60.64          |


### Is there a relationship between the country of origin and the carbon footprint (PCF) of products?

```sql
SELECT country ,ROUND(AVG(carbon_footprint_pcf),2) as Total_Emission
FROM product_emissions
GROUP BY country
ORDER BY Total_Emission DESC
```

### Output:

| country         | total_emission |
|----------------|----------------|
| Spain          | 752778.94      |
| Luxembourg     | 83503.65       |
| Germany        | 33600.37       |
| Brazil         | 9858.10        |
| South Korea    | 6408.82        |
| ...            | ...            |
| China          | 23.76          |
| Switzerland    | 5.02           |
| Belgium        | 1.18           |
| Italy          | 0.84           |
| Greece         | 0.70           |
| Lithuania      | 0.01           |
| Colombia       | 0.00           |


### What is the contribution of each industry group to the total global emissions?

```sql
SELECT industry_group, Round(AVG(carbon_footprint_pcf),2) as average_carbon_footprint
FROM product_emissions 
GROUP BY industry_group
ORDER BY average_carbon_footprint DESC
LIMIT 10
```

### Output:

| industry_group                                  | average_carbon_footprint |
|-------------------------------------------------|---------------------------|
| Electrical Equipment and Machinery              | 891050.69                |
| Automobiles & Components                        | 35373.47                 |
| Pharmaceuticals, Biotechnology & Life Sciences  | 24162.00                 |
| Capital Goods                                   | 7837.35                  |
| Mining – Iron, Aluminum, Other Metals           | 2727.00                  |
| Materials                                       | 2672.04                  |
| Energy                                          | 2154.81                  |
| Software & Services                             | 1723.50                  |
| Chemicals                                       | 1549.64                  |
| Media                                           | 1534.45                  |





