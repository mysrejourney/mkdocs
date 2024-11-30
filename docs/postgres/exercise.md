# Exercises

## DB-TASK-001

**1. Retrieve film titles and their rental rates. Use column aliases to rename title as "Movie Title" and rental_rate as "Rate".**

SELECT title AS "Movie Title", rental_rate AS "Rate" FROM film;

**2. List customer names and their email addresses. Alias first_name and last_name as "First Name" and "Last Name".**

SELECT first_name AS "First name", last_name AS "Last Name" FROM customer;

**3. Get a list of films sorted by rental rate in descending order. If two films have the same rental rate, sort them alphabetically by title.**

SELECT title AS "Movie Title", rental_rate AS "Rate" FROM film ORDER BY "Rate" DESC, "Movie Title" ASC;

**4. Retrieve actor names sorted by last name, then first name.**

SELECT first_name AS "FIRST NAME", last_name AS "LAST NAME" FROM actor ORDER BY "LAST NAME", "FIRST NAME";

**5. List all unique replacement costs from the film table.**

SELECT DISTINCT replacement_cost FROM film;

**6. List all films' title and length in minutes. Alias length as "Duration (min)".**

SELECT title AS "Movie Title", length AS "Duration (Mins)" FROM film;

**7. Retrieve customer first and last names along with their active status. Alias active as "Is Active".**

SELECT first_name AS "First name", last_name AS "Last name", activebool AS "Is Active" from customer;

**8. Retrieve the list of film categories sorted alphabetically.**

SELECT name AS "FILM CATEGORY" from category ORDER BY "FILM CATEGORY";

**9. List films by length, sorted in descending order. Include only the title and length.**

SELECT title AS "MOVIE TITLE", length AS "DURATION (MINS)" FROM film ORDER BY "DURATION (MINS)" DESC;

**10. Retrieve all actor names, sorted by their first name in descending order.**

SELECT first_name AS "FIRST NAME" FROM actor ORDER BY "FIRST NAME" DESC;

**11. List all unique ratings available in the film table.**

SELECT DISTINCT rating AS "RATING" FROM film;

**12. Find all unique rental durations from the film table.**

SELECT DISTINCT rental_rate AS "RENTAL RATE" FROM film;

***************************************************

**13. Retrieve the first unique customer ID based on active status. Include the customer_id and active columns, and order by customer_id.**

SELECT DISTINCT customer_id AS "CUSTOMER ID", active AS "ACTIVE" from customer ORDER BY "CUSTOMER ID" limit 1;

**************************************************

**14. List the earliest rental date for each customer. Include customer_id and rental_date, and order by customer_id.**

SELECT DISTINCT customer_id AS "CUSTOMER ID", rental_date AS "RENTAL DATE" FROM rental ORDER BY "RENTAL DATE" ASC;

**15. List the 10 shortest films by length. Include the title and length.**

SELECT title "MOVIE TITLE", length "DURATION" from film ORDER BY "DURATION" limit 10;

**16. Get the top 5 customers with the highest customer_id. Include the first and last name.**

SELECT customer_id AS "CUSTOMER ID", first_name AS "FIRST NAME", last_name AS "LAST NAME" from customer ORDER BY "CUSTOMER ID" DESC limit 5;

**17. Retrieve all unique values of store_id from the inventory table.**

SELECT DISTINCT store_id AS "STORE ID" from inventory;

**18. Find all unique replacement_cost values in the film table. Sort the results in ascending order.**

SELECT DISTINCT replacement_cost "REPLACEMENT COST" FROM film ORDER BY "REPLACEMENT COST" ASC;

***************************************************
**19. List the first rental date for each store. Include store_id and rental_date, and sort by store_id.**

SELECT rental_date AS "RENTAL DATE", store_id AS "STORE ID" FROM <table> ORDER BY "STORE ID";

***************************************************

**20. Retrieve a list of film ratings sorted alphabetically and include only unique values.**

SELECT DISTINCT rating AS "RATING" FROM film ORDER BY "RATING";

**21. List films by rating in ascending order and length in descending order.**

SELECT rating AS "RATING", length AS "DURATION" FROM film ORDER BY "RATING" ASC, "DURATION" DESC;

**22. Retrieve actor names sorted by last_name in ascending order and first_name in descending order.**

SELECT first_name AS "FIRST NAME", last_name AS "LAST NAME" FROM actor ORDER BY "LAST NAME" ASC, "FIRST NAME" DESC;

**23. List films ordered by replacement_cost in ascending order and rental_rate in descending order.**

SELECT replacement_cost "REPLACEMENT COST", rental_rate "RATE" FROM film ORDER BY "REPLACEMENT COST" ASC, "RATE" DESC;

**24. Retrieve customer names sorted by last_name ascending and first_name descending.**

SELECT first_name "FIRST NAME", last_name "LAST NAME" FROM customer ORDER BY "LAST NAME" ASC, "FIRST NAME" DESC;

**25. List all rentals sorted by customer_id ascending and rental_date descending.**

SELECT * FROM rental ORDER BY customer_id ASC, rental_date DESC;

**26. Retrieve a list of films ordered by rental_duration ascending and title descending.**

SELECT title "MOVIE NAME", rental_duration "RENTAL DURATION" FROM film ORDER BY rental_duration ASC, "MOVIE NAME" DESC;

---

## DB-TASK-002

**1. Get all movies (films) that have a rental rate greater than $3.**

SELECT title, rental_rate FROM film WHERE rental_rate > 3;

**2. Get all movies that have a rental rate greater than $3 and a replacement cost less than $20.**

SELECT title, rental_rate, replacement_cost FROM film WHERE rental_rate > 3 AND replacement_cost < 20;

**3.Get all movies that are either rated as 'PG' or have a rental rate of $0.99.**

SELECT title, rating, rental_rate FROM film WHERE rating='PG' OR rental_rate=0.99; 

**4. Show the first 10 movies sorted by rental rate (highest first).**

SELECT title, rental_rate FROM film ORDER BY rental_rate DESC LIMIT 10;

**5. Skip the first 5 movies and fetch the next 3 sorted by rental rate in ascending order.**

SELECT title, rental_rate FROM film ORDER BY rental_rate ASC OFFSET 5 LIMIT 3;

---
**6. Skip the first 5 movies and fetch the next 3 sorted by rental rate in ascending order.**

SELECT title, rental_rate FROM film ORDER BY rental_rate ASC OFFSET 5 FETCH NEXT 3 ROWS ONLY;
---

**7. Get all movies with a rental duration between 3 and 7 days.**

SELECT title, rental_duration FROM film WHERE rental_duration BETWEEN 3 AND 7;

**8. Get all movies where the title starts with 'A' and ends with 'e'**

SELECT title FROM film WHERE title LIKE 'A%e';

**9. Find all customers who do not have an email address listed.**

SELECT first_name, last_name FROM customer WHERE email is NULL;

**10. Find all movies released in 2006 with a rental rate of $2.99 or $3.99, and their title starts with 'S'. 
Display the top 5 results.
SELECT title, rental_rate, release_year**

SELECT title,rental_rate,
release_year FROM film WHERE release_year=2006 AND rental_rate IN (2.99, 3.99) AND title LIKE 'S%' LIMIT 5;

**11. Display 10 customers after skipping the first 20, sorted alphabetically by last name.**

SELECT first_name, last_name FROM customer ORDER BY last_name ASC OFFSET 20 LIMIT 10;

**12. Get the top 5 movies with the highest replacement cost, skipping the most expensive one.**

SELECT title, replacement_cost FROM film ORDER BY replacement_cost DESC OFFSET 1 FETCH NEXT 5 ROWS ONLY;

**13. Find all rentals that occurred between '2005-05-01' and '2005-06-01'.**

SELECT rental_date FROM rental WHERE rental_date BETWEEN '2005-05-01' AND '2005-06-01';

**14. Get all actors whose last names contain the letters "man".**

SELECT first_name, last_name FROM actor WHERE last_name LIKE '%man%';

**15. Find all movies where the special features are not listed (i.e., special_features is NULL).**

SELECT title FROM film WHERE special_features is NULL;

**16. Find all movies where the rental duration is more than 7 days.**

SELECT title, rental_duration FROM film WHERE rental_duration > 7;

**17. Find the first 10 movies with a rental rate of $2.99 or $4.99, a rating of 'R', and a title containing the word "L".**

SELECT title, rental_rate, rating FROM film WHERE rating='R'
AND title LIKE '%L%' AND rental_rate IN (2.99, 4.99) LIMIT 10;

**18. Find all movies where the title starts with "A" or "B" and ends with "s".**

SELECT title FROM film WHERE title SIMILAR TO '[AB]%s';

**19.Find all movies where the title contains "Man", "Men", or "Woman".**

SELECT title FROM film WHERE title SIMILAR TO '%(Man|Men|Woman)%';

---

## Bonus Q/A

--- 
**1. Find all movies where the special features are not listed (i.e., special_features is NULL).**

SELECT title FROM film WHERE special_features is NULL;

**2. Find all movies where the rental duration is more than 7 days.**

SELECT title, rental_duration FROM film WHERE rental_duration > 7;

---

**3. Find all movies that have a rental rate of $4.99 and a replacement cost of more than $20.**

SELECT title, rental_rate, replacement_cost FROM film WHERE rental_rate = 4.99 AND replacement_cost > 20;

**4. Find all movies that have a rental rate of $0.99 or a rating of 'PG-13'.**

SELECT title, rental_rate, rating FROM film WHERE rental_rate=0.99 AND rating = 'PG-13';

**5. Retrieve the first 5 rows of movies sorted alphabetically by title.**

SELECT title FROM film ORDER BY title ASC LIMIT 5;

**6. Skip the first 10 rows and fetch the next 3 movies with the highest replacement cost.**

SELECT title, replacement_cost FROM film ORDER BY replacement_cost DESC OFFSET 10 FETCH NEXT 3 ROWS ONLY;

**7. Find all movies where the rating is either 'G', 'PG', or 'PG-13'.**

SELECT title, rating FROM film WHERE rating IN ('G', 'PG', 'PG-13');

**8. Find all movies with a rental rate between $2 and $4.**

SELECT title, rental_rate FROM film WHERE rental_rate BETWEEN 2 AND 4;

**9. Find all movies with titles that start with 'The'.**

SELECT title FROM film WHERE title LIKE 'The%';

**10. Find the first 10 movies with a rental rate of $2.99 or $4.99, a rating of 'R', and a title containing the word "Love".**

SELECT title, rental_rate, rating FROM film WHERE title LIKE '%Love%'
AND rental_rate IN (2.99, 4.99) AND rating='R' LIMIT 10;

**11. Find all movies where the title contains the % symbol.**

SELECT title FROM film WHERE title SIMILAR TO '%$%%' ESCAPE '$';

**12. Find all movies where the title contains an underscore (_).**

SELECT title FROM film WHERE title SIMILAR TO '%!_%' ESCAPE '!';

---
**13. Find all movies where the title starts with "A" or "B" and ends with "s".**

SELECT title FROM film WHERE title SIMILAR TO '[AB]%s';

**14. Find all movies where the title contains "Man", "Men", or "Woman".**

SELECT title FROM film WHERE title SIMILAR TO '%(Man|Men|Woman)%';

---

**15. Find all movies with titles that contain digits (e.g., "007", "2", "300").**

SELECT title FROM film WHERE title SIMILAR TO '%[0-9]%';

**16. Find all movies with titles containing a backslash (\).**

SELECT title FROM film WHERE title SIMILAR TO '%\\%';

**17. Find all movies where the title does contain the words "Love" or "Hate".**

SELECT title FROM film WHERE title !~~ '%Love%' OR title !~~ '%Hate%';

**18. Find the first 5 movies with titles that end with "er", "or", or "ar".**

SELECT title FROM film WHERE title SIMILAR TO '%(er|or|ar)';


---






