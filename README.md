# ExamenFinal-Pregunta2
Este proyecto configura un entorno con Docker Compose para desplegar un servidor de base de datos MySQL junto con una interfaz de administración phpMyAdmin. El entorno permite crear y gestionar una base de datos y realizar consultas fácilmente a través de phpMyAdmin.

Estructura del Proyecto docker-compose.yml: Archivo de configuración de Docker Compose para levantar los contenedores de MySQL y phpMyAdmin. init.sql: Archivo SQL para inicializar la base de datos con la creación de tres tablas (clientes, productos y pedidos). Requisitos Previos Docker y Docker Compose instalados en el sistema. Git instalado en el sistema. Configuración del Proyecto Paso 1: Crear los archivos necesarios docker-compose.yml: Archivo para configurar el entorno de Docker con dos contenedores, uno para MySQL y otro para phpMyAdmin.

versión: '3.8'

servicios: mysql: imagen: mysql:latest nombre_contenedor: mysql_server entorno: MYSQL_ROOT_PASSWORD: contraseña_raíz MYSQL_DATABASE: examen_db MYSQL_USER: usuario MYSQL_PASSWORD: contraseña_usuario puertos: - "3306:3306" volúmenes: - mysql_data:/var/lib/mysql - ./init.sql:/docker-entrypoint-initdb.d/init.sql redes: - examen_network

phpmyadmin: imagen: phpmyadmin:latest nombre_contenedor: phpmyadmin entorno: PMA_HOST: mysql PMA_USER: root PMA_PASSWORD: rootpassword puertos: - "8080:80" redes: - examen_network

CREATE DATABASE tienda;
USE tienda;

CREATE TABLE clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    telefono VARCHAR(15)
);

CREATE TABLE productos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    descripcion TEXT,
    precio DECIMAL(10, 2) NOT NULL,
    stock INT NOT NULL
);

CREATE TABLE pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT,
    fecha DATETIME DEFAULT CURRENT_TIMESTAMP,
    total DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES clientes(id)
);


Inicializar repositorio de Git en el proyecto:

git init git agregar. 

git commit -m "firs commit" Conecta el repositorio a GitHub y sube los archivos:

git remoto agregar origen https://github.com/SeanNina/ExamenFinal-Pregunta2 

git push -u origin master Cómo Ejecutar el Proyecto Clona el repositorio:

git clone https://github.com/SeanNina/ExamenFinal-Pregunta2 

cd C:\Users\Vic_S\Desktop\Ej2 - Inicia los contenedores con Docker Compose:

docker-compose up -d Accede a phpMyAdmin en tu navegador en http://localhost:8080 e ingresa las credenciales:

Servidor: mysql Usuario: root Contraseña: ucatec
