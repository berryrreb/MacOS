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
