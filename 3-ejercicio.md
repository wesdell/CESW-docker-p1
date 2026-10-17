## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
La carpeta db del host está vacía, ya que todavía no se ha creado ningún contenedor que guarde información en ella.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
docker run -d --name server-mysql --network net-wp -v /workspace/ejercicio3/db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=12345 -e MYSQL_DATABASE=db_wordpress -e MYSQL_USER=user_wordpress -e MYSQL_PASSWORD=12345 mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Ahora la carpeta db contiene los archivos que crea MySQL para guardar su información, entre ellos una carpeta llamada db_wordpress que corresponde a la base de datos indicada en la variable MYSQL_DATABASE.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
```
docker run -d --name server-wordpress --network net-wp -p 8080:80 -v /workspace/ejercicio3/www:/var/www/html -e WORDPRESS_DB_HOST=server-mysql -e WORDPRESS_DB_USER=user_wordpress -e WORDPRESS_DB_PASSWORD=12345 -e WORDPRESS_DB_NAME=db_wordpress wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
```
docker rm -f server-wordpress
```
Al crear nuevamente el contenedor e ingresar a _http://localhost:8080_ se muestra el sitio de WordPress con la apariencia personalizada y la entrada creada anteriormente. Esto sucede porque los archivos de WordPress se guardan en la carpeta www y la información en la carpeta db del host, por lo que no se pierden al eliminar el contenedor.

