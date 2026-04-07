5.
CREATE VIEW nome_cliente AS SELECT first_name, last_name FROM customer UNION SELECT first_name, last_name FROM staff;

6.
CREATE VIEW cliente_aluga_filme AS SELECT c.first_name, c.last_name, COUNT(rental_id) FROM customer c LEFT JOIN rental ON c.customer_id = rental.customer_id GROUP BY c.first_name, c.last_name;