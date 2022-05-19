# Agregar un HTML personalizado a en servidor web dockerizado Nginx
## · Instalación
Para la realización de esta práctica se ha optado por el uso de la plataforma Play Docker.
Una vez iniciada la sesión y creada una instancia, a través del siguiente comando se lleva a cabo la descarga de la imagen de Nginx en la caché de Docker.
~~~
docker pull nginx
~~~
Una vez descargada, es necesario ejecutar el contenedor de Nginx usando el siguiente comando.
~~~
docker run --rm -d -p 8080:80 --name web nginx
~~~
Para revisar el correcto funcionamiento del servidor web dockerizado basta con introducir localhost:8080, el puerto en el que desplegamos el servidor, y si todo ha ido bien debería aparecer la página de presentación de Nginx. En este caso, la URL viene determinada por la plataforma Play Docker.

![alt](https://github.com/carlosblancoj/Practica_Nginx_Docker/blob/main/1.png)

A continuación, agregaremos un HTML personalizado en lugar de la página por defecto. Para ello, debe detenerse el contenedor de Nginx, en este caso llamado web.
~~~
docker stop web
~~~
## · Agregar un HTML personalizado
Por defecto, el directorio en el que el Nginx busca los archivos es `/usr/share/nginx/html` . De este modo, el HTML personalizado debe estar en ese directorio, por lo tanto haremos uso de volúmenes montados. 

Primero, creamos un directorio nginx y dentro otro llamado site-content `~/nginx/site-content`, en su interior agregamos un archivo index.html con el siguiente código.
~~~
<!DOCTYPE  html>
<html>
<head>
<title>Welcome to nginx!</title>
</head>
<body>
<h1>Hello from Carlos Blanco</h1>
</body>
</html>
~~~
Una vez creado el HTML objetivo, el siguiente paso es montar el reciente directorio local como volumen en el contenedor en ejecución comentado anteriormente. Mediante el uso del siguiente comando, arrancamos de nuevo Nginx pero esta vez con la nueva configuración aplicada.
~~~
docker run --rm -d -p 8080:80 --name web -v ~/nginx/site-content:/usr/share/nginx/html nginx
~~~
Por último verificamos el correcto funcionamiento del proceso.

![alt](https://github.com/carlosblancoj/Practica_Nginx_Docker/blob/main/2.png)
