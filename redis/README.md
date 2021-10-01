# Redis

### Introducción
Veremos como disponer en local de una Redis y un visor web


### Instalación

Modifica en el fichero `docker-compose.yml` el puerto (8090) en el cual abriras el visor


Para iniciar ubícate en el directorio y ejecuta:
```
docker-compose up -d
``` 

Puedes acceder a la pantalla de inicio:
```
http://localhost:8090
``` 

### Configuración

Documentación oficial de la imagen: [Documentación](https://github.com/joeferner/redis-commander)