# Jenkins

## Introducción
Veremos como disponer en local de un jenkins
En este ejemplo configuraremos Jenkins para que utilice una agente como ejecutor. Dejaremos a Jenkins como parte controladora que gestionará los agentes.

## Contenido
- *docker-compose*: fichero con la configuración completa
- *.env*: fichero que contiene variables de entorno necesarias para el agente ssh
- *ssh-key*: par de clave pública/privada necearia para conectar Jenkins con el agente.


## Instalación

### 1. Iniciar los contenedores

Lo primero será iniciar tanto Jenkins como el agente, una jez ejecutado el comadno podrás observar que tienes en tu máquina dos contenedores levantados
```bash
docker compose up -d
```

### 2. Iniciar Jenkins
 Una vez ejecutado tenemos que entar en Jenkins `localhost:8080` ahí tendrás que seguir los primeros pasos para iniciar jenkins 

### 3. Configuración de comunicación master-agente

Puedes usar las claves incluidas en este repositorio pero se recomienda crear un par nuevas.
1. creamos un par de claves SSH `ssh-keygen -t ed25519 -C "jenkins@agent"`
2. insertamos la pública en el fichero `.env` que al final será asignado como varialble de entorno al contendor ssh-agent: `JENKINS_AGENT_SSH_PUBKEY`

Si quieres ejecutar un agente manualmente, podrías ejecutarlo (sustituyendo los corchetes por tu clave pública):
```bash
docker run -d --rm --name=agent-jenkins --network jenkins -p 22:22 -e "JENKINS_AGENT_SSH_PUBKEY=[public-ssh]" jenkins/ssh-agent:jdk17
```

> Es posible que en tu máquina ya esté utilizado el puerto 22, puedes modificar el docker-compose para cambiar el puerto de entrada, pero ten en cuenta que
esto también obligará a modificarlo cuando se esté creando la comunicación del agente con Jenkins

### 4. Configurar agente en Jenkins

Vamos a `Manage Jenkins--> Nodes --> New Node `crear nuevo nodo [guía](https://www.jenkins.io/doc/book/using/using-agents/)

Creamos el nodo poniendo especial atención a estos atributos:
    - *Remote root directory*: /home/jenkins
    - *Launch*: Lauch agents via SSH
    - *host*: <name_host_agent>
    - *host key verification*: Noverifying Verification Strategy

![Agent Config](/doc/ssh-agent-config.png?raw=true "Ssh Agent Config")

Una vez creado podemos ingresar en los logs del agente y verificar la correcta conexión
```bash
Launcher: SSHLauncher
Communication Protocol: Standard in/out
This is a Unix agent
Agent successfully connected and online
```


> Se puede seleccionar otra *host key verification*: know hosts file Verification Strategy, pero para ello habría que realizar estos pasos
 - Configurar el fichero `known_hosts`, es necesario añadir el nuevo agente como hosts conocidos, para ello ejecutamos
 ```bash
 docker exec -it jenkins /bin/bash
 ssh-keyscan agent-jenkins >> /var/jenkins_home/.ssh/known_hosts
 ```
si el fichero no existe debemos de crearlo

Se puede probar la conexión de forma manual desde el contenedor de jenkins con el siguiente comando:
 ```bash
ssh -i <ruta_clave_privada_ssh> <user_name_agent>@<name_host_agent>
ssh -i <ruta_clave_privada_ssh> jenkins@agent-jenkins
 ```

### 4. Modificar Nodo Principal
Una vez configurado nuestro agente pasaremos a configurar el nodo principal para que no ejecute tareas de construcción y únicamete se use como controlador

Vamos a `Manage Jenkins--> Nodes --> Principal --> Configuration` y seleccionamos `Number of executors`:0
          
## Ejecución de tarea con Pipeline

1. Creamos una nueva tarea
2. Seleccionamos que sea una tarea `Pipeline`
3. En la sección de pipeline seleccionamos uno de los de ejemplo: `Hellow Worl`
4. Guardamos y ejecutamos la tarea. Podremos ver que se ejecuta en el agente.
