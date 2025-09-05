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

git add Schema.sql

## Business problems and solutions

1. Find the number of contents added from the year 2020.

   SELECT COUNT(*) AS number_of_contents

FROM netflix

WHERE release_year >= '2020';

2. 
