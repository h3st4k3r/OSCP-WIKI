`findstr` es el equivalente a `grep` en Windows. Se utiliza para buscar cadenas de texto dentro de archivos o en la salida de comandos. En OSCP es útil para encontrar contraseñas, configuraciones sensibles o claves de acceso dentro de archivos de texto, scripts o incluso salidas de comandos.

---

## Uso Básico

```cmd
findstr "cadena" archivo.txt
```

Ejemplo:
```cmd
findstr "password" C:\inetpub\wwwroot\web.config
```

---

## Uso en Recursivo

```cmd
findstr /S /I /M "password" *
```

Explicación:
- `/S`: busca en subdirectorios
- `/I`: sin distinguir mayúsculas/minúsculas
- `/M`: solo muestra el nombre del archivo con coincidencias
- `*`: sobre todos los archivos del directorio actual

---

## Buscar múltiples patrones

```cmd
findstr /S /I /M "password pass pwd key user" *
```

---

## Buscar en combinación con otros comandos

### Buscar en la salida de `type`:
```cmd
type archivo.txt | findstr "admin"
```

### Buscar en la salida de `net user`:
```cmd
net user | findstr "NombreUsuario"
```

---

## Casos de Uso OSCP

- Buscar contraseñas en archivos `.xml`, `.config`, `.ini`, `.ps1`, `.bat`, `.vbs`, etc.
- Filtrar resultados masivos de herramientas como `accesschk` o `winPEAS`
- Inspeccionar logs, scripts o configuraciones en busca de credenciales hardcodeadas

---

## Buenas Prácticas

- Empieza buscando desde `C:\Users\<usuario>` o `C:\inetpub\wwwroot`
- Usa palabras clave: `password`, `pass`, `pwd`, `key`, `secret`, `token`, `user`, `admin`
- Guarda los resultados a archivo para análisis posterior

Ejemplo:
```cmd
findstr /S /I "password" * > resultados.txt
```

---
