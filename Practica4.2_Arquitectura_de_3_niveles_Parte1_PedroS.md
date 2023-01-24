IMPLANTACIÓN DE APLICACIONES WEB
# PRÁCTICA 4.2 Instalar Wordpress en una arquitectura de tres niveles.
![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.001.png)



# Índice
-----
[PRÁCTICA 4.2 Instalar Wordpress en una arquitectura de tres niveles.**](#_t407xxhvh3jg)	

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
## Arquitectura del ejercicio
Para hacer el siguiente ejercicio debemos de crear en la siguiente arquitectura:

![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.002.png)
##
## Fases de la práctica
` `La práctica se compone de las siguientes fases 
### Fase1 : Instalación de wordpress en un nivel 
### Fase2 : Instalación de wordpress en dos niveles web 
(En la fase 1 y 2 ya lo hemos creado gracias al siguiente documento.) 
### Fase3 : Instalación de wordpress en tres niveles (balanceador, web, nfs y mysql) 
La fase 3 es la que vamos a hacer en este documento. 








## Infraestructura y software 
Procederemos a detallar y especificar nuestras máquinas que hemos utilizado para la práctica.


### Infraestructura 

Para las instancias EC2 dispondremos de las siguiente configuración de la instancia, configuración de red, reglas de entrada :
- #### Configuración de la instancia:

    1. Ubuntu 20.04 (Capa gratuita).

    2. t2.micro 1 vCPU

    3. RAM: 1Gb. 

- #### Configuración de la red:

    Permite el tráfico de los puertos 22 (SSH) y 80 (HTTP), el puerto 443 no se utilizará en dicha práctica.

- #### Reglas de entrada:

**EC2 con servidor Web**

![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.003.png)

Para los servidores web con el apache y wordpress, utilizaremos la privada del servidor proxy, para que solo se pueda acceder desde dicho servidor.

**Servidor RDS**

![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.004.png)

Para el servidor RDS, utilizaremos las IP 's privadas de nuestros servidores Web apache, donde se encuentra el Wordpress, para securizarlo.

**EC2 con servidor Proxy**

![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.005.png)

Para el servidor proxy, utilizaremos los puertos 22 (SSH) y 80 (HTTP) con IP 0.0.0.0/0 para que pueda acceder todo el mundo (ya que es la que van a ver los “clientes”)

## Software

A continuación se explicarán los paquetes que se han instalado en cada una de las EC2, tanto del servidor web, como del proxy y la configuración de dicho software.


#### EC2 servidor Web
En las instancias que actúan como servidores web, se han instalado los siguientes paquetes:

- Apache 
- PHP
- Wordpress




#### EC2 servidor Proxy

En la instancia que actúa como servidor proxy, se instalará los paquetes de:

- Apache 
- PHP
- Módulos a2enmod

Además realizaremos un script para activar todos los módulos a2enmod necesarios.

![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.006.png)

### Creación EC2 con servidor Web

Crearemos una nueva instancia EC2 que actuará como un servidor web de la capa front-end. Dicha instancia tendrá la misma configuración que la EC2 realizada en la práctica anterior de instalación de Wordpress de 2 niveles. 

[**Instalación Wordpress**](InstalacionWordPress_AWS.pdf)


### Creación de la EC2 proxy

Para la creación del servidor proxy, instalaremos los paquetes que se han mencionado en los puntos anteriores y activamos el módulo de proxy y proxy\_http.

![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.007.png)

Una vez activados los módulos deberemos de modificar el archivo de configuración de apache, para que actúe como balanceador de carga.

El archivo de configuración se encuentra en /etc/apache2/sites-enabled/000-default.conf y debemos de añadir las siguientes líneas;

![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.008.png)

Se añadirán todos los BalancerMember necesarios/creados en nuestro AWS que actúen como servidores web.


### Balanceador de carga

El **balanceador de carga** distribuye el tráfico entrante entre varios destinos, como instancias Amazon EC2. Esto aumenta la disponibilidad de la aplicación. Puede agregar uno o varios agentes de escucha al balanceador de carga.

Un agente de escucha comprueba las solicitudes de conexión de los clientes, utilizando el protocolo y el puerto configurados, y reenvía las solicitudes a un grupo de destino.

Para comprobar que nuestro servidor proxy actúa adecuadamente como balanceador de cargas, utilizaremos el buscador de internet e insertamos nuestra IP del servidor proxy.

` `![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.009.png)

Una vez comprobado que nos va a nuestro WP creado en los servidores web, veremos el balanceo de carga en la siguiente dirección y comprobamos que balancea correctamente.

![](prac4.2_v1_img/Aspose.Words.b5707927-b63a-4695-af9a-bd9d6838bcf2.010.png)

[Pedro María Sánchez Moscoso](mailto:a21samope@iesgrancapitan.org)


