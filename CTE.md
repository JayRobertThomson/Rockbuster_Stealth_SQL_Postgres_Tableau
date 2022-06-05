# Common Table Expression

## Find average payment of customers with the TOP 5 customers using TOP 10 Cities

WITH cte_total_payments (customer_id,
					     first_name,
					     last_name,
					     country,
					     city,
					     total_amount_paid) AS

( SELECT A.customer_id,
	   B.first_name,
	   B.last_name,
	   D.city,
	   E.country,
	   SUM (amount) AS highest_amount_paid
FROM payment A
INNER JOIN customer B ON A.customer_id = B.customer_id
INNER JOIN address C ON B.address_id = C.address_id
INNER JOIN city D ON C.city_id = D.city_id
INNER JOIN country E ON D.country_id = D.country_id
WHERE E.country IN ('India', 
					'China', 
					'United States', 
					'Japan', 
					'Mexico', 
					'Brazil', 
					'Russina Federation', 
					'Philippines', 
					'Turkey', 
					'Indonesia')
AND D.city IN ('Aurora', 
			   'Atlixco', 
			   'Xintai', 
			   'Adoni', 
			   'Dhule(Dhulia)', 
			   'Kurashiki', 
			   'Puinxiang', 
			   'Sivas', 
			   'Celaya', 
			   'So Leopoldo')
GROUP BY A.customer_id,
	     B.first_name,
	     B.last_name,
	     D.city,
	     E.country
ORDER BY SUM (amount) DESC
LIMIT 5)

SELECT AVG (total_amount_paid) AS average_payment
FROM cte_total_payments

![image](https://user-images.githubusercontent.com/106902397/172072013-1b5cdadc-e3f5-46f3-8331-c24452833024.png)


## Top customer count by countries

WITH 		cte_customer (customer_id, 
				 		  first_name, 
						  last_name, 
						  city, 
						  country, 
					   	  total_amount_paid) AS

(SELECT 	customer.customer_id, 
		    customer.first_name, 
		    customer.last_name, 
		    city.city, 
		    country.country, 
		    SUM(payment.amount) AS total_amount_paid
FROM payment
INNER JOIN 	customer ON payment.customer_id = customer.customer_id
INNER JOIN 	address ON customer.address_id = address.address_id
INNER JOIN 	city ON address.city_id = city.city_id
INNER JOIN 	country ON city.country_id = country.country_id 
WHERE 		city.city IN ('Aurora', 
			      'Tokat',
			      'Tarsus',
			      'Atlixco', 
			      'Emeishan',
			      'Pontianak',
			      'Shimoga',
			      'Aparecida de Goinia',
			      'Zalantun',
			      'Taguig')
GROUP BY 	customer.customer_id, 
		    customer.first_name, 
		    customer.last_name, 
	        city.city, 
			country.country
ORDER BY total_amount_paid DESC
LIMIT 5) 

SELECT 		country.country,
	       	COUNT(DISTINCT customer.customer_id) AS all_customer_count,
	       	COUNT(DISTINCT cte_customer.customer_id) AS top_customer_count
FROM 		customer 
INNER JOIN 	address ON customer.address_id = address.address_id
INNER JOIN 	city ON address.city_id = city.city_id
INNER JOIN 	country ON city.country_id = country.country_id
LEFT JOIN 	cte_customer ON country.country = cte_customer.country
GROUP BY 	country.country
ORDER BY 	all_customer_count DESC


![image](https://user-images.githubusercontent.com/106902397/172072249-bb68e05f-52fc-4ed5-9d13-e3067a04a4b9.png)
