# Práctica 4 SWAP: Asegurar la granja web.

Acceso a la página web con certificado SSL, como es un certificado autofirmado, el navegador nos notifica la posible inseguridad del mismo:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%204/Imágenes/Acceso%20certificado%20SSL.png)

Acceso a la página web:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%204/Imágenes/Acceso%20página%20web.png)

Ejemplo de bloqueo de acceso a una determinada página web:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%204/Imágenes/Bloqueo%20de%20acceso.png)

Edición del fichero rc.local para configuración de iptables:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%204/Imágenes/Edición%20del%20fichero%20rc.local.png)

Si comentamos las reglas que habilitan el tráfico de entrada y salida por el puerto https <insertar dichas reglas> no podemos acceder a la página web desde otra máquina:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%204/Imágenes/Reglas.png)

Cuando reactivamos las reglas podemos acceder sin problema <insertar aquí reglas>:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%204/Imágenes/Reactivación%20de%20reglas.png)



