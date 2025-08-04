Cuando realizas pivoting y rediriges el tráfico a través de otra máquina (por ejemplo con `ssh`, `chisel`, `socks proxy`, etc.), es posible usar `nmap` para escanear redes internas. Esta guía cubre cómo hacerlo correctamente en OSCP.

---

## 1. Escanear a través de interfaz tunelizada (`tun0`, `tap0`, etc.)

Si estás usando una VPN o túnel tipo `sshuttle`, puedes forzar `nmap` a escanear por esa interfaz:

```bash
nmap -e tun0 -sT -Pn 192.168.100.0/24
```

### Explicación:
- `-e tun0`: fuerza uso de la interfaz tunelizada
- `-sT`: escaneo TCP connect (más estable por túneles)
- `-Pn`: omite ping (útil si ICMP está filtrado)

Puedes ver tus interfaces con:
```bash
ip addr
```

---

## 2. Nmap a través de SOCKS proxy (`proxychains`)

Si levantaste un proxy SOCKS (por ejemplo, con `ssh -D` o Meterpreter `socks_proxy`):

### Configura `/etc/proxychains.conf`

```bash
socks5 127.0.0.1 1080
```

### Lanza Nmap:

```bash
proxychains nmap -sT -Pn -n -p 80 192.168.100.10
```

### Importante:
- Solo funciona con `-sT` (TCP connect). Nmap no soporta `-sS` a través de proxy.
- Muy lento en rangos grandes. Úsalo solo para objetivos concretos.
- Añade `-n` para no resolver DNS.

---

## 3. Uso de `--proxies` (opcional)

Nmap tiene una opción `--proxies`, pero está pensada para HTTP/HTTPS (no SOCKS), así que tiene uso muy limitado:

```bash
nmap --proxies http://127.0.0.1:8080 -p 80 192.168.100.10
```

Solo útil en escenarios muy concretos (con proxy HTTP y escaneos lentos).

---

## Casos de Uso OSCP

- Enumerar servicios internos desde tu Kali tras pivoting
- Identificar RDP, SMB, MySQL, HTTP en redes no expuestas directamente
- Complementar con `proxychains` y herramientas como `smbclient`, `winexe`, etc.

---

## Buenas Prácticas

- Escanea con rangos pequeños para evitar cuelgues
- Usa `-T4` con cuidado (más agresivo)
- Guarda siempre los resultados (`-oN`, `-oA`) para análisis posterior

---
