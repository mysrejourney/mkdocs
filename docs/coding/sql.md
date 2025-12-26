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

### Exercise # 5

Table: Tweets

| Column Name | Type    |
|-------------|---------|
| tweet_id    | int     |
| content     | varchar |


Tweet_id is the primary key (column with unique values) for this table.
Content consists of alphanumeric characters, '!', or ' ' and no other special characters.
This table contains all the tweets in a social media app.

#### Question 

1. Write a solution to find the IDs of the invalid tweets. The tweet is invalid if the number of characters used in the content of the tweet is strictly greater than 15.

2. Return the result table in any order

The result format is in the following example.

**Input:** 

Table: Tweets

| tweet_id | content                           |
|----------|-----------------------------------|
| 1        | Let us Code                       |
| 2        | More than fifteen chars are here! |



**Output:** 

| tweet_id |
|----------|
| 2        |



###  Solution # 5


```SQL
SELECT tweet_id 
FROM TWEETS
WHERE
length(content) > 15
```

### Exercise # 6 - Replace Employee ID With The Unique Identifier

Table: Employees

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |


id is the primary key (column with unique values) for this table.
Each row of this table contains the id and the name of an employee in a company.



Table: EmployeesUNI

| Column Name | Type |
|-------------|------|
| id          | int  |
| unique_id   | int  |

(id, unique_id) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the id and the corresponding unique id of an employee in the company.

#### Question 

1. Write a solution to show the unique ID of each user, If a user does not have a unique ID replace just show null.

2. Return the result table in any order

The result format is in the following example.

**Input:** 

Table: Employees

| id | name     |
|----|----------|
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |

Table: EmployeesUNI

| id | unique_id |
|----|-----------|
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |

**Output:** 

| unique_id | name     |
|-----------|----------|
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |


###  Solution # 6


```SQL
SELECT EmployeeUNI.unique_id, Employees.name
FROM Employees
LEFT JOIN EmployeeUNI
ON Employees.id = EmployeeUNI.id
ORDER BY UNIQUE_ID DESC
```

### Lesson Learnt

When you want all records of one table, you need to use JOIN.
In this case, we are using LEFT JOIN.
Here we are filtering the rows based upon the condition where LEFT JOIN ensures all rows from Employees are included,
even if there’s no matching record.
For employees with no entry in EmployeeUNI,
the unique_id column will show NULL.
For those with a matching EmployeeUNI, you get their unique_id.




### Exercise # 7 - Product Sales Analysis I

Table: sales

| Column Name | Type |
|-------------|------|
| sale_id     | int  |
| product_id  | int  |
| year        | int  |
| quantity    | int  |
| price       | int  |


(sale_id, year) is the primary key (combination of columns with unique values) of this table.
product_id is a foreign key (reference column) to Product table.
Each row of this collection shows a sale on the product product_id in a certain year.
Note that the price is per unit.



Table: product

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

product_id is the primary key (column with unique values) of this table.
Each row of this table indicates the product name of each product.

#### Question 

1. Write a solution to report the product_name, year, and price for each sale_id in the Sales table.

2. Return the result collection in any order

The result format is in the following example.

**Input:** 

Table: sales

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

Table: product

| product_id | product_name |
|------------|--------------|
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

**Output:** 

| product_name | name | year |
|--------------|------|------|
| Nokia        | 2008 | 5000 |
| Nokia        | 2009 | 5000 |
| Apple        | 2011 | 9000 |


###  Solution # 7


```SQL
SELECT Product.product_name, Sales.year,Sales.Price
FROM Sales
LEFT JOIN Product
ON Sales.product_id = Product.product_id
```

### Lesson Learnt

Here we are filtering the rows based on 'INNER JOIN.' 
Inner join will keep the rows of both tables only if the condition is satisfied.


### Exercise # 8 - Customer Who Visited but Did Not Make Any Transactions

Table: Visits

| Column Name | Type |
|-------------|------|
| visit_id    | int  |
| customer_id | int  |


visit_id is the column with unique values for this table.
This table contains information about the customers who visited the mall.


Table: Transactions

| Column Name    | Type |
|----------------|------|
| transaction_id | int  |
| visit_id       | int  |
| amount         | int  |

transaction_id is a column with unique values for this table.
This table contains information about the transactions made during the visit_id.


#### Question 

1. Write a solution to find the IDs of the users who visited without making any transactions,
and the number of times they made these types of visits.

2. Return the result collection in any order

The result format is in the following example.

**Input:** 

Table: Visits

| visit_id | customer_id |
|----------|-------------|
| 1        | 23          |
| 2        | 9           |
| 4        | 30          |
| 5        | 54          |
| 6        | 96          |
| 7        | 54          |
| 8        | 54          |

Table: Transactions

| transaction_id | visit_id | amount |
|----------------|----------|--------|
| 2              | 5        | 310    |
| 3              | 5        | 300    |
| 9              | 5        | 200    |
| 12             | 1        | 910    |
| 13             | 2        | 970    |

**Output:** 

| customer_id | count_no_trans |
|-------------|----------------|
| 54          | 2              |
| 30          | 1              |
| 96          | 1              |

**Explanation:** 

Customer with id = 23 visited the mall once and made one transaction during the visit with id = 12.
Customer with id = 9 visited the mall once and made one transaction during the visit with id = 13.
Customer with id = 30 visited the mall once and did not make any transactions.
Customers with id = 54 visited the mall three times.During 2 visits they did not make any transactions, 
and during one visit they made 3 transactions.
Customer with id = 96 visited the mall once and did not make any transactions.
As we can see, users with IDs 30 and 96 visited the mall one time without making any transactions. 
Also, user 54 visited the mall twice and did not make any transactions.

###  Solution # 8


```SQL
SELECT  v.customer_id, COUNT(v.customer_id) as count_no_trans
FROM Visits v
LEFT JOIN Transactions t
ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id
```

![sql_8.png](../assets/sql_8.png)

### Lesson Learnt

Here we are filtering the rows based on 'LEFT JOIN.'
This will merge both tables and keep all records in table 1, and for table 2,
it will keep the records if the value matches and the rest of the column shows as "NULL."


