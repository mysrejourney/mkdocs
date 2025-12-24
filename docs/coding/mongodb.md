# Exercises from Leetcode - MongoDB


### Exercise # 1

Collection: Products

| Field      | Data type |
|------------|-----------|
| product_id | int       |
| low_fats   | enum      |
| recyclable | enum      |


low_fats is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM (category) of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.
 
#### Question 
Write a solution to find the ids of products that are both low fat and recyclable.
Return the result table in any order.
The result format is in the following example.

**Example 1:**

**Input:** 
Products collection:

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

```MongoDB
db.practice.find({low_fats: 'Y', recyclable: 'Y'},{_id:0, product_id: 1}).sort({product_id: 1})
```

![mongo_1.png](../assets/mongo_1.png)

**Explanation:** 
Only products 1 and 3 are both low fat and recyclable.


### Exercise # 2

Collections: Customer

| Field      | Data type |
|------------|-----------|
| id         | int       |
| name       | string    |
| referee_id | int       |


In collection, id is the primary key column for this table.
Each document of this collection indicates the id of a customer,
their name, and the id of the customer who referred them.
 

#### Question 
Find the names of the customer that are either:

1. referred by any customer with id != 2.
2. not referred by any customer.

Return the result in any order.

The result format is in the following example.

**Input:** 

Collections: Customer

| id | name | referee_id |
|----|------|------------|
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |


Output:

| name |
|------|
| Will |
| Jane |
| Bill |
| Zack |

### Solution  # 2

```MongoDB
db.practice.find({$or: [{referee_id: {$ne: 2}},{referee_id: null}]},{_id:0, name: 1})
```

![mongo_2.png](../assets/mongo_2.png)




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

Input: 

Collection: world

| name        | continent | area    | population | gdp          |
|-------------|-----------|---------|------------|--------------|
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |


Output: 

| name        | population | area    |
|-------------|------------|---------|
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |


###  Solution # 3


```MongoDB
db.world.find({$or: [{country: {$gt: 3000000}}, {population: {$gt: 25000000}}]},{name: 1, population: 1, area: 1, _id: 0})
```

![mongo_3.png](../assets/mongo_3.png)



### Exercise # 4

Collections: Views

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

Collections: Views

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
db.views.aggregate([
{
	$match: {
		$expr: { 
			$eq: ["$author_id", "$viewer_id"] 
		}
	}
},
{
	$group: {
		_id: "$viewer_id",
	}
},
{
	$project: {
		_id: 0,
		id: "$_id"
	}
},
{
	$sort: {
		id: -1
	}
}
])
```

![mongo_4.png](../assets/mongo_4.png)



### Exercise # 5

Collection: Tweets

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

Collection: Tweets

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
db.tweets.aggregate([
{
	$match: {
		$expr: {
			$gt:
			[
				{
					$strLenCP: "$content"
				}, 15 
			]
		}
	}
},
{
	$project: {
		_id: 0, 
		tweet_id: 1
	}
}
])
```

![mongo_5.png](../assets/mongo_5.png)



### Exercise # 6 - Replace Employee ID With The Unique Identifier

Collection: Employees

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |


id is the primary key (column with unique values) for this collection.
Each row of this collection contains the id and the name of an employee in a company.



Collection: EmployeesUNI

| Column Name | Type |
|-------------|------|
| id          | int  |
| unique_id   | int  |

(id, unique_id) is the primary key (combination of columns with unique values) for this collection.
Each row of this collection contains the id and the corresponding unique id of an employee in the company.

#### Question 

1. Write a solution to show the unique ID of each user, If a user does not have a unique ID replace just show null.

2. Return the result collection in any order

The result format is in the following example.

**Input:** 

Collection: Employees

| id | name     |
|----|----------|
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |

Collection: EmployeesUNI

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


```MongoDB
db.employees.aggregate([
{
	$lookup: {
		from: "employeesUni",
		localField: "id",
		foreignField: "id",
		 as: "matchedData"
	}
},
{
	$unwind: {
		path: "$matchedData",
		preserveNullAndEmptyArrays: true
	}
},
 {
    $unset: "matchedData._id"
 },
{
	$project: {
		_id: 0,
		unique_id: {
			$ifNull: ["$matchedData", "null"]
		},
		name: 1
	}
},
])
```

![mongo_6.png](../assets/mongo_6.png)


### Lesson Learnt

1. $lookup ALWAYS returns an array, even if there is only one match. That’s why $unwind is needed.
2. $unwind will produce multiple output documents (one per match).
3. You DON’T need $unwind when
   * You want the joined data as an array
   * You don’t need to access individual fields.
   * You don’t care about NULL handling