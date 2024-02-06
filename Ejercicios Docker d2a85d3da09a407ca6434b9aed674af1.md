# Ejercicios Docker



[TOC]

## Ejercicios volúmenes.

1. Crea un volumen docker que se llame `miweb` 

```bash
sudo docker volume create miweb
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled.png)



2. Crea un contenedor desde la imagen `php:7.4-apache` donde montes en el directorio/var/www/html (que sabemos que es el DocumentRoot del servidor que nos ofrece esa imagen) el volumen docker que has creado.

```bash
docker run -d -v miweb:/var/www/html --name miweb-container -p 8080:80 php:7.4-apache
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%201.png)



3. Utiliza el comando docker cp para copiar un fichero `index.html`  en el directorio
   `/var/www/html.` 

```bash
sudo docker cp index.html miweb-container:/var/www/html/
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%202.png)



4. Accede al contenedor desde el navegador para ver la información ofrecida por el fichero
   `index.html.` 

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%203.png)

5. Borra el contenedor

```bash
docker stop miweb-container
docker rm miweb-container
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%204.png)



6. Crea un nuevo contenedor y monta el mismo volumen como en el ejercicio anterior.

```bash
sudo docker run -d --name miweb-container-2 -v miweb:/var/www/html -p 8080:80 php:7.4-apache
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%205.png)



7. Accede al contenedor desde el navegador para ver la información ofrecida por el fichero
   `index.html`  . ¿Seguía existiendo ese fichero?

![Si.](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%206.png)

Si.

---

## Ejercicios bind mount

1. Crea un directorio en tu host y dentro crea un fichero `index.html.` 

```bash
mkdir dockerej
cd dockerej/
sudo nano index.html
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%207.png)



2. Crea un contenedor desde la imagen `php:7.4-apache`  donde montes en el directorio
   `/var/www/html`  el directorio que has creado por medio de bind mount .

```bash
sudo docker run -d --name miweb-container -v ~/dockerej:/var/www/html -p 8080:80 php:7.4-apache
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%208.png)



3. Accede al contenedor desde el navegador para ver la información ofrecida por el fichero
   `index.html` .

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%209.png)

4. Modifica el contenido del fichero `index.html`  en tu `host`  y comprueba que al refrescar la
   página ofrecida por el contenedor, el contenido ha cambiado.

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%2010.png)

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%2011.png)



5. Borra el contenedor

```bash
sudo docker stop miweb-container
sudo docker rm miweb-container
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%2012.png)



6. Crea un nuevo contenedor y monta el mismo directorio como en el ejercicio anterior.

```bash
sudo docker run -d --name miweb-container-2 -v ~/dockerej:/var/www/html -p 8081:80 php:7.4-apache
```

![Untitled](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%2013.png)



7. Accede al contenedor desde el navegador para ver la información ofrecida por el fichero
   `index.html`  . ¿Se sigue viendo el mismo contenido?

![Si.](Ejercicios%20Docker%20d2a85d3da09a407ca6434b9aed674af1/Untitled%2014.png)

Si.