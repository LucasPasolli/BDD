# Ejercicios Clase 11

## Lucas Pasolli

### 4. Find all the film titles that are not in the inventory. 

```sql
SELECT title 
FROM film f
left join inventory i 
ON f.film_id = i.film_id 
WHERE i.film_id is NULL 
```

### 5. Find all the films that are in the inventory but were never rented. 
   - Show title and inventory_id.  
   - This exercise is complicated. 
   - hint: use sub-queries in FROM and in WHERE or use left join and ask if one of the fields is null

```sql
SELECT title, inventory_id
FROM film f
INNER JOIN inventory i USING(film_id)
LEFT JOIN rental r USING(inventory_id)  
WHERE r.rental_id is NULL
```

### 6. Generate a report with.
   - customer (first, last) name, store id, film title.
   - when the film was rented and returned for each of these customers.
   - order by store_id, customer last_name.

```sql
SELECT c.first_name, c.last_name, s.store_id, f.title
FROM film f 
INNER JOIN inventory i USING(film_id)
INNER JOIN rental r USING(inventory_id)
INNER JOIN customer c ON c.customer_id = r.customer_id 
INNER JOIN store s ON s.store_id = c.store_id
WHERE NOT r.return_date IS NULL
ORDER BY s.store_id, c.last_name 
```

### 7. Show sales per store (money of rented films).
   - show store's city, country, manager info and total sales (money).

```sql
SELECT s.store_id, CONCAT(s2.first_name, ' ', s2.last_name) as manager, s2.email as manager_mail, c2.city, c3.country, SUM(p.amount) as money_of_rented_films
FROM payment p
INNER JOIN rental r ON p.rental_id = r.rental_id
INNER JOIN customer c ON r.customer_id = c.customer_id
INNER JOIN store s ON c.store_id = s.store_id
INNER JOIN address a ON s.address_id = a.address_id 
INNER JOIN city c2 ON a.city_id = c2.city_id 
INNER JOIN country c3 ON c2.country_id =c3.country_id
INNER JOIN staff s2 ON s.manager_staff_id = s2.staff_id
GROUP BY s.store_id
```

### 9. Which actor has appeared in the most films?

```sql
SELECT a.first_name, COUNT(fa.actor_id) AS films
FROM film f 
INNER JOIN film_actor fa ON f.film_id = fa.film_id
INNER JOIN actor a ON fa.actor_id = a.actor_id
GROUP BY a.first_name 
ORDER BY films DESC
LIMIT 1
```