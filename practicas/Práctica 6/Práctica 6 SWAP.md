# Práctica 6 SWAP: Discos en RAID.

Comprobamos con la utilidad sudo fdisk -l que podemos ver las dos unidades de almacenamiento desde la máquina virtual:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%206/Imágenes/Utilidad%20sudo%20fdisk-l.png)

Creamos el RAID 1 a partir de las dos unidades de almacenamiento /dev/sdb y /dev/sdc:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%206/Imágenes/Creación%20RAID%201.png)

Creamos el sistema de ficheros del RAID:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%206/Imágenes/Creación%20sistema%20de%20ficheros.png)

Creamos el directorio donde queremos montar el RAID y lo montamos en él:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%206/Imágenes/Creación%20directorio.png)

Comprobación del estado del RAID:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%206/Imágenes/Comprobación%20RAID.png)

Comprobación del UUID del RAID:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%206/Imágenes/Comprobación%20UUID%20RAID.png)

Edición del fichero fstab para arranque automático:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%206/Imágenes/Edición%20fichero%20fstab.png)

Comprobación de que el RAID conserva los archivos a pesar de simular fallos en una de las unidades o incluso extraerlas:

![imagen](https://github.com/juliancifuentes95/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/Prácticas/Práctica%206/Imágenes/Comprobación%20RAID%20final.png)

