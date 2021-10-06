# MongoDb como repositorio en local

### Introducción
Veremos como levantar una bbdd noSql en local

### Instalación

Modifica en el fichero `docker-compose.yml` la ruta donde se generará el volumen en tu máquina:
```
- /{directorio}/mongodb:/data/db
``` 

Para iniciar ubícate en el directorio y ejecuta:
```
docker-compose up -d
``` 

