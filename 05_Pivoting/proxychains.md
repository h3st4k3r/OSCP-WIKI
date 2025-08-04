`proxychains` permite redirigir el tráfico de herramientas de red a través de un proxy SOCKS (como el que generas con `ssh -D`, `chisel`, o Meterpreter). Muy útil en OSCP para escanear y acceder a redes internas tras pivot.

---

## 1. Configurar proxychains

Edita `/etc/proxychains.conf`:
```bash
sudo nano /etc/proxychains.conf
```

Al final del archivo, comenta todas las líneas `socks` y añade:
```bash
socks5 127.0.0.1 1080
```

*(puerto 1080 o el que estés usando)*

Puedes usar `proxychains4` si tu sistema lo tiene separado de `proxychains`.

---

## 2. Uso básico

Ejecuta cualquier herramienta con `proxychains`:

```bash
proxychains nmap -sT -Pn -n -p 80 192.168.100.10
proxychains curl http://192.168.100.10
proxychains smbclient -L 192.168.100.10 -N
```

### Solo funciona con herramientas que respetan `connect()`
No funcionará con herramientas que usen `raw sockets` directamente (por ejemplo `nmap -sS`).

---

## 3. Proxy dinámico desde Kali

Puedes usar `ssh` para generar un proxy:
```bash
ssh -D 1080 user@10.10.10.10
```
O desde Meterpreter:
```bash
run auxiliary/server/socks_proxy
```

---

## Casos de Uso OSCP

- Escaneo de red interna tras comprometer un pivot
- Uso de herramientas como `smbclient`, `rdesktop`, `crackmapexec`, etc. contra objetivos internos
- Enumeración sin usar túneles `-L` específicos

---

## Buenas Prácticas

- Usa siempre `-sT` con `nmap`
- Añade `-n` para no resolver DNS
- No escanees rangos grandes, se vuelve muy lento
- Puedes usar `proxychains -q` para salida más limpia

---