# Exercises from Leetcode - Top SQL 50


### Exercise # 1

Table: Products

| Column Name | Type |
|-------------|------|
| product_id  | int  |
| low_fats    | enum |
| recyclable  | enum |


product_id is the primary key (column with unique values) for this table.
low_fats is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM (category) of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.
 
#### Question 
Write a solution to find the ids of products that are both low fat and recyclable.
Return the result table in any order.
The result format is in the following example.

Example 1:

**Input:** 
Products table:

| product_id | low_fats | recyclable |
|------------|----------|------------|
| 0          | Y        | N          |
| 1          | Y        | Y          |
| 2          | N        | Y          |
| 3          | Y        | Y          |
| 4          | N        | N          |


**Output:** 

| product_id |
|------------|
| 1          |
| 3          |


### Solution  # 1

```SQL
SELECT product_id 
FROM Products 
WHERE
low_fats ='Y' 
AND
recyclable ='Y'
```


**Explanation:** 
Only products 1 and 3 are both low fat and recyclable.




### Exercise # 2

Table: Customer

| column     | Data type |
|------------|-----------|
| id         | int       |
| name       | string    |
| referee_id | int       |


In table, id is the primary key column for this table.
Each document of this collection indicates the id of a customer,
their name, and the id of the customer who referred them.
 

#### Question 
Find the names of the customer that are either:

1. referred by any customer with id != 2.
2. not referred by any customer.

Return the result in any order.

The result format is in the following example.

**Input:** 

Table: Customer

| id | name | referee_id |
|----|------|------------|
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |


**Output:**

| name |
|------|
| Will |
| Jane |
| Bill |
| Zack |

### Solution  # 2


```SQL
SELECT name 
FROM Customer
WHERE referee_id != 2
OR
referee_id is null
```


### Exercise # 3

Table: World

| Column Name | Type    |
|-------------|---------|
| name        | varchar |
| continent   | varchar |
| area        | int     |
| population  | int     |
| gdp         | bigint  |

"name" is the primary key (column with unique values) for this table.
Each row of this table gives information about the name of a country, 
the continent to which it belongs, its area, the population, and its GDP value.
 
#### Question 

A country is big if:

1. It has an area of at least three million (i.e., 3,000,000 km2), or
2. It has a population of at least twenty-five million (i.e., 25,000,000).

Write a solution to find the name, population, and area of the big countries.

Return the result table in any order.

The result format is in the following example.

**Input:** 

Table: world

| name        | continent | area    | population | gdp          |
|-------------|-----------|---------|------------|--------------|
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |


**Output:** 

| name        | population | area    |
|-------------|------------|---------|
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |


###  Solution # 3


```SQL
SELECT name, population, area
FROM World
WHERE area >= 3000000 
OR
population >= 25000000
```



### Exercise # 4

Table: Views

| Column Name | Type |
|-------------|------|
| article_id  | int  |
| author_id   | int  |
| viewer_id   | int  |
| view_date   | date |

There is no primary key (column with unique values) for this table, the table may have duplicate rows.
Each row of this table indicates that some viewer viewed an article (written by some author) on some date. 
Note that equal author_id and viewer_id indicate the same person.

#### Question 

1. Write a solution to find all the authors that viewed at least one of their own articles.

2. Return the result table sorted by id in ascending order.

The result format is in the following example.

**Input:** 

Table: Views

| article_id | author_id | viewer_id | view_date  |
|------------|-----------|-----------|------------|
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |


**Output:** 

| id |
|----|
| 4  |
| 7  |


###  Solution # 4


```SQL
SELECT DISTINCT AUTHOR_ID AS id
FROM VIEWS
WHERE author_id = viewer_id ORDER BY author_id ASC
```
