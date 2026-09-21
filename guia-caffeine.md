# Guía de LaunchAgents en macOS: Mantener tu Mac despierta con `caffeinate`

Un **LaunchAgent** es un servicio que se ejecuta en segundo plano bajo el contexto de tu usuario tan pronto como inicias sesión. Esta guía te enseña cómo configurar y administrar el script `caffeine` para evitar que tu Mac se duerma.

---

## 1. Crear el Archivo de Configuración

Los LaunchAgents de usuario se guardan en el directorio `~/Library/LaunchAgents/`. 

1. Abre tu terminal y crea el archivo `.plist` usando `vim` (o `vi`):
   ```bash
   vim ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
   ```

2. Pega el siguiente contenido XML:
   *(En **vim**, presiona la tecla `i` para entrar en modo de inserción, luego pega el texto)*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
   <dict>
       <key>Label</key>
       <string>com.maumelendez.caffeine</string>
       <key>ProgramArguments</key>
       <array>
           <string>/usr/bin/caffeinate</string>
           <string>-dimsu</string>
       </array>
       <key>RunAtLoad</key>
       <true/>
       <key>KeepAlive</key>
       <true/>
   </dict>
   </plist>
   ```
   *Para guardar y salir de vim, presiona la tecla `Esc`, escribe `:wq` y luego presiona `Enter`.*

3. Asegura los permisos correctos del archivo (solo tu usuario debe poder escribir en él):
   ```bash
   chmod 644 ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
   ```

---

## 2. Cargar y Activar el Servicio (Iniciar)

Una vez creado el archivo, debes indicarle al sistema de inicio de macOS (`launchd`) que lo registre y ejecute.

* **Método estándar (compatible con cualquier versión de macOS):**
  ```bash
  launchctl load ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
  ```

* **Método moderno (macOS Big Sur y posteriores):**
  ```bash
  launchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
  ```

---

## 3. Verificar que esté Corriendo

Puedes confirmar que el agente está activo de dos maneras:

1. **Buscando el servicio en `launchctl`:**
   ```bash
   launchctl list | grep caffeine
   ```
   *Si todo está bien, verás el PID (ID de proceso) a la izquierda y un código de salida `0` en medio.*

2. **Verificando el proceso de `caffeinate` activo:**
   ```bash
   ps aux | grep caffeinate
   ```

---

## 4. Actualizar la Configuración

Si deseas cambiar los parámetros (por ejemplo, quitarle el flag `-d` para permitir que la pantalla se apague pero la Mac siga despierta):

1. **Detén (descarga) el servicio primero:**
   ```bash
   launchctl unload ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
   ```
2. Abre y edita el archivo `.plist` con `vim`:
   ```bash
   vim ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
   ```
3. **Vuelve a cargar el servicio** para aplicar los cambios:
   ```bash
   launchctl load ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
   ```

---

## 5. Desactivar y Borrar el Servicio (Eliminar)

Si deseas quitar esta automatización por completo de tu sistema:

1. **Detén el servicio de manera definitiva:**
   ```bash
   launchctl unload ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
   ```
   *(O usando el comando moderno: `launchctl bootout gui/$(id -u) ~/Library/LaunchAgents/com.maumelendez.caffeine.plist`)*

2. **Elimina el archivo físico:**
   ```bash
   rm ~/Library/LaunchAgents/com.maumelendez.caffeine.plist
   ```
