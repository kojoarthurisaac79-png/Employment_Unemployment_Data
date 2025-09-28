Employment, Unemployment & GDP Data Analysis

This project explores a dataset containing employment, unemployment, and GDP statistics for multiple countries over several years. The goal is to practice and demonstrate SQL concepts such as window functions, CTEs, triggers, and analytical queries.

 Dataset Overview

The dataset contains approximately 5752 rows with the following columns:
	•	country_name – Name of the country
	•	year_y – Year of the record
	•	employment_agriculture – Employment share in agriculture sector (%)
	•	employment_industry – Employment share in industry sector (%)
	•	employment_services – Employment share in services sector (%)
	•	unemployment_rate – Unemployment rate (%)
	•	gdp_usd – Gross Domestic Product (in USD)

 SQL Concepts Practiced
	•	Data Cleaning & Transformation
	•	Renaming columns for consistency
	•	Handling NULL values
	•	Changing data types
	•	Analytical Queries
	•	Year-to-year GDP growth using LAG
	•	3-year rolling average GDP using AVG OVER
	•	Highest GDP country per year using ROW_NUMBER
	•	Employment sector comparisons
	•	CTEs (Common Table Expressions)
	•	Simplifying complex queries
	•	Isolating subsets of data for analysis
	•	Triggers
	•	Setting default values (unemployment_rate = 0 if NULL)
	•	Enforcing rules (gdp_usd < 0 → set to NULL)

  SELECT year_y, country_name, GDP_in_USD
FROM (
  SELECT year_y, country_name, GDP_in_USD,
         ROW_NUMBER() OVER (PARTITION BY year_y ORDER BY GDP_in_USD DESC) AS rn
  FROM EUD
) t
WHERE rn = 1;

DELIMITER //
CREATE TRIGGER trg_gdp_nonnegative
BEFORE INSERT ON EUD
FOR EACH ROW
BEGIN
  IF NEW.GDP_in_USD < 0 THEN
    SET NEW.GDP_in_USD = NULL;
  END IF;
END //
DELIMITER ;

 Future Improvements
	•	Add data visualization with Python (Matplotlib/Seaborn).
	•	Automate reporting with stored procedures.
	•	Integrate Airflow for scheduled analysis.

 License

This project is open-source and available under the MIT License.
