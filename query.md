# Atividades avaliativas


### 2- Escolha uma tabela qualquer e crie uma visão sobre ela.
R: 

### 3- Escolha duas tabelas com cardinalidade 1:N e crie uma visão que faça uma junção entre elas.
R: 

### 4- Crie duas sequencias para serem usadas em duas tabelas quaisquer e faça pelo menos dois inserts em cada uma delas.
R:

### 5- Crie uma visão que faça uma união (UNION) entre os campos nomes dentro das tabelas customer e staff.
R: CREATE VIEW nome_cliente AS SELECT first_name, last_name FROM customer UNION SELECT first_name, last_name FROM staff;

select * from nome_cliente;

### 6- Crie uma visão para trazer os nomes dos clientes (customers) que alugaram os filmes. A consulta deve trazer o nome (first_name + last_name) e a quantidade de filmes alugados. Importante: se o cliente não alugou nada, deve trazer a quantidade 0.
R: CREATE VIEW cliente_aluga_filme AS SELECT c.first_name, c.last_name, COUNT(rental_id) FROM customer c LEFT JOIN rental ON c.customer_id = rental.customer_id GROUP BY c.first_name, c.last_name;

select * from cliente_aluga_filme;

### 7- Crie uma visão para trazer os nomes dos clientes (customers) que alugaram os filmes. A consulta deve trazer o nome (first_name + last_name) e os títulos dos filmes alugados. Importante: se o cliente não alugou nada, deve trazer valor nulo.
R: 
