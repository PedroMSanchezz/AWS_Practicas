IMPLANTACIÓN DE APLICACIONES WEB
# PRÁCTICA 4.5 Finalizar escenario cluster



![](./prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.001.png)



# Índice
-----
[**PRÁCTICA 4.5 Finalizar escenario cluster](#_t407xxhvh3jg)	

[**Índice](#_9fb30wxk007a)	

[Finalización página Web](#_127szxsjjynw)	

[Creación Base de Datos Donativos](#_pbmqxsbmhrh1)	

[Conectar base de datos con página web](#_k20meanjrze5)	

[Instalación de PHP en EC2 Linux](#_i4r9a38p7bzo)	

[Últimos pasos](#_j1foptmco08m)	

[Resultado final de la página web](#_gsh0ednnsfko)	

[Cosas a tener en cuenta](#_gife70u3xpon)	
##
## Finalización página Web

Para la finalización de dicha página web, crearemos diversos archivos en los que navegaremos por nuestra página web de las películas de netflix y en las que añadiremos apartados para la donación a la gente de Siria y Turquía por las catástrofes naturales que ha sufrido esta última semana.

Principalmente modificaremos nuestro index.html, y le añadiremos un a href para nombra la página de las donaciones.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.002.png)

De esta forma una vez guardemos nuestro archivo, al recargar la página veremos este nuevo apartado en nuestra página principal.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.003.png)



Tras la modificación del archivo anterior, crearemos una nueva página (para los donativos) que será un formulario y dicho formulario tendrá los valores que pondremos en nuestra base de datos y el nombre del archivo será formulario.php ya que lo hemos referenciado en el href del index.html.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.004.png)

Una vez terminemos, guardamos el archivo y comprobamos que funciona correctamente.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.005.png)

## Creación Base de Datos Donativos

Tras finalizar, la creación del formulario y conocer cómo hemos llamado a los valores, crearemos nuestras tablas en la base de datos.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.006.png)


## Conectar base de datos con página web

Para que nuestra BD se conecte con los valores que se van a insertar en nuestra página de formulario, debemos crear el siguiente archivo php y añadirle los valores de la BD.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.007.png)

Seguidamente, creamos otro archivo php, a este lo llamaremos grabar.php, este actuará como finalización de la página, es decir, una vez hayamos “donado algo” nos saldrá una página web dándonos las gracias y un enlace a nuestra página principal.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.008.png)

Una vez hayamos finalizado todos estos procesos, comprobaremos si funciona correctamente.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.009.png)

Podrá haber dos posibles casos, funciona correctamente o nos saldrá el siguiente error.

Este error se debe a que no tenemos instalado php en nuestra instancia EC2 de Linux, por lo que el siguiente paso es instalar los paquetes de php.


## Instalación de PHP en EC2 Linux

Procederemos a hacer los pasos que se encuentran en la siguiente página web;

<https://arstech.net/install-php-7-on-amazon-linux-2/>

- Paso 1: Realizamos un update.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.010.png)

- Paso 2: Instalamos los módulos de php.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.011.png)

- Paso 3: Instalamos los módulos que nos indican.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.011.png)


- Paso 4: Reiniciar el servicio de httpd

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.012.png)

- Paso 5: Realizar el mismo procedimiento en la otra EC2 Linux que disponemos.

Una vez finalizados estos pasos, modificaremos nuestro grabar.php y le añadiremos el siguiente script de inserción de datos.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.013.png)

Tras guardar el archivo con el script de inserción que hemos añadido, comprobamos que funciona correctamente y se guardan los datos en nuestra BD.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.014.png)

Nos vamos a nuestra base de datos y comprobamos que el valor añadido se encuentra.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.015.png)



## Últimos pasos

Tras terminar todos los pasos anteriores, modificaremos nuestros archivos para hacerlos un poco más visibles de cara al público.

Como por ejemplo nuestra página de formularios que era una página web básica en blanco.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.016.png)

Le añadimos un style ( es como un css pero en el mismo archivo ).

Guardamos el archivo y comprobamos que se ha guardado correctamente y se ve de una forma más visible de cara al público.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.017.png)



En nuestra página web principal, queremos que todos los usuarios puedan ver el total de donaciones que se lleva recaudado hasta la fecha por lo que debemos de hacer una consulta a nuestra bases de datos de la tabla donativo y añadirla a nuestro archivo de index.html

Al querer añadir esta consulta en debemos incluir un php para que establezca conexión de nuestro archivo conexion.php, por lo que modificaremos nuestro html y le pondremos index.php.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.018.png)


Al modificar nuestro html a php, también debemos cambiar nuestro grabar.php ya que al introducir una donación y querer volver a nuestra página de inicio lo teníamos con html por lo que le cambiamos el href al nuevo nombre de index.php


![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.019.png)


## Resultado final de la página web

Tras finalizar todos los pasos anteriores, iremos a nuestra página principal y comprobamos que se encuentran todos los cambios que hemos realizado.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.020.png)



## Cosas a tener en cuenta

Una vez hayamos terminado de modificar todo, debemos de securizar nuestro sitio por lo que iremos a los grupos de seguridad de las EC2 de Linux y le quitamos el acceso por el puerto 22.

![](prac4.5_img/Aspose.Words.a88ceebe-eb0e-44c0-9b01-b28fd6ec8b7c.021.png)
