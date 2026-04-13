
--TRABALHO ABDD

-- 2- Escolha uma tabela qualquer e crie uma visão sobre ela.

create view v_actor_first_name as select first_name from actor;

select * from v_actor_first_name;

-- 3- Escolha duas tabelas com cardinalidade 1:N e crie uma visão que faça uma junção entre elas.

CREATE VIEW v_film_inventory AS SELECT f.film_id, f.title, i.inventory_id, i.store_id FROM film f
JOIN inventory i 
ON f.film_id = i.film_id;

select * from v_film_inventory;

SELECT COUNT(*) FROM inventory i
JOIN film f 
ON f.film_id = i.film_id
WHERE f.title = 'Academy Dinosaur';

-- 4- Crie duas sequencias para serem usadas em duas tabelas quaisquer e faça pelo menos dois inserts em cada uma delas.

CREATE SEQUENCE sid_country
START WITH 110;

-- select nextval('sid_country');

INSERT INTO country (country_id, country, last_update) VALUES (nextval('sid_country'),'Uruguay', '2026-04-14 10:00:00'),
															  (nextval('sid_country'),'Panama', '2026-04-14 11:30:00') RETURNING country_id;

--select * from country;

CREATE SEQUENCE sid_city
START WITH 601;

-- select nextval('sid_city');

INSERT INTO city (city_id, city, country_id, last_update) VALUES (nextval('sid_city'),'Montevideo', 110, '2026-04-14 10:00:00'),
															     (nextval('sid_city'),'Panama City', 110, '2026-04-14 11:30:00') RETURNING city_id;

-- select * from city;

-- 5- Crie uma visão que faça uma união (UNION) entre os campos nomes dentro das tabelas customer e staff.

CREATE VIEW nome_cliente AS SELECT first_name, last_name FROM customer UNION SELECT first_name, last_name FROM staff;

select * from nome_cliente;

-- 6- Crie uma visão para trazer os nomes dos clientes (customers) que alugaram os filmes. A consulta deve trazer o nome (first_name + last_name) e a quantidade de filmes alugados. Importante: se o cliente não alugou nada, deve trazer a quantidade 0.

CREATE VIEW cliente_aluga_filme AS SELECT c.first_name, c.last_name, COUNT(rental_id) FROM customer c LEFT JOIN rental ON c.customer_id = rental.customer_id GROUP BY c.first_name, c.last_name;

select * from cliente_aluga_filme;

-- 7- Crie uma visão para trazer os nomes dos clientes (customers) que alugaram os filmes. A consulta deve trazer o nome (first_name + last_name) e os títulos dos filmes alugados. Importante: se o cliente não alugou nada, deve trazer valor nulo.

CREATE VIEW v_nome_cliente_aluga_filme 
AS 
SELECT c.first_name AS nome, c.last_name AS sobrenome, f.title AS nome_filme  FROM customer c 
LEFT JOIN rental r ON c.customer_id = r.customer_id 
LEFT JOIN inventory i ON r.inventory_id = i.inventory_id 
LEFT JOIN film f ON i.film_id = f.film_id;

-- INSERT INTO customer VALUES (600, 1, 'Kawam', 'Freitas', 'freitas@gmail.com', 20 , true, '2026-01-20', '2026-04-14', 1);

SELECT * FROM v_nome_cliente_aluga_filme;

