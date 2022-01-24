<h1>AJAX + PHP + MySQL</h1>
<p>Vamos a crear una página web llamada index.html que contiene únicamente un button, un input y un div. El funcionamiento de la página será el siguiente:</p>

<ul>
    <li>Cada vez que se pulsa el botón se hará una llamada asíncrona desde el archivo script.js al archivo action.php.</li>
    <li>El archivo action.php recogerá los datos escritos en el input enviados por AJAX mediante el método POST.</li>
    <li>El archivo action.php se conectará a una base de datos dws, donde realizará una consulta sobre la tabla alumnos, filtrando a través del identificador que ha recibido por POST.</li>
    <li>El archivo action.php escribirá una tabla HTML con los datos del alumno. Dicha tabla es la que recibe AJAX de forma asíncrona.</li>
    <li>Cuando lleguen los datos, el archivo script.js escribirá dinámicamente en index.html la tabla en el contenedor.</li>
    <li>Cuando se escriba en el input la palabra Todos, se mostrará una tabla con todos los datos de la tabla alumnos.</li>
</ul>
<p>Para facilitar la tarea, partir del siguiente código fuente:</p>
<p>Archivo SQL con la creación de la base de datos y la tabla:</p>
<code>
        -- phpMyAdmin SQL Dump
        -- version 4.8.3
        -- https://www.phpmyadmin.net/
        --
        -- Host: localhost:3306
        -- Server version: 5.7.24-log
        -- PHP Version: 7.2.10
        
        SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
        SET AUTOCOMMIT = 0;
        START TRANSACTION;
        SET time_zone = "+00:00";
        
        
        /*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
        /*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
        /*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
        /*!40101 SET NAMES utf8mb4 */;
        
        --
        -- Database: `dws`
        --
        CREATE DATABASE IF NOT EXISTS `dws` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
        USE `dws`;
        
        -- --------------------------------------------------------
        
        --
        -- Table structure for table `alumnos`
        --
        
        CREATE TABLE `alumnos` (
          `idAlumno` int(11) NOT NULL,
          `nombre` varchar(20) NOT NULL,
          `apellido` varchar(20) NOT NULL,
          `nota` decimal(10,0) NOT NULL
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
        
        --
        -- Dumping data for table `alumnos`
        --
        
        INSERT INTO `alumnos` (`idAlumno`, `nombre`, `apellido`, `nota`) VALUES
        (1, 'Julio', 'Salinas', '8'),
        (2, 'Pepe', 'Pérez', '10');
        
        --
        -- Indexes for dumped tables
        --
        
        --
        -- Indexes for table `alumnos`
        --
        ALTER TABLE `alumnos`
          ADD PRIMARY KEY (`idAlumno`);
        
        --
        -- AUTO_INCREMENT for dumped tables
        --
        
        --
        -- AUTO_INCREMENT for table `alumnos`
        --
        ALTER TABLE `alumnos`
          MODIFY `idAlumno` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;
        COMMIT;
        
        /*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
        /*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
        /*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
</code>
<p>index.html:</p>
<code>
        <!DOCTYPE html>
        <html>

        <head>
            <meta charset="utf-8">
            <meta http-equiv="X-UA-Compatible" content="IE=edge">
            <title>AJAX</title>
            <meta name="viewport" content="width=device-width, initial-scale=1">
        </head>

        <body>
            <button id="boton">Cargar</button>
            <input id="input" type="text">
            <div id="contenedor"></div>
            <script src="https://code.jquery.com/jquery-3.3.1.js"></script>
            <script src="script.js"></script>
        </body>

        </html>
</code>