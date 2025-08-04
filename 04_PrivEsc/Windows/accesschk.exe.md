`AccessChk.exe` es una herramienta de Sysinternals (Microsoft) usada para enumerar permisos de archivos, servicios, directorios, etc. En OSCP es totalmente válida y puede ayudarte a encontrar escaladas de privilegios por mala configuración de permisos.

---

## Descarga

Desde el sitio oficial:
https://learn.microsoft.com/en-us/sysinternals/downloads/accesschk

O desde tu máquina Kali:
```bash
wget https://download.sysinternals.com/files/AccessChk.zip
unzip AccessChk.zip
```

Sube `accesschk.exe` a la máquina víctima usando `smbserver.py`, `certutil`, `python3 -m http.server`, etc.

---

## Uso básico

### Enumerar servicios que puede modificar el usuario actual:
```cmd
accesschk.exe -uwcqv "<usuario>" * /accepteula
```

Ejemplo práctico:
```cmd
accesschk.exe -uwcqv "johndoe" *
```

### Enumerar servicios con permisos de escritura:
```cmd
accesschk.exe -uwcqv "Users" *
```

Si alguno muestra `SERVICE_ALL_ACCESS`, puedes modificarlo y escalar privilegios.

---

## Otros usos útiles

### Ver permisos sobre una carpeta:
```cmd
accesschk.exe -d "C:\Program Files\NombreApp"
```

### Ver acceso a registros:
```cmd
accesschk.exe -k HKEY_LOCAL_MACHINE\Software
```

### Ver accesos sobre un ejecutable:
```cmd
accesschk.exe -q -v C:\Windows\System32\some.exe
```

---

## Escalada típica

1. Encuentras un servicio donde el grupo `Users` tiene `SERVICE_ALL_ACCESS`
2. Paras el servicio, reemplazas el ejecutable por un reverse shell, lo reinicias
3. Shell con permisos elevados

---

## Buenas Prácticas

- Usa `accesschk` como alternativa ligera a `winPEAS` para pasar más desapercibido
- Siempre intenta identificar servicios mal configurados
- Documenta cada ruta o servicio vulnerable para explotarlo paso a paso

---