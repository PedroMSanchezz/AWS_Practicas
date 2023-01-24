
IMPLANTACIÓN DE APLICACIONES WEB
# PRÁCTICA 4.2 Instalar Wordpress en una arquitectura de tres niveles. PARTE 2
![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.001.png)



# Índice
-----
[**PRÁCTICA 4.2 Instalar Wordpress en una arquitectura de tres niveles.**](#_t407xxhvh3jg)	

[**Índice**](#_9fb30wxk007a)	

Arquitectura del ejercicio	

Fases de la práctica	

Infraestructura y software	

Infraestructura	

Software	

EC2 servidor Web	

EC2 servidor Proxy	

Creación EC2 con servidor Web	

Creación de la EC2 proxy	

Comprobación balanceo de carga	
##
Fase 2. Instalación NFS Server

Una vez terminada la fase 2 hasta el proceso del balanceador de cargas terminado en la práctica anterior [Practica 4.2](Practica4.2_Arquitectura_de_3_niveles_Parte1_PedroS.md), empezaremos con la instalación del NFS Server.

**¿Qué es NFS?**

NFS es un protocolo de nivel de aplicación, según el Modelo OSI. Es utilizado para sistemas de archivos distribuidos en un entorno de red de computadoras de área local. Posibilita que distintos sistemas conectados a una misma red accedan a ficheros remotos como si se tratara de locales.

#### **Creación y configuración NFS**

Creamos una nueva instancia EC2 que aloja el servicio NFS, en dicha instalación añadiremos una nueva regla de entrada que es del propio puerto NFS.

Regla de entrada

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.002.png)



Una vez entramos por consola en nuestro servidor de NFS, instalaremos el servicio NFS.

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.003.png)



Cuando termine la instalación del nfs server, crearemos un directorio que será el host de los contenidos que se van a compartir.

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.004.png)


Tras la instalación del paquete de nfs, modificaremos un fichero llamado /etc/exports.

En dicho fichero añadiremos las entradas que van a exportar nuestro directorio de wordpress que va a actuar de host.

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.005.png)

En dichas entradas, se le añadirá la ruta del host (que hemos creado) con la IP privada de cada instancia que actúa como servidor Web.

Tras guardar el fichero, haremos el siguiente comando para comprobar que se ha guardado correctamente y actuará de host cogiendo el contenido de las siguientes IP’s.

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.006.png)


### Creación del punto de montaje en el cliente NFS

En cada uno de los clientes, crearemos un punto de montaje en el directorio que actuará de host de nuestro servidor NFS.

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.007.png)

Para comprobar que se ha montado correctamente el punto de montaje se verificará con el siguiente comando.

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.008.png)


### Editar el archivo /etc/fstab en el cliente NFS

Editamos el archivo /etc/fstab para que al iniciar la máquina se monte automáticamente el directorio compartido por NFS.

Añadimos la siguiente línea:

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.009.png)

### Instalación WP en servidor NFS

Una vez terminados los pasos anteriores, instalaremos WordPress en nuestro servidor de NFS, ya que al actuar como host todo lo que modifiquemos en los archivos de /var/www/html de nuestro host se modificarán automáticamente en las instancias EC2 de servidores Web.



Para la instalación de wordpress haremos los mismos pasos que en las prácticas anteriores y una vez terminada su instalación comprobamos que funciona correctamente.

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.010.png)

Además comprobamos que nuestro wordpress balancea correctamente, por lo que nos vamos al balancer-manager y verificamos que funciona correctamente.

![](prac4.2_v2_img/Aspose.Words.0103bbb6-9652-45ca-8d10-81ca31d8d07f.011.png)


### Webgrafía

<https://github.com/PedroMSanchezz/AWS_Practicas.git>

