# Guía de Configuración de Ubuntu 24

Este documento detalla paso a paso el proceso de configuración de un sistema Ubuntu 24 recién instalado.

---

## Índice

1. [Preparativos Iniciales](#preparativos-iniciales)
2. [Actualización del Sistema](#actualizacion-del-sistema)
3. [Instalación de Herramientas Esenciales](#instalacion-de-herramientas-esenciales)
4. [Personalización del Escritorio](#personalizacion-del-escritorio)
5. [Configuración de Desarrollo](#configuracion-de-desarrollo)
6. [Seguridad y Backups](#seguridad-y-backups)

---

## 1. Preparativos Iniciales

### Componente: Adaptador Wifi D-Link DWA-172
**Descripción:** Configurar conexión a internet con adaptador usb D-Link DWA-172
- **URL:**
- **Comandos:**
  ```bash
  sudo apt remove rtl8812au-dkms
  sudo apt install git
  git clone https://github.com/morrownr/8821au-20210708.git
  sudo dkms add ./8821au-20210708
  sudo dkms install rtl8821au/5.12.5.2
  ```

---

## 2. Actualización del Sistema

### Componente: Actualización del Sistema Operativo
- **Comandos:**
  ```bash
  sudo apt update
  sudo apt upgrade -y
  sudo apt dist-upgrade -y
  ```

  Nota: Usa <apt dist-upgrade> cuando necesites realizar actualizaciones importantes que requieran cambios en las dependencias o eliminación de paquetes antiguos.

### Componente: Limpieza del Sistema
- **Comandos:**
  ```bash
  sudo apt autoremove -y
  sudo apt autoclean
  ```

---

## 3. Instalación de Herramientas Esenciales

### Componente: Git
- **URL:** https://git-scm.com/downloads/linux
- **Referencia externa:** [Configuración de ssh](git_ssh-setup.md)
- **Comandos:**
  ```bash
  sudo apt install git -y
  git --version
  ```

  si quieres la última versión puedes añadir el repositorio PPA:
  ```bash
  sudo add-apt-repository ppa:git-core/ppa
  ```

### Componente: curl y wget
**Descripción:** Descarga de archivos y contenido web.
- **Comandos:**
  ```bash
  sudo apt install curl wget -y
  curl --version
  wget --version
  ```

---

## 4. Personalización del Escritorio

### Componente: Instalación de ZSH y Oh My ZSH
**Descripción:** Instalar y configurar en Ubuntu la shell ZSH y el framework Oh My ZSH.
- **Referencia externa:** [Configuración de ZSH y Oh My ZSH](zsh-setup.md)

---

## 5. Herramientas de Desarrollo

### Componente: Docker y Docker Compose
**Descripción:** Instalar Docker y Docker Compose para entornos de desarrollo.
- **url:** https://docs.docker.com/engine/install/ubuntu/#install-from-a-package
- **Comandos:**
  ```bash
  # Tras seguir los pasos del sitio oficial

  # Verificar instalación
  sudo systemctl status docker

  # Añadir usuario al grupo Docker (opcional)
  sudo usermod -aG docker $USER

  Configuración del arranque automático de los servicios:
  sudo systemctl enable docker.service
  sudo systemctl enable containerd.service
  ```

  ### Componente: SDKMAN
**Descripción:** Instalación y configuración de SDKMAN para gestionar versiones de SDKs como Java, Kotlin, Maven, etc.
- **URL:** https://sdkman.io/install/
- **Comandos:**
  ```bash
  # Descargar e instalar SDKMAN
  curl -s "https://get.sdkman.io" | bash

  # Cargar SDKMAN en la sesión actual
  source "$HOME/.sdkman/bin/sdkman-init.sh"

  # Verificar instalación
  sdk version

  # Uso básico (instalar Java como ejemplo)
  sdk install java java 17.0.13-tem
  sdk install maven
  ```

### Componente: NVM (Node Version Manager)
**Descripción:** Instalación de NVM para gestionar múltiples versiones de Node.js.
- **URL:** https://github.com/nvm-sh/nvm
- **Comandos:**
  ```bash
  # Descargar e instalar NVM
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

  # Verificar instalación
  nvm --version

  # Uso básico (instalar la última versión de Node.js)
  nvm install node
  nvm use node
  ```

### Componente: IntelliJ IDEA Community Edition
**Descripción:** Instalación y configuración de IntelliJ IDEA Community Edition, un IDE para desarrollo en Java, Kotlin, y más.
- **URL:** https://www.jetbrains.com/idea/download/
- **Comandos:**
  ```bash
  # Descargar IntelliJ IDEA Community Edition desde JetBrains Toolbox o con wget
  wget https://download.jetbrains.com/idea/ideaIC-2023.2.3.tar.gz

  # Extraer el archivo descargado
  tar -xvzf ideaIC-2023.2.3.tar.gz

  # Mover al directorio de aplicaciones (opcional)
  sudo mv idea-IC-*/ ~/opt/intellij-idea

  # Crear la carpeta bin si no existe
  mkdir -p ~/bin

  # Crear un enlace simbólico para facilidad de uso
  ln -s ~/opt/intellij-*/bin/idea ~/bin/idea

  # Editar el archivo de configuración de ZSH (~/.zshrc) para hacer el cambio permanente
  echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc

  # Recargar la configuración
  source ~/.zshrc

  # Ejecutar IntelliJ IDEA
  idea
  ```

---

## 6. Seguridad y Backups

(En construcción)
---

## Notas Adicionales

- Actualiza este documento a medida que cambien las herramientas o tus necesidades.
- Considera exportar esta guía a un PDF para mayor accesibilidad.

---
