# Subquery on Top 10 countries and if they have Top count customers

        SELECT (country.country),
            COUNT(DISTINCT customer.customer_id) AS all_customer_count,
            COUNT(DISTINCT country.country_id) AS top_customer_count
        FROM
        (SELECT A.customer_id,
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
        LIMIT 10) AS top_10_customers

        LEFT JOIN customer ON customer.customer_id = customer.customer_id 
        LEFT JOIN address ON customer.address_id = address.address_id
        LEFT JOIN city ON address.city_id = city.city_id
        LEFT JOIN country ON city.country_id = country.country_id
        GROUP BY country.country
        ORDER BY all_customer_count DESC
        LIMIT 10;

![image](https://user-images.githubusercontent.com/106902397/172073677-f253b901-2676-4ca6-8df1-a71e6aaa3c3c.png)

