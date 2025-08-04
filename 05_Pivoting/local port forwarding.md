El *Local Port Forwarding* permite redirigir el tráfico desde tu máquina atacante (local) hacia un servicio remoto, a través de una máquina comprometida que tenga acceso al objetivo.

Es extremadamente útil en pentests y en OSCP para acceder a servicios internos que no son accesibles desde fuera.

---

## Sintaxis básica

```bash
ssh -L <puerto_local>:<host_objetivo>:<puerto_objetivo> <usuario>@<ip_intermedia>
```

- `<puerto_local>`: puerto que escucharás en tu máquina
- `<host_objetivo>`: IP/DNS del host al que solo la máquina intermedia tiene acceso
- `<puerto_objetivo>`: servicio en el host objetivo
- `<ip_intermedia>`: máquina comprometida (gateway/pivot)

---

## Ejemplo práctico

Tienes acceso SSH a `10.11.0.5`, y esa máquina puede ver `192.168.100.10:3306` (MySQL). Quieres interactuar con ese MySQL desde tu máquina:

```bash
ssh -L 3306:192.168.100.10:3306 user@10.11.0.5
```

Luego desde tu equipo:
```bash
mysql -h 127.0.0.1 -P 3306 -u root -p
```

---

## Cómo verificar si funciona

Una vez conectado, puedes hacer:
```bash
netstat -an | grep 3306
```

O directamente intentar consumir el servicio (MySQL, RDP, HTTP, etc.) desde tu 127.0.0.1:

```bash
curl http://127.0.0.1:8080
```

---

## Casos de uso OSCP

- Acceder a bases de datos internas no expuestas
- Conectarse a un panel web interno
- Enumerar puertos internos con herramientas desde tu máquina directamente

---

## Buenas prácticas

- Usa puertos altos (no reservados) en tu lado local para evitar conflictos
- Documenta cada túnel activo y a dónde apunta
- Siempre verifica si la conexión se mantiene viva (usa `-N` si no necesitas shell)

Ejemplo:
```bash
ssh -L 8080:10.10.10.50:80 user@pivot -N
```

---
