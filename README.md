# sql-12
SELECT COUNT(*) FROM film
WHERE length > (SELECT AVG(length) FROM film);

SELECT COUNT((SELECT MAX(rental_rate) FROM film)) FROM film

SELECT title FROM film
WHERE (rental_rate  = (SELECT MIN(rental_rate) FROM film)) AND (replacement_cost = (SELECT MIN(replacement_cost) FROM film));

SELECT customer.first_name, customer.last_name FROM customer
JOIN payment On customer.customer_id = ANY
(SELECT customer_id FROM payment
GROUP BY customer_id 
ORDER BY COUNT(customer_id) DESC
LIMIT 5)
LIMIT 5;
