# JOINS

## INNER JOIN

      SELECT A.payment_id,
             A.customer_id,
             A.amount,
             B.first_name,
             B.last_name
      FROM payment A
      INNER JOIN customer B ON A.customer_id = B.customer_id
 

## LEFT JOIN

        SELECT A.payment_id,
               A.customer_id,
               A.amount,
               B.first_name,
               B.last_name
        FROM payment A
        LEFT JOIN customer B ON A.customer_id = B.customer_id
        
 

## RIGHT JOIN

        SELECT A.payment_id,
               A.customer_id,
               A.amount,
               B.first_name,
               B.last_name
        FROM payment A
        RIGHT JOIN customer B ON A.customer_id = B.customer_id

## FULL JOIN

        SELECT A.payment_id,
               A.customer_id,
               A.amount,
               B.first_name,
               B.last_name
        FROM payment A
        FULL JOIN customer B ON A.customer_id = B.customer_id
        
## MULTIPLE JOIN 

        SELECT A.staff_id,
               D.country
        FROM staff A
        INNER JOIN address B ON A.address_id = B.address_id
        INNER JOIN city C ON B.city_id = C.city_id
        INNER JOIN country D ON C.country_ID = D.country_ID
        
# Further JOINS 

## Top 10 countries by count of customers

        SELECT D.country,
             COUNT (customer_id) AS customer_count
        FROM customer A
        INNER JOIN address B ON A.address_id = B.address_id
        INNER JOIN city C ON B.city_id = C.city_id
        INNER JOIN country D ON C.country_ID = D.country_ID
        GROUP BY country
        ORDER BY COUNT (customer_id) DESC
        LIMIT 10;

![image](https://user-images.githubusercontent.com/106902397/172072789-66157052-bff6-4f78-840a-c61dcf62344f.png)


## Top 10 cities from the Top 10 countries

        SELECT D.country,
             C.city,
             COUNT (customer_id) AS customer_count
        FROM customer A
        INNER JOIN address B ON A.address_id = B.address_id
        INNER JOIN city C ON B.city_id = C.city_id
        INNER JOIN country D ON C.country_ID = D.country_ID
        WHERE D.country IN ('India',
                  'China',
                  'United States',
                  'Japan',
                  'Mexico',
                  'Brazil',
                  'Russian Federation',
                  'Philippines',
                  'Turkey',
                  'Indonesia')
        GROUP BY city, country
        ORDER BY COUNT (customer_id) DESC
        LIMIT 10;
        
![image](https://user-images.githubusercontent.com/106902397/172072967-6f70bfbf-be71-4748-93a5-88c1eaac0394.png)

## Top 10 customers from the Top 10 coutries and Top 10 cities

        SELECT A.customer_id,
             B.first_name,
             B.last_name,
             E.country,
             D.city,
             SUM (amount) AS highest_amount_paid
        FROM payment A
        INNER JOIN customer B ON A.customer_id = B.customer_id
        INNER JOIN address C ON B.address_id = C.address_id
        INNER JOIN city D ON C.city_id = D.city_id
        INNER JOIN country E ON D.country_ID = E.country_ID
        WHERE E.country IN ('India',
                  'China',
                  'United States',
                  'Japan',
                  'Mexico',
                  'Brazil',
                  'Russian Federation',
                  'Philippines',
                  'Turkey',
                  'Indonesia')
        AND D.city IN ('Aurora',
                 'Atlixco',
                 'Xintai',
                 'Adoni',
                 'Dhule (Dhulia)',
                 'Kurashiki',
                 'Pingxiang',
                 'Sivas',
                 'Celaya',
                 'So Leopoldo')
        GROUP BY A.customer_id,
               B.first_name,
               B.last_name,
               E.country,
               D.city
        ORDER BY SUM (amount) DESC
        LIMIT 10;
        
        ![image](https://user-images.githubusercontent.com/106902397/172073252-9ed8e8ac-20f2-48c3-855e-d4e2dc52145a.png)

