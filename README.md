-- script_crear_db.sql
CREATE DATABASE IF NOT EXISTS sistema_funcionarios CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE sistema_funcionarios;

-- Tabla cargo
CREATE TABLE IF NOT EXISTS cargo (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
);

-- Tabla dependencia
CREATE TABLE IF NOT EXISTS dependencia (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(150) NOT NULL
);

-- Tabla funcionario
CREATE TABLE IF NOT EXISTS funcionario (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  apellido VARCHAR(100) NOT NULL,
  documento VARCHAR(50) NOT NULL UNIQUE,
  email VARCHAR(150),
  telefono VARCHAR(50),
  cargo_id INT,
  dependencia_id INT,
  fecha_ingreso DATE,
  FOREIGN KEY (cargo_id) REFERENCES cargo(id) ON DELETE SET NULL,
  FOREIGN KEY (dependencia_id) REFERENCES dependencia(id) ON DELETE SET NULL
);

-- Poblado básico
INSERT INTO cargo (nombre) VALUES ('Administrador'), ('Bibliotecario'), ('Auxiliar'), ('Coordinador');
INSERT INTO dependencia (nombre) VALUES ('Dirección'), ('Servicios'), ('Atención al usuario'), ('Mantenimiento');

INSERT INTO funcionario (nombre, apellido, documento, email, telefono, cargo_id, dependencia_id, fecha_ingreso)
VALUES
('Ana', 'García', '100200300', 'ana.garcia@example.com', '3001112222', 2, 3, '2021-03-10'),
('Juan', 'Pérez', '100300400', 'juan.perez@example.com', '3003334444', 1, 1, '2019-07-01'),
('María', 'López', '100400500', 'maria.lopez@example.com', '3005556666', 3, 2, '2022-11-15');
