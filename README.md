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

1. Find the number of contents added after the year 2020.

```sql
SELECT COUNT(*) AS number_of_contents

FROM netflix

WHERE release_year >= '2020';
```
Ans: 1545 

2. 
