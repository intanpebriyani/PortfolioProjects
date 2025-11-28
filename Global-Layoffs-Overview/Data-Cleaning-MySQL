-- MySQL Project: Data Cleaning and Exploratory Data Analysis
-- Inspired by Alex The Analyst's MySQL YouTube Series
-- Dataset: https://www.kaggle.com/datasets/swaptr/layoffs-2022
-- Author: Intan Pebriyani
-- Date: October 2025


SELECT *
FROM world_layoffs.layoffs;



-- First thing we need to do is create a staging table. This is the one that we will work in and clean the data. We want a table with the raw data in case something happens. 
CREATE TABLE world_layoffs.layoffs_staging
LIKE world_layoffs.layoffs;

INSERT layoffs_staging
SELECT *
FROM world_layoffs.layoffs;


-- During data cleaning, we typically follow these main steps:
-- 1. Identify and remove duplicate records
-- 2. Standardize data formats and correct inconsistencies
-- 3. Handle null or missing values appropriately
-- 4. Remove unnecessary columns or rows to keep the dataset clean and relevant


-- 1. Remove Duplicates

-- first check the duplicates
SELECT *
FROM world_layoffs.layoffs_staging;
SELECT *,
row_number() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, `date`, stage, country, funds_raised_millions) AS row_num
FROM world_layoffs.layoffs_staging;

WITH duplicate_CTE AS
(
SELECT *,
row_number() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, `date`, stage, country, funds_raised_millions) AS row_num
FROM world_layoffs.layoffs_staging
)
SELECT *
FROM duplicate_CTE
WHERE row_num > 1;

SELECT *
FROM world_layoffs.layoffs_staging
WHERE company = 'Casper' ;


WITH duplicate_CTE AS
(
SELECT *,
row_number() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, `date`,
 stage, country, funds_raised_millions) AS row_num
FROM world_layoffs.layoffs_staging
)
DELETE 
FROM duplicate_CTE
WHERE row_num > 1;


CREATE TABLE `world_layoffs`.`layoffs_staging3` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` INT
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
FROM world_layoffs.layoffs_staging3
WHERE row_num > 1;

INSERT INTO world_layoffs.layoffs_staging3
SELECT *,
row_number() OVER(
partition by company, location,
industry, total_laid_off, percentage_laid_off, `date`, stage,
country, funds_raised_millions) row_num
FROM world_layoffs.layoffs_staging;

DELETE
FROM world_layoffs.layoffs_staging3
WHERE row_num > 1;

SELECT *
FROM world_layoffs.layoffs_staging3
WHERE row_num > 1;

SELECT *
FROM world_layoffs.layoffs_staging3;

-- 2. Standardizing Data

SELECT DISTINCT (company), TRIM(company)
FROM world_layoffs.layoffs_staging3;

UPDATE world_layoffs.layoffs_staging3
SET company = TRIM(company);

SELECT DISTINCT industry
FROM world_layoffs.layoffs_staging3
;

UPDATE world_layoffs.layoffs_staging3
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

SELECT DISTINCT country
FROM world_layoffs.layoffs_staging3
WHERE country LIKE 'United States%'
ORDER BY 1;

SELECT DISTINCT country, TRIM(TRAILING '.' FROM country)
FROM world_layoffs.layoffs_staging3
ORDER BY 1;

UPDATE world_layoffs.layoffs_staging3
SET country = TRIM(TRAILING '.' FROM country)
WHERE country LIKE 'United States';

SELECT `date`
FROM world_layoffs.layoffs_staging3
;

UPDATE world_layoffs.layoffs_staging3
SET `date` = str_to_date(`date`, '%m/%d/%Y');

ALTER TABLE world_layoffs.layoffs_staging3
MODIFY COLUMN `date` DATE;

-- 3. Handling Null and missing Values

-- The null values in total_laid_off, percentage_laid_off, and funds_raised_millions appear to be valid. 
-- I’ll keep them as NULL for now since they represent missing information accurately. 
-- Leaving them as NULL also makes future calculations during the EDA phase easier and more consistent.


-- 4. remove any columns and rows we need to

SELECT *
FROM world_layoffs.layoffs_staging3
WHERE total_laid_off IS NULL
AND percentage_laid_off IS NULL;

UPDATE world_layoffs.layoffs_staging3
SET industry = null
WHERE industry = '';

SELECT *
FROM world_layoffs.layoffs_staging3
WHERE industry IS NULL
OR industry = ''
;

SELECT *
FROM world_layoffs.layoffs_staging3
WHERE company LIKE 'Bally%';

SELECT t1.industry, t2.industry
FROM world_layoffs.layoffs_staging3 t1
JOIN world_layoffs.layoffs_staging3 t2
	ON t1.company = t2.company
WHERE (t1.industry IS NULL OR t1.industry = '')
AND t2.industry IS NOT NULL;

UPDATE world_layoffs.layoffs_staging3 t1
JOIN world_layoffs.layoffs_staging3 t2
	ON t1.company = t2.company
SET t1.industry = t2.industry
WHERE t1.industry IS NULL 
AND t2.industry IS NOT NULL;

SELECT *
FROM world_layoffs.layoffs_staging3
WHERE total_laid_off IS NULL
AND percentage_laid_off IS NULL;

DELETE
FROM world_layoffs.layoffs_staging3
WHERE total_laid_off IS NULL
AND percentage_laid_off IS NULL;

SELECT *
FROM world_layoffs.layoffs_staging3;

ALTER TABLE world_layoffs.layoffs_staging3
DROP COLUMN row_num;

-- Exploratory Data Analysis (EDA)

-- In this step, we’ll explore the dataset to identify trends, patterns, and potential outliers.  
-- Typically, the EDA process begins with a few questions or hypotheses in mind,  
-- but for this project, we'll simply explore the data to uncover any interesting insights or observations.


SELECT *
FROM world_layoffs.layoffs_staging3;

SELECT MAX(total_laid_off)
FROM world_layoffs.layoffs_staging3;

--Looking at Percentage to see how big these layoffs were
SELECT MAX(percentage_laid_off), MIN(percentage_laid_off)
FROM world_layoffs.layoffs_staging3
WHERE percentage_laid_off IS NOT NULL;

-- Which companies had 1 which is basically 100 percent of they company laid off
SELECT *
FROM world_layoffs.layoffs_staging2
WHERE  percentage_laid_off = 1;

-- these are mostly startups it looks like who all went out of business during this time

-- if we order by funds_raised_millions we can see how big some of these companies were
SELECT *
FROM world_layoffs.layoffs_staging3
WHERE percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;

-- Companies with the most Total Layoffs
SELECT company, SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY company
ORDER BY 2 DESC
LIMIT 10;

-- By location
SELECT location, SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY location
ORDER BY 2 DESC
LIMIT 10;


-- This represents the total values recorded within the dataset timeframe (approximately the past 3 years).

SELECT MIN(`date`), MAX(`date`)
FROM world_layoffs.layoffs_staging3;

SELECT country, SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY country
ORDER BY 2 DESC;

SELECT *
FROM world_layoffs.layoffs_staging3;

SELECT YEAR(`date`), SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY YEAR(`date`)
ORDER BY 2 DESC;

SELECT stage, SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY stage
ORDER BY 2 DESC;

SELECT company, SUM(percentage_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY company
ORDER BY 2 DESC;

SELECT SUBSTRING(`date`,1,7) `MONTH`, SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
WHERE SUBSTRING(`date`,1,7) IS NOT NULL
GROUP BY `MONTH`
ORDER BY 1 ASC;

WITH Rolling_Total AS
(
SELECT SUBSTRING(`date`,1,7) `MONTH`, SUM(total_laid_off) total_off
FROM world_layoffs.layoffs_staging3
WHERE SUBSTRING(`date`,1,7) IS NOT NULL
GROUP BY `MONTH`
ORDER BY 1 ASC
)
SELECT `MONTH`, total_off,
SUM(total_off) OVER(ORDER BY`MONTH`) rolling_total
FROM Rolling_Total;



SELECT company, SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY company
ORDER BY 2 DESC;

SELECT company, YEAR( `date`), SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY company, YEAR( `date`)
ORDER BY 3 DESC;

WITH Company_Year (company, years, total_laid_off) AS
(
SELECT company, YEAR( `date`), SUM(total_laid_off)
FROM world_layoffs.layoffs_staging3
GROUP BY company, YEAR( `date`)
), Company_Year_Rank AS
(
SELECT *, 
DENSE_RANK() OVER(PARTITION BY years ORDER BY total_laid_off DESC) ranking
FROM Company_Year
WHERE years IS NOT NULL
)
SELECT *
FROM Company_Year_Rank
WHERE ranking <= 5
;

-- Rolling Total of Layoffs Per Month
SELECT SUBSTRING(date,1,7) as dates, SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY dates
ORDER BY dates ASC;

-- now use it in a CTE so we can query off of it
WITH DATE_CTE AS 
(
SELECT SUBSTRING(date,1,7) as dates, SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY dates
ORDER BY dates ASC
)
SELECT dates, SUM(total_laid_off) OVER (ORDER BY dates ASC) as rolling_total_layoffs
FROM DATE_CTE
ORDER BY dates ASC;

SELECT *
FROM world_layoffs.layoffs_staging3;


