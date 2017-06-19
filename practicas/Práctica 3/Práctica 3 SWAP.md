# Práctica 3 SWAP: Balanceo de Carga.
Edición del fichero de configuración nginx:

![Imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%203/Imágenes/Configuración%20nginx.png)

El balanceador de carga va seleccionando entre realizar la petición a la máquina 1 con el fichero editado y la palabra **"MAQUINA1"** al final del head, y la máquina 2, con la palabra **"MAQUINA2"**.

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%203/Imágenes/Balanceador%20de%20carga.png)

Peticiones desde M4 hacia M3, que ejecuta haproxy para las máquinas M1 y M2:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%203/Imágenes/Peticiones.png)

Ejecución de ab -n 1000 -c 10 http://10.0.2.5/index.html sobre la máquina con haproxy:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%203/Imágenes/Ejecución.png)

ab contra la máquina con nginx:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%203/Imágenes/AB%20nginx.png)

Contra haproxy prueba 2 (la definitiva quizás):

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%203/Imágenes/Haproxy.png)

## Parte Opcional: 

Instalación de lighttpd.

		apt install lighttpd

Configuración lighttpd.conf:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%203/Imágenes/Configuración%20lighttpd.png)

Como podemos ver, con el servicio lighttpd corriendo con la configuración realizada, podemos obtener la página web de las dos máquinas de manera alternativa:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%203/Imágenes/Web%20dos%20máquinas.png)

