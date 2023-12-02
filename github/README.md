# Github

## Introducción
Ire explicando paso a paso como realizar diferentes configuraciones de git con github


## Conexión SSH
Una guía completa puede encontrarla en este [enlace](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

1. Generar un par de claves

```bash
ssh-keygen -t ed25519 -C "user@host"
```

El comentario es opcional. Cuando pulses intro se te pedirá que inserte el nombre del fichero y si quieres una clave secreta para el par de llaves.

2. Agrega la clave privada al ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```
Primero inicia el agente de ssh en segundo plano (puede depender del entorno) y agrege su clave privada al ssh-agent

3. Agrega la clave pública a Github

Dirigete a tu cuenta de github -> Settings --> SSh and GPG keys y agregue la clave pública con "New SSH key"

4. Probar conexión

```bash
ssh -T git@github.com
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```

Tras insertar el comando puede que aparezca un mensaje de advertencia para que acepte la "huella digital", acepte. Debe de aparecer el mensaje de confirmación.