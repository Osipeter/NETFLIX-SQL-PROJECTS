# Netflix Movies and TV Shows End-to-End Data Analysis Project using SQL
 
## Overview

This project requires a thorough examination of Netflix's movie and TV show data using SQL. The purpose is to extract relevant insights and answer a variety of (20+) business questions using the dataset. This paper details the project's objectives, business challenges, solutions, findings, and conclusions.
 
## Objectives
 
- Examine the distribution of content types (movies versus television shows).

- Determine the most frequent ratings for films and television shows.

- Organise and analyse content by release year, country, and duration.

- Analyse and categorise information using precise criteria and keywords.
 
## Dataset
 
Though the dataset for this project is sourced from the Kaggle dataset, but its uploaded here: Netflix_titles.csv
 
### 1. Display the total Number of Movies vs TV Shows
 
```sql

SELECT 

   type,

   COUNT(*) count_type

FROM netflix_titles

GROUP BY type

```
 
**Objective:** Determine the distribution of content types on Netflix.


### 2. Count the Number of Content Items in Each Genre

```sql
  
SELECT 
	Trim(Value) AS genre,

	COUNT(*) AS total_content

FROM netflix_titles

CROSS APPLY string_split (listed_in, ',')

GROUP BY Trim(Value);
  
 ```

**Objective:** Count the number of content items in each genre.


### 3. List All Movies Released in a 2020

```sql
  
SELECT *

FROM netflix_titles

WHERE release_year = 2020;
  
 ```

**Objective:** Retrieve all movies released in a specific year.


### 4. Find the Top 5 Countries with the Most Content on Netflix

```sql
  
SELECT Top(5) * 
FROM
(
	SELECT

	Trim(Value) AS country,
 
	COUNT(*) AS total_content

	FROM netflix_titles

	   CROSS APPLY string_split (country, ',')

	GROUP BY Trim(Value)

) AS temp

WHERE country IS NOT NULL

ORDER BY total_content DESC
  
 ```

**Objective:** Identify the top 5 countries with the highest number of content items.



### 5. Find Content Added in the Last 5 Years

```sql
  
SELECT * FROM Netflix_Titles

WHERE DATEDIFF(YEAR, date_added, GETDATE()) >= 5
  
 ```

**Objective:** Identify the content added in the last 5 years.



### 6. List All Movies that are Documentaries

```sql
  
SELECT * FROM
(
	SELECT show_id, Trim(value) Listed_In

	FROM netflix_titles

	CROSS APPLY string_split(Listed_In,',')

) AS ANSWER

WHERE Listed_In = 'Documentaries'

OR

SELECT * FROM Netflix_Titles

WHERE type = 'movie' And Listed_in LIKE '%Documentaries%'
  
 ```

**Objective:** Identify the content items that are Documentaries.


 
