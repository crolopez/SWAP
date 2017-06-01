# Trabajo realizado por:
## [Julián Cifuentes Jiménez](https://github.com/juliancifuentes95)
## [José Álvaro Garrido López](https://github.com/alvarospunk)
##  [Alejandro Francisco Alguacil Camarero](https://github.com/alguacilaguamara)
##  [Alejandro Manuel do Nascimento Rodríguez](https://github.com/donas11)


# Introducción

Nuestro trabajo consiste en recrear las prácticas de la asignatura en un servidor casero, con el objetivo de observar a ras de circuito la importancia y el funcionamiento de las herramientas que hemos utilizado en el curso.

Para ello, hemos puesto a punto cuatro máquinas, las cuales tendrán como fin aunar potencia de cómputo y memoria para procesar las peticiones que lleguen al mismo. Una de estas máquinas será el balanceador de carga, el cual se encargará de repartir el grueso de las peticiones entre las máquinas preparadas para tal efecto. Todas ellas vendrán provistas de unos cuantos servidores web (apache) y una base de datos (MariaDB), utilizando como motor de virtualización los contenedores de Docker, intentando sacarle el máximo jugo a esta útil herramienta. Posteriormente entraremos en más detalles sobre la puesta a punto de los servidores y la configuración que hemos tenido que realizar sobre los mismos.

Para ello vamos a utilizar Docker.

# ¿Qué es Docker?

Docker es una plataforma de software que le permite crear, probar e implementar aplicaciones rápidamente. Docker empaqueta software en unidades estandarizadas llamadas
contenedores que incluyen todo lo necesario para que el software se ejecute, incluidas bibliotecas, herramientas de sistema, código y tiempo de ejecución. Con Docker, puede implementar y ajustar la escala de aplicaciones rápidamente en cualquier entorno con la certeza de saber que su código se ejecutará.


# Ventajas de Docker

Mejore la productividad de desarrollo Docker reduce el tiempo empleado en configurar nuevos entornos o en solucionar los problemas asociados con el uso de entornos diferentes. Estandarice las operaciones de aplicaciones Las aplicaciones con contenedores facilitan la implementación, la identificación de problemas y el retorno a una fase anterior para remediarlos.


# Empresas que lo Utilizan

Organizaciones contribuidoras apuestan por Docker:
* Red Hat
* IBM 
* Google por ejemplo con Google Container Engine y Kubernetes 
* NETFLIX utiliza a nivel muy bajo contenedores dockers en sus servidores de Amazon EC2 Container Service ya que este proporciona soporte técnico para Docker
* HPE - Composable Infrastructure Partner Program
* ADP
* Paypal
* 

# Configuraciones iniciales que desechamos
## Ideas iniciales: conexiones de dispositivos 
### Idea principal
La idea principal para dar el servicio del servidor fue conectar todos los ordenadores y configurar alguno de los routers secundarios que tuviesemos en desuso y configurarlo para que emitiese ua red wifi conectando todos nuestros portatiles por cable, razones por las que se descarto:

* los routers que teniamos no permitian hacer la configuración o teniamos que modificar partes del hardware soldando algunas conexiones.
* las conexiones de uno de los portatil necesitaba un adaptador de conexiones(usb-c) a red(Gigabit Ethernet) que costaba uns 33€, esto se solucionaba conectandolo por wifi

![img](./imagenes/con1.png)


### Segunda idea
Descartando la anterior idea, escogimos optar por una mejora de la anterior la cual fue conectar todos los ordenadores al router y desde el ordenador balanceador de carga que era por el que tendrían que acceder al servicio y montar con una tarjeta wifi interna del portatil o externa(con esta opción se dispondría de acceso a internet) emitiendo una red wifi, los motivos por que la desechamos:

* La prueba que realizamos en clase funciono bien, excepto a una persona con un móvil pero el sistema en si funciono decentemente
* se intento crear un servidor con DNS local para facilitar el acceso y no tener que dar una IP, pero no se obtubieron resultados

![img](./imagenes/con2.png)

### Últimas ideas
Concluimos después de las ideas anteriores era mejor tener una direccion en vez de una IP y por eso discutimos entre las dos siguientes posiciones:

* dejar todos los ordenadores en red en una de nuestra casas
* dejar distribuidos los equipos en cada casa con cada uno de nuestro ISP(Internet Service Provider)

de las que decidimos optar por la distribuirl
os y configurarlos con No-ip para tener una dirección en vez de una IP

![img](./imagenes/con3.png)

## Ideas iniciales: conexiones de contenedores 

# Máquina Julián

~~~
sudo docker run -d -p 1111:80 -p 1112:22 -p 1113:443 -p 1114:3306 -i -t --name ApacheTrabajo1 ubuntu bash
~~~

<table cellspacing="0" border="0">
	<colgroup width="92"></colgroup>
	<colgroup width="128"></colgroup>
	<colgroup width="85"></colgroup>
	<tr>
		<td height="17" align="center"><b>Puertos Host</b></td>
		<td align="center"><b>Puertos contenedor</b></td>
		<td align="center"><b>Utilizado para</b></td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1111" sdnum="3082;">1111</td>
		<td align="center" sdval="80" sdnum="3082;">80</td>
		<td align="center">HTTP</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1112" sdnum="3082;">1112</td>
		<td align="center" sdval="22" sdnum="3082;">22</td>
		<td align="center">SSH</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1113" sdnum="3082;">1113</td>
		<td align="center" sdval="443" sdnum="3082;">443</td>
		<td align="center">HTTPS</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1114" sdnum="3082;">1114</td>
		<td align="center" sdval="3306" sdnum="3082;">3306</td>
		<td align="center">MySQL</td>
	</tr>
</table>

~~~
apt-get update
~~~
~~~
apt-get install apache2 php libapache2-mod-php php-mysql
~~~
~~~
apt-get install openssh-server openssh-client
~~~
~~~
apt-get install rsync 
~~~
~~~
apt-get install cron
~~~

~~~
sudo docker export --output=ApacheTrabajo.tar ApacheTrabajo
~~~

~~~
sudo docker images
~~~

~~~
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
<none>					<none>				ce51d2645415		3 seconds ago		302.6 MB
~~~

~~~
sudo docker run -d -p 1115:80 -p 1116:22 -p 1117:443 -p 1118:3306 -i -t --name ApacheTrabajo2 ce51d2645415 bash
~~~

<table cellspacing="0" border="0">
	<colgroup span="3" width="85"></colgroup>
	<tr>
		<td height="17" align="center"><b>Puertos Host</b></td>
		<td align="center"><b>Puertos contenedor</b></td>
		<td align="center"><b>Utilizado para</b></td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1115" sdnum="3082;">1115</td>
		<td align="center" sdval="80" sdnum="3082;">80</td>
		<td align="center">HTTP</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1116" sdnum="3082;">1116</td>
		<td align="center" sdval="22" sdnum="3082;">22</td>
		<td align="center">SSH</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1117" sdnum="3082;">1117</td>
		<td align="center" sdval="443" sdnum="3082;">443</td>
		<td align="center">HTTPS</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1118" sdnum="3082;">1118</td>
		<td align="center" sdval="3306" sdnum="3082;">3306</td>
		<td align="center">MySQL</td>
	</tr>
</table>

~~~
sudo docker run -d -p 1119:80 -p 1120:22 -p 1121:443 -p 1122:3306 -i -t --name ApacheTrabajo3 ce51d2645415 bash
~~~

<table cellspacing="0" border="0">
	<colgroup span="3" width="85"></colgroup>
	<tr>
		<td height="17" align="center"><b>Puertos Host</b></td>
		<td align="center"><b>Puertos contenedor</b></td>
		<td align="center"><b>Utilizado para</b></td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1119" sdnum="3082;">1119</td>
		<td align="center" sdval="80" sdnum="3082;">80</td>
		<td align="center">HTTP</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1120" sdnum="3082;">1120</td>
		<td align="center" sdval="22" sdnum="3082;">22</td>
		<td align="center">SSH</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1121" sdnum="3082;">1121</td>
		<td align="center" sdval="443" sdnum="3082;">443</td>
		<td align="center">HTTPS</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1122" sdnum="3082;">1122</td>
		<td align="center" sdval="3306" sdnum="3082;">3306</td>
		<td align="center">MySQL</td>
	</tr>
</table>

~~~
sudo docker run -d -p 1123:80 -p 1124:22 -p 1125:443 -p 1126:3306 -i -t --name ApacheTrabajo3 ce51d2645415 bash
~~~

<table cellspacing="0" border="0">
	<colgroup span="3" width="85"></colgroup>
	<tr>
		<td height="17" align="center"><b>Puertos Host</b></td>
		<td align="center"><b>Puertos contenedor</b></td>
		<td align="center"><b>Utilizado para</b></td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1119" sdnum="3082;">1123</td>
		<td align="center" sdval="80" sdnum="3082;">80</td>
		<td align="center">HTTP</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1120" sdnum="3082;">1124</td>
		<td align="center" sdval="22" sdnum="3082;">22</td>
		<td align="center">SSH</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1121" sdnum="3082;">1125</td>
		<td align="center" sdval="443" sdnum="3082;">443</td>
		<td align="center">HTTPS</td>
	</tr>
	<tr>
		<td height="17" align="center" sdval="1122" sdnum="3082;">1126</td>
		<td align="center" sdval="3306" sdnum="3082;">3306</td>
		<td align="center">MySQL</td>
	</tr>
</table>




##Configuarción SSH copia automática
Creamos la clave
~~~
keygen -t rsa
~~~

La copiamos en la maquina principal de nuestros contenedores
~~~
ssh# ssh-copy-id -i ~/.ssh/id_rsa 172.17.0.2
~~~

# Máquina Donas

# 
## Descripción
El objetivo de esta página web es gestionar la entrada y salida de usuarios registrados, guardar datos de aspectos tecnicos del servidor y del cliente, y ver porcentajes sobre los datos guardados

## Objetivos
* El sistema almacenara datos
* El sistema mostrara datos de una forma visual
* El sistema permitira acceder mediante usuario y contraseña
* El sistema permitira salir 

## Descripción de los implicados
### Entorno de usuario
Los	 usuarios directos de la aplicación a desarrollar es el usuario registrado que dispone de todas las opciones de la pagina web

### Resumen de los implicados

<table border="0" cellspacing="0" cellpadding="0" class="ta1"><colgroup><col width="134"/><col width="194"/><col width="99"/><col width="99"/></colgroup><tr class="ro1"><td style="text-align:left;width:30.76mm; " class="ce3"><p>Nombre</p></td><td style="text-align:left;width:44.38mm; " class="ce3"><p>Descripción </p></td><td style="text-align:left;width:22.58mm; " class="ce3"><p>Tipo</p></td><td style="text-align:left;width:22.58mm; " class="ce3"><p>Responsabilidad</p></td></tr><tr class="ro1"><td style="text-align:left;width:30.76mm; " class="Default"><p>Usuario registrado </p></td><td style="text-align:left;width:44.38mm; " class="Default"><p>Representa un usuario registrado</p></td><td style="text-align:left;width:22.58mm; " class="Default"><p>Usuario del sistema</p></td><td style="text-align:left;width:22.58mm; " class="Default"><p>Iniciar sesión, cerrar sesión, guardar datos y visualizar porcentajes</p></td></tr></table>

### Criterios de Exito
* Usuario registrado: Que el sistema le permita utilizar la navegación de forma sencilla y rápida. 


### Requisitos Funcionales
* **RF-1. Iniciar sesión** El sistema realizará una consulta 
	* RF-1.1. El sistema sera capaz de responder al entrar
* **RF-2. Guardar Datos** El sistema guardará los datos
	* RF-1.1. El sistema será capaz de almacenar los datos
* **RF-3. ver estadisticas** El sistema mostrará los datos
	* RF-1.1. El sistema sera capaz de mostrar porcentajes de datos guardados
* **RF-4. Cerrar sesión** El sistema eliminará los datos 
	* RF-1.1. El sistema borrara todos los datos utilizados en la sesión 

### Requisitos No Funcionales
* **RNF1** Es necesario de conocimientos iniciales de navegación por web
* **RNF2** No es necesario documentación al usuario
* **RNF3** Es necesario la utilización de un navegador de internet
* **RNF4** El sistema debe ser estable y escalable
* **RNF5** El sistema debe soportar un número indefinido de usuarios
simultáneamente
* **RNF6** El sistema debe de ser veloz y con los mínimos tiempos de
carga posibles.


### Requisitos de Información
* ** RI1 Iniciar Sesion**
	* Imformación de usuario 
	* **Contenido:** un usuario esta identificado por su usuario y la contraseña  
	* **Requisitos asociados:** RF-1, RF-2,RF-3,RF-4

* ** RI2 Datos**
	* Información del servidor y del cliente
	* **Contenido:** Información destinada para guardar direcciones IP, Sistemas operativos, Navegadores tamaños de pantalla y usuario
	* **Requisitos asociados:**RF2,RF3



## Diagramas

### Diagramas de caso de uso
![img](./imagenes/Casosdeuso.png)


### Descripción de los casos de usos

### Descripción de los actores

### Descripción Extendida de los Casos de Uso

### Glosario de términos extendido

###Modelo Conceptual

### Diagramas de Secuencia

### iniciar sesión

### Diagrama de clases del diseño

# Máquina Álvaro

## Importamos el contenedor que exportamos
~~~
sudo docker import ApacheTrabajo.tar
~~~

## lo buscamos entre las imagenes
~~~
sudo docker images
~~~

~~~
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
<none>					<none>				ce51d2645415		3 seconds ago		302.6 MB
~~~

## Arrancamos un contenedor con la imagen importada
~~~
sudo docker run -d -p 1111:80 -p 1112:22 -p 1113:443 -p 1114:3306 -i -t --name ApacheTrabajo ce51d2645415 bash
~~~
### Creamos otro contenedor
~~~
sudo docker run -d -p 1115:80 -p 1116:22 -p 1117:443 -p 1118:3306 -i -t --name ApacheTrabajo2 ce51d2645415 bash
~~~
## Preparamos el sistema montando los dispositivos para conectarlos en RAID

Montamos nuestros dos dispositivos de almacenamiento
~~~
sudo mkdir/run/media/alvarogl/swap1
sudo mkdir/run/media/alvarogl/swap2
sudo mount /dev/sdb1 /run/media/alvarogl/swap1/
sudo mount /dev/sdb2 /run/media/alvarogl/swap2/
~~~
![img](./imagenes/RAID1-5.png)
creamos, arrancamos contenedor docker y accedemos
~~~
sudo docker run --nam=apache_raid --privileged -d -p 1111:80 -p 1112:443 -p 1113:22  --device /dev/sdb1/:/dev/sdb  --device /dev/sdb1/:/dev/sdc -it 11d359dad1c2 bash
sudo docker attach apache_raid
~~~
![img](./imagenes/RAID1-4.png)

comprobamos los dispositivos de almacenamiento
~~~
fdisk -l
~~~
![img](./imagenes/RAID1-1.png)
~~~
mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb1 /dev/sdb2
mkfs /dev/md0
~~~

![img](./imagenes/RAID1-3.png)


~~~
mdadm --detail /dev/md0
~~~
![img](./imagenes/RAID1-0.png)


configuramos el archivo /etc/fstab

~~~
UUID=1ee1f774:c5d0c62d:dc01f0cf:98c776a8 /dat ext2 defaults 0 0
~~~
![img](./imagenes/RAID1-2.png)


# Máquina Alejandro


## Creamos un nuevo contenedor

~~~
sudo docker run -d -p 80:80 -p 443:443 -p 10022:22 -i -t --name BalanceadorTrabajo nginx bash
~~~

## accedemos a el

~~~
sudo docker attach BalanceadorTrabajo
~~~

## modificamos archivo /etc/nginx/conf.d/default.conf

~~~
upstream apaches {
    	ip_hash;
    	server alvarospunk.ddns.net:1217;
    	server juliansito.ddns.net:1113;
    	server juliansito.ddns.net:1117;
    	server juliansito.ddns.net:1121;
    	server donas11.hopto.org:1113;
    	server donas11.hopto.org:1117;
    	server donas11.hopto.org:1121;
    	server juliansito.ddns.net:1125;
	}
server{
    	listen 80;
     	listen 443 ssl;
     	ssl on;
     	ssl_certificate    	/tmp/apache.crt;
     	ssl_certificate_key	/tmp/apache.key;
    	server_name balanceador;
    	access_log /var/log/nginx/balanceador.access.log;
    	error_log /var/log/nginx/balanceador.error.log;
    	root /var/www/;
    	location /
    	{
            	proxy_pass https://apaches;
            	proxy_set_header Host $host;
            	proxy_set_header X-Real-IP $remote_addr;
            	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            	proxy_http_version 1.1;
            	proxy_set_header Connection "";
    	}
}
~~~

## reiniciamos servicio

~~~
service nginx restart
~~~

# Anécdotas

# Hemos roto un Router
* Justo antes de reiniciar de HAPROXY el router desconecta la Wifi
* Creemos que era por que se habia calentado por estar colocado verticalmente cuando su forma correcta es horizontal

# Se actualiza el sistema operativo en el último día antes de la exposición
* Un integrante del grupo se había actualizado el sistema operativo de OpenSuse y la noche anterior le habia pasado un kernel panic, pero seguía funcionando, pues al día siguiente no se pueden ejecutar algunos comando, y tampoco iniciar los contenedores de docker que se tenian nos da un error, esto pasa en la hora de prácticas bueno vamos a ver si en casa intentamos solucionarlo

![img](./imagenes/1.jpg)



* estando haciendo pruebas y más intentando tener otras opciones por si fallan los principales ordenadores, se une compañero que venía de hacer un examen  prueba arrancar docker en su maquína con Antergos y se encuentra con errores tambien
![img](./imagenes/2.jpg)
![img](./imagenes/2-1.jpg)
![img](./imagenes/3.jpg)



* Mientras que mis compañeros preguntan en el grupo de Telegram de Docker ES por si alguno de sus miembros le ha ocurrido para poder dar solución a esos errores  rezo para que a mi no me pase , y empiezo a crear copias de seguridad por si, ocurriese algo, crucemos los dedos sin dejar de teclear

* Despues de un rato los errores del segundo compañero se consiguen solucionar con una actulización y un reboot

* Parece que con la gente del grupo de Telegram Docker ES consiguén ayudar a mi compañero y una propuesta es que copia las carpetas que contienen los contenedores 
en la carpeta /var/lib/docker
~~~
du -sh /var/lib/docker
~~~
desinstala docker completo aunque el paso más importante fue borrar el subvolumen del btrfs que parecia que es lo que estaba acaparando todo
~~~
btrfs subvolume delete /var/lib/docker/btrfs/subvolumes/*
~~~
intenta copiar la carpeta de vuelta a docker de nuevo instalado y:

Se queda sin espacio en disco 

![img](./imagenes/5.jpg)

intentos de copiar archivos desde terminal

![img](./imagenes/6.jpg)



___
***
- - -
1. [IBM-Docker](https://www.docker.com/ibm)
2. [Qué es Docker - Red hat](https://www.redhat.com/es/containers/what-is-docker)
3. [Google-Docker](https://cloud.google.com/container-engine/)
4. [Amazon Web services -Docker](https://aws.amazon.com/es/docker/)
5. [Empresas que utilizan Docker](https://www.docker.com/customers)
6. [AWS -Netflix](https://aws.amazon.com/es/solutions/case-studies/netflix/)
7. [Securing Containers the Netflix Way](https://speakerdeck.com/bdpayne/securing-containers-the-netflix-way)
8. [Netflix and containers not a stranger thing](https://es.slideshare.net/aspyker/netflix-and-containers-not-a-stranger-thing)
9. [Deploying Docker Containers with Netflix Spinnaker on Kubernetes and Titus](https://www.youtube.com/watch?v=ySdqDGfEOHo)
10. [AWS-Docker](https://aws.amazon.com/es/getting-started/tutorials/deploy-docker-containers/)
11. [AWS-Docker-EC2 Container Service](https://aws.amazon.com/es/ecs/)
12. [Spinnaker](http://www.spinnaker.io/docs/frequently-asked-questions)
13. [HPE-Docker](http://h22168.www2.hpe.com/us/en/partners/docker/)




