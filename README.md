# Netflix-Data-Analysis-with-SQL

![netflix.logo](https://github.com/senguptariya38-ux/Netflix-Data-Analysis-with-SQL/blob/main/netflix.logo.jpg)

## Overview

This project showcases my end-to-end data analysis workflow using PostgreSQL on a Netflix dataset. This project serves as a practical example of how SQL can be used to drive business intelligence and solve real-world problems.

## Objective 

* To use SQL to perform a comprehensive data analysis of a simulated Netflix dataset. 
* Demonstrate my ability to translate real-world business questions into technical queries.
* Extract meaningful insights from raw data, and present findings that can inform strategic decisions. 
* To solve 15 key business problems for a streaming service like Netflix using SQL.

## Dataset

[Netflix.Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)

## Schema

```sql
DROP TABLE IF EXISTS netflix;
CREATE TABLE netflix
(
	show_id	VARCHAR(5),
	type    VARCHAR(10),
	title	VARCHAR(250),
	director VARCHAR(550),
	casts	VARCHAR(1050),
	country	VARCHAR(550),
	date_added	VARCHAR(55),
	release_year	INT,
	rating	VARCHAR(15),
	duration	VARCHAR(15),
	listed_in	VARCHAR(250),
	description VARCHAR(550)
);
```

## Business problems and solutions (Data available till 2021)

1. Count the content titles added from 2020 onwards.

```sql
SELECT COUNT(*) AS number_of_contents

FROM netflix

WHERE release_year >= '2020';
```
Ans: 1545 

2. Find All Movies/TV Shows by Director 'Christopher Nolan'

```sql
SELECT title, director
FROM netflix
WHERE director = 'Christopher Nolan'
```
3. Find each year the numbers of content release in India on netflix.

```sql
SELECT country, release_year, count(*) AS total_release

FROM
netflix

WHERE country = 'India'
GROUP BY country, release_year
```

4. Idenyify the longest and shortest movies.

```sql
SELECT 
    title, duration
FROM netflix

WHERE type = 'Movie' and duration IS NOT NULL
ORDER BY SPLIT_PART(duration, ' ', 1)::INT DESC

LIMIT 1;

SELECT 
    title, duration
FROM netflix

WHERE type = 'Movie' and duration IS NOT NULL
ORDER BY SPLIT_PART(duration, ' ', 1)::INT ASC

LIMIT 1;
```
Ans: Longest movie- "Black Mirror: Bandersnatch" (312min), shortest movie- "Silent" (3min)

5. Count the Number of Content Items in Each Genre

```sql
SELECT 
    UNNEST(STRING_TO_ARRAY(listed_in, ',')) AS genre,
    COUNT(*) AS total_content
FROM netflix
GROUP BY genre;
```



   
