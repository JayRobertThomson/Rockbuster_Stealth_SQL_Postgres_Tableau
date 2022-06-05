 # Filtering
 
 ## Filtering with CASE - movies to show parents which are suitable for kids
 
       SELECT film_id,
             title,
             rating,
             CASE
                 WHEN rating = 'PG' THEN 'Kids allowed'
                 WHEN rating = 'NC-17' THEN 'Not allowed'
                 ELSE 'Parental Guidance recommended'
             END AS kids_allowed
      FROM film

![image](https://user-images.githubusercontent.com/106902397/172073800-aef8d49b-62eb-440c-aa54-08f746d81340.png)

## Count of stores with more than 2300 movies 

          SELECT store_id,
                 COUNT(store_id) AS count_of_movies
          FROM inventory
          GROUP BY store_id
          HAVING COUNT(store_id) > 2300
          ORDER BY count_of_movies DESC
          
![image](https://user-images.githubusercontent.com/106902397/172073837-a7fd7402-e2ac-4579-93cb-87d0be0c0d11.png)

## Filtering with IN

          SELECT *
          FROM film
          WHERE rating IN ('PG',
                           'G',
                           'PG-13')
                           
## Count of movies with PG or G rating

          SELECT rating,
          COUNT (film_id) AS count_of_movies,
          AVG (rental_rate) AS average_movie_rental_rate,
          MIN (rental_duration) AS minimun_rental_duration,
          MAX (rental_duration) AS maximun_rental_duration
          FROM film
          WHERE rating = 'PG' OR rating = 'G'
          GROUP BY rating
          
![image](https://user-images.githubusercontent.com/106902397/172074009-122cecf5-4e56-420f-902d-600681475a89.png)


## Movies > 120mins

          SELECT film_id,
               title,
               description
          FROM film
          WHERE length > 120
          ORDER BY film_id ASC
          
