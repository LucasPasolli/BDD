# Ejercicios Clase 7

## Lucas Pasolli

### 1. Find the films with the lesser duration, show the title and rating.
```sql
SELECT title, rating
FROM film
WHERE length <= ALL (SELECT length FROM film)
```

### 2. Write a query that returns the tiltle of the film which duration is the lowest. If there are more than one film with the lowest durtation, the query returns an empty resultset.
```sql
SELECT title, rating
FROM film 
WHERE length < ALL (SELECT length FROM film);
```


### 3. Generate a report with list of customers showing the lowest payments done by each of them. Show customer information, the address and the lowest amount, provide both solution using ALL and/or ANY and MIN.

```sql
SELECT c.first_name, c.last_name, a.address, p.amount
FROM address a , payment p , customer c
WHERE p.amount <= ALL (SELECT amount FROM payment) and p.amount != 0;
```

### 4. Generate a report that shows the customer's information with the highest payment and the lowest payment in the same row.
```sql
SELECT first_name, last_name
FROM customer
WHERE customer_id IN(
    SELECT customer_id 
    FROM rental r
    GROUP BY customer_id 
    HAVING COUNT(*) > 1);
    
SELECT c.first_name, c.last_name, a.address, p.amount
FROM address a , payment p , customer c
WHERE p.amount <= (SELECT MIN(amount) FROM payment) AND p.amount
AND a.address_id = c.address_id
AND p.customer_id = c.customer_id;
```

### 5. Generate a report that shows the customer's information with the highest payment and the lowest payment in the same row.
```sql
SELECT customer.customer_id, first_name, last_name, MAX(amount) max_amount,MIN(amount) min_amount
FROM customer, payment 
WHERE customer.customer_id = payment.customer_id 
GROUP BY customer_id, first_name, last_name 
ORDER BY max_amount DESC, customer_id DESC ;
```


