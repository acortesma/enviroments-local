# Kafka y Visor Web

### Introducción
Veremos como disponer en local de un kafka y un visor web de los topics.


### Instalación

Para iniciar ubícate en el directorio y ejecuta:
```
docker-compose up -d
``` 

Podrás publicar y consumir eventos conectando tu aplicación a la ruta:
```
localhost:9092
``` 

Puedes acceder a la pantalla de inicio del visor web:
```
http://localhost:9090
``` 

### Configuración

Documentación oficial de la imagen del visor web: [Documentación](https://hub.docker.com/r/obsidiandynamics/kafdrop)
Documentación oficial de la imagen kafka: [Documentación](https://hub.docker.com/r/obsidiandynamics/kafka)
