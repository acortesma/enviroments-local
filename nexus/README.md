# Nexus 3 como repositorio en local

### Introducción
Veremos como instalar y configurar un repositorio de artefatos y de imágenes docker

### Instalación

Modifica en el fichero `docker-compose.yml` la ruta donde se generará el volumen en tu máquina:
```
- /{directorio}/nexus-data:/nexus-data
``` 

Para iniciar ubícate en el directorio y ejecuta:
```
docker-compose up -d
``` 

Puedes acceder a la pantalla de inicio con:
```
http://localhost:8081
``` 

La password de administrador puedes encontrarla en el fichero:
```
/nexus-data/admin.password
```

### Configuración

Documentación oficial de la imagen: [Documentación](https://hub.docker.com/r/sonatype/nexus3#red-hat-certified-image)

Tutorial para crear tus repositorios: [Usando Nexus 3](https://blog.sonatype.com/using-nexus-3-as-your-repository-part-1-maven-artifacts)
