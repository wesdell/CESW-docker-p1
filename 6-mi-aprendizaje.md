# MI APRENDIZAJE
Antes de realizar la práctica sabía crear contenedores, pero no conocía cómo guardar la información que se generaba dentro de ellos, ya que al eliminar un contenedor todo se perdía. Con esta práctica aprendí lo siguiente:

- Existen diferentes formas de guardar la información de un contenedor: bind mount, volumen nombrado y volumen anónimo.
- Con un bind mount se usa una carpeta de mi computador, por lo que puedo ver y modificar los archivos directamente, como pasó con el template de html5up y con las carpetas db y www del ejercicio de WordPress.
- Con los volúmenes nombrados Docker se encarga de guardar la información y solo debo indicar el nombre del volumen, esto fue útil para PostgreSQL y Drupal.
- Es importante revisar la documentación de cada imagen en Docker Hub para saber en qué carpeta guarda su información.
- Los contenedores que están en la misma red se pueden comunicar usando su nombre en lugar de la dirección IP.
- Al eliminar un contenedor y crearlo nuevamente con el mismo volumen, la información se mantiene.

### Problemas encontrados
- Al crear el contenedor de PostgreSQL con la imagen `postgres` (versión 18) la ruta donde se guardan los datos cambió, ahora es `/var/lib/postgresql` en lugar de `/var/lib/postgresql/data` que se usaba en versiones anteriores.
- El contenedor de WordPress tardó varios minutos en estar listo, porque primero copia todos sus archivos en la carpeta www del host.

### Otros comandos utilizados
Ver los volúmenes creados
```
docker volume ls
```
Ver la información de un volumen, como su Mountpoint
```
docker volume inspect vol-postgres
```
