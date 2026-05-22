# Configuración de Terminal en Debian 🐧

Guía completa para configurar Zsh + Oh My Zsh + Powerlevel10k con plugins útiles para desarrollo.

---

## Requisitos

- Debian con GNOME
- Conexión a internet
- `git` y `curl` instalados

```bash
sudo apt install git curl -y
```

---

## 1. Instalar Zsh

```bash
sudo apt install zsh -y
```

Verificar instalación:
```bash
zsh --version
```

---

## 2. Instalar Oh My Zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

> Cuando pregunte `Do you want to change your default shell to zsh? [Y/n]` → escribe **Y** y Enter.

---

## 3. Instalar Powerlevel10k

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
  ~/.oh-my-zsh/custom/themes/powerlevel10k
```

Activar el tema en `~/.zshrc`:
```bash
sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="powerlevel10k\/powerlevel10k"/' ~/.zshrc
```

Aplicar cambios:
```bash
source ~/.zshrc
```

Configurar el tema con el asistente visual:
```bash
p10k configure
```

---

## 4. Configuración del Prompt

Para mostrar usuario y directorio en el prompt, editar `~/.p10k.zsh`:

```bash
nano ~/.p10k.zsh
```

Buscar `LEFT_PROMPT_ELEMENTS` y dejarlo así:

```bash
typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(user dir vcs)
```

Aplicar cambios:
```bash
source ~/.zshrc
```

El prompt quedará así:
```
mauro-dev ~/Documents/Docker_course_2026  main ❯
```

---

## 5. Instalar Plugins

### 5.1 zsh-autosuggestions
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
```

### 5.2 zsh-syntax-highlighting
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting \
  ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```

### 5.3 you-should-use
```bash
git clone https://github.com/MichaelAquilina/zsh-you-should-use \
  ~/.oh-my-zsh/custom/plugins/you-should-use
```

### 5.4 fzf
```bash
sudo apt install fzf -y
```

### 5.5 zoxide
```bash
sudo apt install zoxide -y
```

Agregar al final de `~/.zshrc`:
```bash
eval "$(zoxide init zsh)"
```

### 5.6 python3-pygments (para colorize)
```bash
sudo apt install python3-pygments -y
```

---

## 6. Activar todos los plugins

Editar `~/.zshrc`:
```bash
nano ~/.zshrc
```

Buscar la línea `plugins=(` y reemplazarla por:

```bash
plugins=(
  git
  docker
  docker-compose
  zsh-autosuggestions
  zsh-syntax-highlighting
  you-should-use
  copypath
  copyfile
  colorize
  fzf
)
```

Aplicar cambios:
```bash
source ~/.zshrc
```

---

## 7. Referencia de Plugins

| Plugin | Función | Uso |
|---|---|---|
| `git` | Alias para Git | `gst`, `gco`, `gp` |
| `docker` | Alias para Docker | `dps`, `dpsa`, `dib` |
| `docker-compose` | Alias para Docker Compose | `dcu`, `dcd`, `dcl` |
| `zsh-autosuggestions` | Sugerencias en gris mientras escribes | `→` para aceptar |
| `zsh-syntax-highlighting` | Colorea comandos en tiempo real | Automático |
| `you-should-use` | Recuerda usar alias | Automático |
| `copypath` | Copia ruta actual al portapapeles | `copypath` |
| `copyfile` | Copia contenido de archivo | `copyfile archivo` |
| `colorize` | Colorea archivos al verlos | `ccat archivo.py` |
| `fzf` | Búsqueda inteligente en historial | `Ctrl + R` |
| `zoxide` | Navegación inteligente de carpetas | `z Docker` |

---

## 8. Alias útiles de Docker

| Alias | Comando real |
|---|---|
| `dps` | `docker ps` |
| `dpsa` | `docker ps -a` |
| `dcu` | `docker compose up` |
| `dcd` | `docker compose down` |
| `dcl` | `docker compose logs` |
| `dce` | `docker compose exec` |
| `dib` | `docker image build` |
| `dils` | `docker image ls` |

---

## 9. Solución de problemas

### La terminal sigue abriendo Bash
```bash
chsh -s $(which zsh)
```
Cerrar sesión de GNOME completamente y volver a entrar.

### Plugin not found
Verificar que los plugins están instalados:
```bash
ls ~/.oh-my-zsh/custom/plugins/
```

### Reconfigurar Powerlevel10k
```bash
p10k configure
```

---

## Autor

**Mauro Dev** — Debian + Docker + Zsh 🚀
