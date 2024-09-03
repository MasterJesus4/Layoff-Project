# Layoff-Project
Exploratory Data Analysis In SQL

## Project Overview
Layoff Trends and Insight.
Dataset: Layoff Data ( Company, Location, Industry, Total laid off, Percentage laid off, Date, Stage and Country).
The dataset contains information on layoffs across various companies, industries and countries. The data provides insights into the extent of layoffs and stages of layoffs. The analysis aims to identify the trends, patterns and correlation within data.

## Data Source
The data source is a collection of data from various sources including :
- Government databasee
- Industry association,etc

  ## Objectives
  To identify the trends, patterns and correlartion within layoff data and to provide insights on the factors contributing layoffs, in order to inform business strategies polcy decisions and support affected individuals.

  ## Tools
  SQL

  ## Ouery
1. Companies with the most total laid off

   Select company, sum(total_laid_off) AS total_laid_off

 From [Portfolio Project].dbo.layoff_standing
	
 GROUP BY company
	
 ORDER BY Sum(total_laid_off) DESC
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 2. Industries with the most total laid off
	
 Select industry, sum(total_laid_off) AS total_laid_off
	
 From [Portfolio Project].dbo.layoff_standing
	
 GROUP BY industry
	
 ORDER BY  sum(total_laid_off) DESC
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 3. Countries with total laid off
	
 Select country, sum(total_laid_off) AS total_laid_off

 From [Portfolio Project].dbo.layoff_standing

 GROUP BY country
	
 ORDER BY  sum(total_laid_off) DESC
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. Location with the most total laid off
	
 Select location, sum(total_laid_off) AS total_laid_off
	
 From [Portfolio Project].dbo.layoff_standing
	
 GROUP BY location
	
 ORDER BY  sum(total_laid_off) DESC

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

5. Total laid off by year
	
 Select YEAR(date), sum(total_laid_off) AS total_laid_off
	
 From [Portfolio Project].dbo.layoff_standing

 GROUP BY  YEAR(date)
	
 ORDER BY  1 DESC

 ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 6. Total laid off by stage

 Select stage, sum(total_laid_off) AS total_laid_off
	
 From [Portfolio Project].dbo.layoff_standing
	
 GROUP BY stage
	
 ORDER BY  1 DESC

 ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 7.  Company with total laid off , the year and the numbers
	
	Select company, YEAR(date) AS Year, SUM(total_laid_off) AS total_laid_off

 From [Portfolio Project].dbo.layoff_standing
	
 GROUP BY company, YEAR(date)
	
 ORDER BY 3 DESC;

 ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 8.  Earlier we looked at Companies with the most Layoffs. Now let's look at that per year.


 WITH Company_Year(company,years,total_laid_off) AS
(

Select company, YEAR(date) AS Year, SUM(total_laid_off) AS total_laid_off

From [Portfolio Project].dbo.layoff_standing

GROUP BY company, YEAR(date)

)

Select *, DENSE_RANK() OVER (PARTITION BY years ORDER BY total_laid_off DESC) AS Ranking

From  Company_Year

WHERE years IS NOT NULL

ORDER BY Ranking ASC



-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

9.  Companies with most laid off top 5

WITH Company_Year(company,years,total_laid_off) AS

(

Select company, YEAR(date) AS Year, SUM(total_laid_off) AS total_laid_off

From [Portfolio Project].dbo.layoff_standing

GROUP BY company, YEAR(date)

), Company_Year_Rank AS

(Select *, DENSE_RANK() OVER (PARTITION BY years ORDER BY total_laid_off DESC) AS Ranking

From  Company_Year

WHERE years IS NOT NULL

)

SELECT *

From  Company_Year_Rank

WHERE Ranking <=5












  
