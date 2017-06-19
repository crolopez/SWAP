# Práctica 5 SWAP: Replicación de bases de datos MySQL.

- En primer lugar, creamos la Base de Datos mediante los siguientes comandos en la terminal de SQL:

		CREATE DATABASE PracticasSWAP;
		USE PracticasSWAP;

- Ahora creamos una tabla para la base de datos creada anteriormente:

		CREATE TABLE Prueba();
		
- Posteriormente, hacemos una copia de seguridad de nuestra base de datos completa haciendo uso de mysqldump. Para ello, accedemos a la base de datos y bloqueamos las tablas que haya, seguido de esto, salimos y volvemos a acceder por segunda vez a la BD y por último desbloqueamos las tablas.

- Después, restauramos la copia de seguridad que hemos hecho anteriormente en la segunda máquina virtual.

- Por último, realizamos la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.

			

