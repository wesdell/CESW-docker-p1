# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)

### Comando usado
```
docker run -d --name srvnginx -p 8080:80 -v /workspace/nginx/html:/usr/share/nginx/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar a _http://localhost:8080_ el servidor de Nginx devulve el código de error 403 (Forbidden) debido a que la carpeta nginx/html está vacía.

### ¿Qué pasa con el archivo index.html del contenedor?
El archivo index.html de la imagen de nginx queda oculto. Dado que usamos un bind mount, el contenido del directorio del host sobrescribe temporalmente la visibilidad del directorio en el contenedor.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
El servidor ahora muestra la página web del template descargado.

### Eliminar el contenedor
```
docker rm -f srvnginx
```

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
Al ingresar nuevamente a localhost:8080, la página web del template se muestra inmediatamente debido a la persistencia de datos.
