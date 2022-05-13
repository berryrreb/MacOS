# MacOS

MacOS Cheat guide 

## Cambiar número de íconos en launchpad

Elegimos el número de filas y columnas deseado por pantalla y matamos el proceso de launchpad, se reiniciará y tendrá los nuevos ajustes.

```sh
defaults write com.apple.dock springboard-rows -int 10

defaults write com.apple.dock springboard-columns -int 10

defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock
```
## Limpiar RAM 

```sh
sudo purge
```

## Quitar control de Chrome/Edge desde media control/keys

Ir desde la barra de navegación a la dirección:

```txt
chrome://flags/#hardware-media-key-handling #Para chrome
 
edge://flags/#hardware-media-key-handling #Para edge
```

Buscar y deshabilitar la opción **Hardware Media Key Handling**

> Para **Edge** puede que ya no exista dicha opción, habilitar *Temporarily unexpire M100 flags* o similar para ver si la opción sigue vigente.

Reiniciar Edge/Chrome

## Descargar Command Line Tools

Abrir Terminal y correr el comando:

```sh
xcode-select --install
```

Saldrá un promp con pasos a seguir para instalar la herramienta.

Si esto no funciona, se puede descargar desde [developer.apple](https://developer.apple.com/download/more/)

## Cambiar promp terminal

Editar archivo /etc/zshrc y cambiar la línea PS1=... por algo como lo siguiente. Según deseado.

```txt
PS1="[MacBook %1~]$ "
```

## Evitar la creación de archivo .DS_Store en cada directorio

```zsh
defaults write com.apple.desktopservices DSDontWriteNetworkStores true
```
Si quieres regresar a al configuración original:

```zsh
defaults write com.apple.desktopservices DSDontWriteNetworkStores false
```

## Now Playing App

[Now Playing](https://github.com/teaminkling/now-playing)

## Homebrew Installation

[Homebrew](https://docs.brew.sh/Installation)

## OhMyZSH

Installation

```zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Add the *zshrc_bck* file to your home directory.

After that, add it to your *~/.zshrc* file:

```zsh
echo 'source ~/zshrc_bck' >> ~/.zshrc
```

> Modify every custom line in the *~/zshrc_bck* file. Maybe username info.

### Edit your *~/.zshrc* file's plugins part:

```txt
plugins=( 
        git
        macos
        terraform
)
```

### Change OhMyZsh theme

```zsh
sed -i .bck 's/ZSH_THEME.*/ZSH_THEME="geoffgarside"/g' ~/.zshrc
```
