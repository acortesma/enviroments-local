# Jenkins

### Introducción
Veremos como disponer en local de un jenkins que tenga acceso al Docker del host local.


### Instalación

Modifica en el fichero `docker-compose.yml` la ruta donde se generará el volumen en tu máquina:
```
- /{directorio}/jenkins_home:/var/jenkins_home
``` 

Para iniciar ubícate en el directorio y ejecuta:
```
docker-compose up -d
``` 

Puedes acceder a la pantalla de inicio:
```
http://localhost:8080
``` 

### Configuración

Documentación oficial de la imagen: [Documentación](https://hub.docker.com/r/jenkins/jenkins)