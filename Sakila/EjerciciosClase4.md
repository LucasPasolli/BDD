# Ejercicios Clase 4 

## Lucas Pasolli

### 1. Show title and special_features of films that are PG-13
```sql
SELECT title, special_features
FROM film WHERE rating = 'PG-13';
```
### 2. Get a list of all the different films duration.
```sql
SELECT LENGTH FROM film;
```
### 3. Show title, rental_rate and replacement_cost of films that have replacement_cost from 20.00 up to 24.00
```sql
SELECT title, rental_rate, replacement_cost 
FROM film where replacement_cost BETWEEN 20 and 24;
```
### 4. Show title, category and rating of films that have 'Behind the Scenes' as special_features
```sql
SELECT title, name, rating
FROM film, film_category, category
WHERE film.film_id = film_category.film_id and special_features = 'Behind the Scenes';
```
### 5. Show first name and last name of actors that acted in 'ZOOLANDER FICTION'
```sql
SELECT  first_name, last_name
FROM film, film_actor, actor
WHERE film.film_id = film_actor.film_id and film.title = 'ZOOLANDER FICTION';
```
### 6. Show the address, city and country of the store with id 1
```sql
SELECT address, city, country
FROM store, address, city, country
WHERE store.store_id = 1;
```
### 7.  Show pair of film titles and rating of films that have the same rating.
```sql
SELECT f1.title, f2.title, f1.rating 
FROM film f1, film f2
WHERE f1.rating = f2.rating;
```
### 8. Get all the films that are available in store id 2 and the manager first/last name of this store (the manager will appear in all the rows).
```sql
SELECT title, first_name, last_name
FROM film, inventory, store, staff
WHERE film.film_id = inventory.film_id and inventory.store_id = store.store_id and store.manager_staff_id = staff.staff_id and store.store_id = 2;
```




