# Exercises

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