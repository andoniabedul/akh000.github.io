---
layout: post
title: "Scaffold Express V4. Como arquitectar una app con NodeJS y Express"
date:   2017-02-13 23:51:00 -0400
categories: blog javascript architecture
---
Siempre me he preocupado en la forma en la que se arquitecta una aplicación por el tema de la escalabilidad, y las buenas prácticas. 

Cuando realizas una aplicación web en NodeJS, a diferencia de Java, realizas un scaffold con directorios, es decir, carpetas normales y corrientes. Lo cual, por una parte es excelente ya que te permite libertad para *arquitectar* tu aplicación, pero por otra parte pierde robustez y estandarización. 

Estuve navegando en la web para elegir como *arquitectar* una aplicación *sencilla* bajo el patrón de diseño MVC. Inclusive discutí el tema con un compañero y me compartió dos enlaces interesantes:

* [[ 1 ] How to build a RESTful API using Express V4](http://www.codekitchen.ca/guide-to-structuring-and-building-a-restful-api-using-express-4/)  
* [[ 2 ] Best practices for Express app structure](https://www.terlici.com/2014/08/25/best-practices-express-structure.html)

Cuanta abstracción es suficiente abstracción.

Sin embargo, yo apuesto por el minimalismo. A la hora de crear una aplicación web bajo MVC, utilizo el siguiente scaffold:
<pre><code>
	– app.js # O también index.js es el archivo main de la aplicación
	- config/ # Archivos de configuración
		- config/development.json # Archivo de desarrollo.
		- config/production.json # Archivo de producción o stage.
	– routes/ # Contiene controladores
	– models/ # Un directorio que contiene los modelos. La capa de Base de Datos.
	– views/ # Las vistas, a su vez tiene carpetas que contienen las vistas por controlador.
	– helpers/ # Un directorio que contiene los archivos de utilidad o ayudantes en un nivel atómico. Mailers, lo incluyo aquí. 
	– bin/ # El directorio de los archivos binarios de los modulos de node.
</code></pre>

Es bastante sencillo e intuitivo. Ahora, en uso con un modulo de usuarios, sería:
<pre><code>
	– app.js # O también index.js es el archivo main de la aplicación
	- config/ # Archivos de configuración
		- config/development.json # Archivo de desarrollo.
		- config/production.json # Archivo de producción o stage.
	– routes/ # Contiene controladores
		– users.js # El controlador del modulo de Usuarios. 
	– models/ # Un directorio que contiene los modelos. La capa de Base de Datos.
		– user.js # El modulo de Base de Datos que contiene el esquema del Usuario y los métodos que consulta, crea, elimina y actualiza. 
	– views/ # Las vistas, a su vez tiene carpetas que contienen las vistas por controlador.
		– users/ # Carpeta con las vistas del módulo de Usuario.
			– register.ejs # La pantalla de registro.
			– login.ejs # Pantalla de login.
	– public/ # Archivos necesarios para la vista y accesos publicos. 
		– css/ # Estilos css.
		– js/ # JavaScript, jQuery, etc.
		– bower_components/ # Componentes front-end con Bower. 
	– helpers/ # Un directorio que contiene los archivos de utilidad o ayudantes en un nivel atómico. Mailers, lo incluyo aquí. 
		– strUtil.js # Archivo de funciones de utilidad para strings. 
	– bin/ # El directorio de los archivos binarios de los modulos de node.
</code></pre>

Hasta ahora, ese es el scaffold que uso actualmente en mis aplicaciones. De hecho, realicé un [repositorio](https://github.com/akh000/scaffold) en Github para hacer fork y comenzar desde ahí. 

Estoy consciente de que existen alternativas como el maravilloso Yeoman. Sin embargo, probé muchísimos generadores y no quedé satisfecho con ninguno. Los generadores instalan demasiadas dependencas que inclusive ni siquiera llegas a usar y añaden peso a la aplicación. Más es el trabajo que hago eliminando dependencias y haciendo refactor del scaffold hecho por el generador, que el tiempo que me tardo arquitectando y haciendo mis carpetas. Sé que muchas veces son el "entorno ideal" pero me siento en la obligación de usar Gulp o Grunt si está instalado, y la verdad, es que para la aplicación que haré no necesito Grunt o Gulp.

Quizás puedes decir: *para que un directorio de vista si lo que se usa actualmente en el front-end son frameworks como Angular, React o Vue* y tienes razón, sin embargo, depende del tamaño y alcance de tu aplicación, no para todo tienes que usar un framework de front-end. A veces me gusta recordar esos tiempos donde usabamos template engines y el front-end era solo CSS, JavaScript y la carpeta views. 

De hecho, puedes usar el scaffold que acabo de plantear arriba y en todas tus rutas arquitectar de forma que respondas y leas JSON, entonces dependiendo de la petición respondes en HTML o en JSON. Entonces, tu aplicación main, utiliza el template engine para mostrar la página principal, y toda la aplicación; un template engine como Jade/Pug, EJS, Handlebars, entre otros. A su vez, como respondes en JSON, si quieres usar Angular o React, puedes hacerlo comodamente. Y estas son unas de las decisiones que te ahorran tiempo y te compran escalabilidad. 

<pre><code>
	
</code></pre>