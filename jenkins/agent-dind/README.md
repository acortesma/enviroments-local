# Jenkins

## Introducción
Veremos como disponer en local de un jenkins

## Contenido
- *docker-compose*: fichero con la configuración completa
- 


## Instalación


### 1. Resumen docker-compose.yml
 - Usuario root por defecto (ver otras formas más adelante), esto es debido a problemas con el plugin de git (no tenía permisos para acceder a certificados tls y no hacía check contra github con https)
 - 

 ### 2. Construcción del agente ssh

 ### 3. Configuración de comunicación master-agente

1. creamos un par de claves SSH `ssh-keygen -t ed25519 -C "jenkins@agent"`
2. insertamos la pública en el agente a través de `JENKINS_AGENT_SSH_PUBKEY`

Si quieres ejecutar un agente manualmente, podrías ejecutar (sustituyendo los corchetes por tu clave pública):
```bash
docker run -d --rm --name=agent-jenkins --network jenkins -p 22:22 -e "JENKINS_AGENT_SSH_PUBKEY=[public-ssh]" jenkins/ssh-agent:jdk17
docker run -d --rm --name=agent-jenkins --network jenkins -v /var/run/docker.sock:/var/run/docker.sock -p 22:22 -e "JENKINS_AGENT_SSH_PUBKEY=[public-ssh]" agent-jenkins-dind
```

3. Configurar agente en Jenkins
 - Crear nueva credencial ssh con la clave privada
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

 - crear nuevo nodo [guía](https://www.jenkins.io/doc/book/using/using-agents/)

    Nos vamos a "Administración Jenkins -> Nodos -> New Nodo y craamos el nodo poniendo especial atención a:
    - *Remote root directory*: /home/jenkins
    - *Launch*: Lauch agents via SSH
    - *host*: <name_host_agent>
    - *host key verification*: know hosts file Verification Strategy

          
## Configurando conexión con Github

### 1. crear enlace para exponer jenkins al mundo
    - instalar ngrok en la máquina, crear una cuenta
    - configurar tunel en fichero, añadir autenticación, 

### 2. configurar webhook en github
    añadir la url de ngrok (sale en la consola "Forwarding") acabada en "/github-webhook/" y ‘Content type’ select: ‘application/json’

### 3. Configuramos conexion SSH jenkins con github
    - creamos claves : `ssh-keygen -t rsa -b 4090 -C "github-acortes-jenkins"`
    - agregamos la "private key" en jenkins
    - agregamos la "public key" en github
    - NOTA: existe un problema con Jenkins y es que aún añadiendo la clave SSH no se añade github en el fichero "known_hosts".
        En Jenkins se podemos ir a config y eliminar este requisito o entrar por consola en el contenedor de Jenkins y agregarlo manualmente con uno de estas dos formas:
            1. `ssh-keyscan github.com >> ~/.ssh/known_hosts` (si no existe el fichero se crea manualmente)
            2. `ssh -T git@github.com` esto comprueba, al comprobar te sale el mensaje si quieres añadirlo


## Ejecución de tarea con Pipeline

### 1. Nuevo proyecto
    - creamos un nuevo repo en gitHub
    - Agregamos un fichero `JenkinsFile` en la raíz del repo

### 2. Seleccionando agente