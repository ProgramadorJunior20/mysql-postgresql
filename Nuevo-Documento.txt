
/*
-- Creación de tablas
-- Agregar columnas a las tablas 
*/
CREATE TABLE IF NOT EXISTS employees(
	id INT,
);

-- Tipos de datos: CHAR, VARCHAR, TEXT
CREATE TABLE IF NOT EXISTS employees(
	id INT,
	name VARCHAR(250),
	married BOOLEAN,
	genre CHAR(1)
);

-- Insertar datos
INSERT INTO employees (id, name, married, genre) VALUES (1, 'Jeff', TRUE, 'M'); 

/*
-- Tipos de datos: boolean
*/
CREATE TABLE IF NOT EXISTS employees(
	id INT,
	married BOOLEAN
);

INSERT INTO employees (id, married) VALUES (1, TRUE);
INSERT INTO employees (id, married) VALUES (2, FALSE);

-- Tipo de dato numerico
CREATE TABLE IF NOT EXISTS employees(
	id INT,
	name VARCHAR(250),
	married BOOLEAN,
	genre CHAR(1),
	salary NUMERIC(9, 2)
);

-- Insertar datos
INSERT INTO employees (id, name, married, genre, salary) VALUES (2, 'Jeff', TRUE, 'M', 29689.23);

-- Tipo de dato: DATE
CREATE TABLE IF NOT EXISTS employees(
	id INT,
	name VARCHAR(250),
	married BOOLEAN,
	genre CHAR(1),
	salary NUMERIC(9, 2),
	birth_date DATE
);

-- Insertar datos
INSERT INTO employees (id, name, married, genre, salary, birth_date) VALUES (2, 'Jeff', TRUE, 'M', 29689.23, '2000-02-21');

-- Tipo de dato: TIME
CREATE TABLE IF NOT EXISTS employees(
	id INT,
	name VARCHAR(250),
	married BOOLEAN,
	genre CHAR(1),
	salary NUMERIC(9, 2),
	birth_date DATE,
	start_at TIME
);
INSERT INTO employees (id, name, married, genre, salary, birth_date, start_at) 
VALUES (1, 'Jeff', TRUE, 'M', 29689.23, '2000-02-21', '08:00:00');

-- Identificador autoincremental 
CREATE TABLE IF NOT EXISTS employees(
	id SERIAL,
	name VARCHAR(250),
	married BOOLEAN,
	genre CHAR(1),
	salary NUMERIC(9, 2),
	birth_date DATE,
	start_at TIME
);

INSERT INTO employees (name, married, genre, salary, birth_date, start_at) 
VALUES ('Jeff', TRUE, 'M', 29689.23, '2000-02-21', '08:00:00');

-- Verificar que todavia sigue permitiendo insertar un id duplicado
INSERT INTO employees (id, name, married, genre, salary, birth_date, start_at) 
VALUES (1, 'Jeff', TRUE, 'M', 29689.23, '2000-02-21', '08:00:00');

-- Primary key
CREATE TABLE IF NOT EXISTS employees(
	id SERIAL PRIMARY KEY,
	name VARCHAR(250),
	married BOOLEAN,
	genre CHAR(1),
	salary NUMERIC(9, 2),
	birth_date DATE,
	start_at TIME
);

INSERT INTO employees (name, married, genre, salary, birth_date, start_at) 
VALUES ('Antonio', TRUE, 'M', 29689.23, '2000-02-21', '08:00:00');

-- Verificar que ya no permite insertar id duplicado
INSERT INTO employees (id, name, married, genre, salary, birth_date, start_at) 
VALUES (1, 'Jeff', TRUE, 'M', 29689.23, '2000-02-21', '08:00:00');

-- Hacer que un campo sea oblicatorio con NOT NULL
CREATE TABLE IF NOT EXISTS employees(
	id SERIAL PRIMARY KEY,
	name VARCHAR(250) NOT NULL,
	married BOOLEAN,
	genre CHAR(1),
	salary NUMERIC(9, 2),
	birth_date DATE,
	start_at TIME
);

-- Comprobar que no deja insertar sin su respectivo nombre
INSERT INTO employees (married, genre, salary, birth_date, start_at) 
VALUES (TRUE, 'M', 29689.23, '2000-02-21', '08:00:00');

-- Hacer que un campo sea único con UNIQUE
CREATE TABLE IF NOT EXISTS employees(
	id SERIAL PRIMARY KEY,
	name VARCHAR(250) NOT NULL,
	email VARCHAR(100) UNIQUE,
	married BOOLEAN,
	genre CHAR(1),
	salary NUMERIC(9, 2),
	birth_date DATE,
	start_at TIME
);

INSERT INTO employees (name, email, married, genre, salary, birth_date, start_at) 
VALUES ('Employee1', 'Employee1@gmail.com', TRUE, 'M', 29689.23, '2000-02-21', '08:00:00');

-- Verificar que de fallo por email repetido deberia ser único
INSERT INTO employees (name, email, married, genre, salary, birth_date, start_at) 
VALUES ('Employee2', 'Employee1@gmail.com', TRUE, 'M', 29689.23, '2000-02-21', '08:00:00');

SELECT * FROM employees;

-- Restricciones en rango de tados CHECK 
CREATE TABLE IF NOT EXISTS employees(
	id SERIAL PRIMARY KEY,
	name VARCHAR(250) NOT NULL,
	email VARCHAR(100) UNIQUE,
	married BOOLEAN,
	genre CHAR(1),
	salary NUMERIC(9, 2) CHECK (salary >= 15000),
	birth_date DATE CHECK (birth_date >= '1971-05-05'),
	start_at TIME
);

INSERT INTO employees (name, email, married, genre, salary, birth_date, start_at) 
VALUES ('Employee1', 'Employee1@gmail.com', TRUE, 'M', -1, '2000-02-21', '08:00:00');

INSERT INTO employees (name, email, married, genre, salary, birth_date, start_at) 
VALUES ('Employee1', 'Employee2@gmail.com', TRUE, 'M', 16000, '1960-02-21', '08:00:00');





-- Renombrar tabla
ALTER TABLE IF EXISTS employees RENAME TO employees_2021;

-- Agregar columnas a las tablas
ALTER TABLE employees ADD COLUMN  email VARCHAR(100);

-- Barrar columnas de una tabla
ALTER TABLE employees DROP COLUMN IF EXISTS  email;

-- Ver datos de una tabla
select * from employees;

-- Borrar una tabla
DROP TABLE IF EXISTS employees;