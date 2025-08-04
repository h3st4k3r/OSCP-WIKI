# Guía de Uso de smbclient para OSCP

`smbclient` es una herramienta de línea de comandos que permite conectarse a recursos compartidos (shares) SMB/CIFS en sistemas Windows o Linux. Es útil en OSCP para listar, leer o descargar archivos desde shares accesibles, incluso como usuario anónimo.

---

## Instalación

```bash
sudo apt install smbclient
```

---

## Enumeración de Shares (sin credenciales)

```bash
smbclient -L //<IP>/ -N
```

- `-L`: lista recursos compartidos
- `-N`: no pedir contraseña (modo anónimo)

### Con credenciales:
```bash
smbclient -L //<IP>/ -U usuario
```

---

## Conexión a un Share

### Como usuario anónimo:
```bash
smbclient //<IP>/sharename -N
```

### Con usuario y contraseña:
```bash
smbclient //<IP>/sharename -U usuario
```

Una vez dentro:
- `ls`: listar archivos
- `cd <dir>`: cambiar directorio
- `get <file>`: descargar archivo
- `put <file>`: subir archivo (solo si está permitido)

---

## Descargar Archivos Desde Línea

```bash
smbclient //<IP>/sharename -N -c 'get secret.txt'
```

---

## Montar Share en Linux (temporal)

```bash
sudo mount -t cifs //10.11.1.100/share /mnt/smb -o user=usuario,password=clave,vers=2.0
```

> Requiere paquete `cifs-utils`

---

## Casos de Uso OSCP

- Acceso a backups, contraseñas, scripts o archivos de configuración
- Detección de rutas interesantes o archivos `.ps1`, `.txt`, `.bak`
- Extracción de documentos con metadatos, historiales, claves

---

## Buenas Prácticas

- Probar siempre acceso anónimo primero
- Descargar solo lo necesario y documentar hashes (`sha256sum`)
- Complementar con `enum4linux-ng`, `rpcclient` o `crackmapexec`

---