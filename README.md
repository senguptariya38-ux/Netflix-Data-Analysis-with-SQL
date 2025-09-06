# Netflix-Data-Analysis-with-SQL

![netflix.logo](https://github.com/senguptariya38-ux/Netflix-Data-Analysis-with-SQL/blob/main/netflix.logo.jpg)

## Overview

This project showcases my end-to-end data analysis workflow using PostgreSQL on a Netflix dataset. This project serves as a practical example of how SQL can be used to drive business intelligence and solve real-world problems.

## Objective 

* To use SQL to perform a comprehensive data analysis of a simulated Netflix dataset. 
* Demonstrate my ability to translate real-world business questions into technical queries.
* Extract meaningful insights from raw data, and present findings that can inform strategic decisions. 
* To solve 10 key business problems for a streaming service like Netflix using SQL.

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

### 1. Count the content titles added from 2020 onwards.

```sql
SELECT COUNT(*) AS number_of_contents

FROM netflix

WHERE release_year >= '2020';
```
### **- Content Growth Post-2020: A total of 1,545 titles were added from 2020 onwards, indicating Netflix’s aggressive expansion during and after the pandemic era**

### 2. Find All Movies/TV Shows by Director 'Christopher Nolan'

```sql
SELECT title, director
FROM netflix
WHERE director = 'Christopher Nolan'
```
### **- Director-Specific Insights: The platform features multiple works by Christopher Nolan, showcasing its commitment to hosting high-profile creators and attracting cinephiles**

### 3. Find each year the numbers of content release in India on netflix.

```sql
SELECT country, release_year, count(*) AS total_release

FROM
netflix

WHERE country = 'India'
GROUP BY country, release_year
```
### **- Regional Focus – India: Year-wise analysis of content released in India revealed consistent growth, reflecting Netflix’s investment in regional markets and its localization strategy.**

### 4. Idenyify the longest and shortest movies.

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
### **- Duration Extremes: The longest movie, Black Mirror: Bandersnatch (312 minutes), and the shortest, Silent (3 minutes), highlight the platform’s diverse content lengths catering to varied viewer preferences.**

### 5. Count the Number of Content Items in Each Genre

```sql
SELECT 
    UNNEST(STRING_TO_ARRAY(listed_in, ',')) AS genre,
    COUNT(*) AS total_content
FROM netflix
GROUP BY genre;
```
### **- Genre Distribution: By unnesting genre data, we quantified content across categories, helping identify dominant genres and potential gaps in the catalog.**

### 6. Count the number of TV shows vs movies.

```sql
SELECT type, COUNT(*) AS number_of_contents

   FROM netflix

GROUP BY type
   ```
### **- Content Type Breakdown: The count of TV Shows vs Movies provided clarity on format preferences, useful for production planning and subscriber targeting.**

### 7. Find the Top 5 Countries with the Most Content on Netflix.

```sql
SELECT UNNEST(STRING_TO_ARRAY(country, ',')) AS country, 
COUNT(*) AS number_of_contents

FROM netflix

WHERE country IS NOT NULL
GROUP BY country
```
### **- Global Reach: The top 5 countries with the most content revealed Netflix’s strongest content-producing regions, aiding in future licensing and partnership decisions.**

### 8. List All Movies that are Thrillers.

```sql
SELECT UNNEST(STRING_TO_ARRAY(listed_in, ',')) AS genre, 
type, title

FROM netflix

WHERE listed_in LIKE 'Thrillers' AND type = 'Movie';
```
### **- Thriller Inventory: Listing all thriller movies helped isolate genre-specific offerings, valuable for thematic promotions or curated watchlists.**

### 9. Find the Top 10 Actors Who Have Appeared in the Highest Number of Movies Produced in India

```sql
SELECT UNNEST(STRING_TO_ARRAY(casts, ',')) AS actors, country, 
count(*) AS number_of_movies

   FROM netflix
   WHERE casts IS NOT NULL AND country = 'India' 
   AND type = 'Movie'
   
GROUP BY actors, country
ORDER BY number_of_movies DESC
LIMIT 10;
```
### **- Star Power in India: The top 10 actors in Indian movies gave insight into casting trends and popular faces, useful for marketing and future collaborations.**

### 10. Categorize Content Based on the Presence of 'Kill' and 'Violence' Keywords.

```sql
SELECT title, 
CASE 

	WHEN description ILIKE '%kill%' AND  description ILIKE '%violence%' 
	THEN 'Contains Kill and Violence' 
	WHEN description ILIKE '%kill%' THEN 'Contains Kill'
	WHEN description ILIKE 'Violence' THEN 'Contains Violence'
	ELSE 'No Kill or Violence'
	
END AS content_categorization
FROM netflix
GROUP BY title, content_categorization;
```
### **- Content Sensitivity Analysis: Categorizing titles based on keywords like kill and violence enabled a basic sentiment filter, which can be extended for parental controls or content warnings.**

## Conclusion

This project demonstrates how SQL can be leveraged not just for data retrieval, but for strategic storytelling. From identifying regional trends to understanding genre saturation and actor popularity, the insights extracted can guide Netflix’s content strategy, marketing campaigns, and user experience enhancements.
