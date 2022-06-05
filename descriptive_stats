#Descriptive Statistics for the Films and Customer Tables 

##Films 

SELECT COUNT(film_id) AS count_film_id,
	   MIN (rental_duration) AS min_rental,
	   MAX (rental_duration) AS max_rental,
	   AVG (rental_duration) AS avg_rental,
	   
	   MIN (rental_rate) AS min_rate,
	   MAX (rental_rate) AS max_rate,
	   AVG (rental_rate) AS avg_rate,
	   
	   MIN (length) AS min_length,
	   MAX (length) AS max_length,
	   AVG (length) AS avg_length,
	   
	   MIN (replacement_cost) AS min_cost,
	   MAX (replacement_cost) AS max_cost,
	   AVG (replacement_cost) AS avg_cost,
	   
	   MODE() WITHIN GROUP(ORDER BY rating) AS modal_rating,
	   
	   MODE() WITHIN GROUP(ORDER BY description) AS modal_description,
	   
	   MODE() WITHIN GROUP(ORDER BY title) AS modal_title
	   
FROM film;


##Customers 

SELECT COUNT(customer_id) AS count_cust,
	   MIN(customer_id) AS min_cust,
	   MAX(customer_id) AS max_cust,
	   AVG(customer_id) AS avg_cust,
	   
	   COUNT(store_id) AS count_store,
	   
	   COUNT(first_name) AS count_first_name,
	   COUNT(last_name) AS count_last_name,
	   COUNT(email) AS count_email
	   
FROM customer;


