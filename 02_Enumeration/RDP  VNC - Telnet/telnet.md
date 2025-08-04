`telnet` es una herramienta de red simple pero muy útil para la fase de enumeración y validación de servicios en OSCP. Aunque su protocolo (puerto 23 TCP) está obsoleto para acceso remoto, sigue siendo valioso como herramienta de diagnóstico y enumeración manual.

---

## Instalación (si no lo tienes)

```bash
sudo apt install telnet
```

---

## Verificar Servicio Telnet (puerto 23)

```bash
telnet <IP> 23
```

Si responde con algo como `login:` o `Welcome`, el servicio está activo. Prueba credenciales por defecto si se permite:
- `admin:admin`
- `root:root`
- `admin:password`

> Nunca fuerces login sin autorización explícita.

---

## Uso como Cliente de Diagnóstico (cualquier puerto)

Telnet es excelente para comprobar conectividad a servicios como SMTP, HTTP, FTP, IMAP, etc.

### Ejemplo: Validar SMTP manualmente
```bash
telnet <IP> 25
EHLO test.com
MAIL FROM:<a@a.com>
RCPT TO:<juan>
```

### Ejemplo: Verificar Banner HTTP
```bash
telnet <IP> 80
GET / HTTP/1.0

```

### Ejemplo: Verificar FTP
```bash
telnet <IP> 21
```

---

## Comprobaciones Rápidas con Bash

```bash
echo "GET / HTTP/1.0\n" | telnet <IP> 80
```

O con redirección:
```bash
echo -e "USER test\nPASS test" | telnet <IP> 21
```

---

## Casos de Uso OSCP

- Verificar si un servicio está escuchando
- Observar banners de servicios para fingerprinting
- Hacer pruebas manuales sin herramientas pesadas

---

## Buenas Prácticas

- Úsalo para ver respuestas rápidas de servicios
- No envíes comandos no documentados
- Combínalo con `netcat` o `nmap` según convenga

---
