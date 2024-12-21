# Guía para Instalar y Configurar ZSH y Oh My ZSH

Esta guía explica cómo instalar ZSH, configurarlo como shell predeterminado y personalizarlo con Oh My ZSH, utilizando también un archivo `.zshrc` personalizado.

---

## 1. Instalación de ZSH

ZSH (Z Shell) es una potente shell con funciones avanzadas de scripting y personalización.

### Comandos:
```bash
sudo apt update
sudo apt install zsh -y
zsh --version
```

### Configurar ZSH como predeterminado:
```bash
chsh -s $(which zsh)
```

**Nota:** Y luego cierra sesión y vuelve a entrar. Comprueba con `echo $SHELL`.

---

## 2. Instalación de Oh My ZSH

Oh My ZSH es un framework para gestionar configuraciones de ZSH de forma sencilla y eficiente.

### Comandos para instalar Oh My ZSH:
**url:** https://ohmyz.sh/#install
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

---

## 3. Personalización de ZSH con `.zshrc`

A continuación abra el archivo `.zshrc` y añada la siguiente configuración:

```zsh
# Configuración de plugins

ZSH_THEME="robbyrussell"

COMPLETION_WAITING_DOTS="true"

plugins=(
    git
    mvn
    sdk
    docker
    docker-compose
    ubuntu
    zsh-completions
    zsh-autosuggestions
    colored-man-pages
    zsh-syntax-highlighting
)

fpath+=${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions/src

# User configuration

ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#757575"

---

## 4. Instalación de Plugins Adicionales

Oh My ZSH soporta plugins que pueden mejorar la funcionalidad de ZSH.

### Plugins que requieren instalación manual:

#### 1. `zsh-completions`
Este plugin mejora las opciones de autocompletado.
**url:** https://github.com/zsh-users/zsh-completions
```bash
  git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions
```

#### 2. `zsh-autosuggestions`
Proporciona sugerencias automáticas basadas en tu historial de comandos.
**url:** https://github.com/zsh-users/zsh-autosuggestions?tab=readme-ov-file
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

#### 3. `zsh-syntax-highlighting`
**url:** https://github.com/zsh-users/zsh-syntax-highlighting
Añade resaltado de sintaxis para mejorar la legibilidad de comandos.
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### Asegúrate de incluir estos plugins en la lista de `plugins` en el archivo `.zshrc`.

---

## Referencias

- [ZSH Documentation](https://zsh.sourceforge.io/)
- [Oh My ZSH GitHub](https://github.com/ohmyzsh/ohmyzsh)
- [Guía asanzdiego](https://www.asanzdiego.com/2018/04/instalar-y-configurar-zsh-y-ohmyzsh-en-ubuntu.html)
