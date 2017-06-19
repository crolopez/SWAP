# Práctica 2 SWAP: Clonar la información de un sitio web.

- En primer lugar, hacemos un ejemplo copiando un archivo mediante ssh desde la máquina virtual principal.
- Posteriormente, clonamos una carpeta entre las dos máquinas virtuales.
- Después, configuramos ssh de tal forma que no se nos solicite contraseña cuando queramos acceder.
- Por último, establecemos una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas virtuales de las que disponemos.

Para esta última tarea, será necesario que ejecutemos el siguiente comando en la terminal:

	crontab -e
	
y después reiniciamos el servicio cron. Posteriormente, cuando transcurra una hora, la tarea se volverá a ejecutar de forma sucesiva cada vez que pase ese tiempo.	
	









