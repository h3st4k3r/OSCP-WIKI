`smtp-user-enum` es una herramienta especializada para enumerar usuarios a través del protocolo SMTP, aprovechando respuestas del servidor ante comandos como VRFY, EXPN o RCPT TO. En OSCP puede ayudarte a encontrar usuarios válidos sin necesidad de fuerza bruta.

---

## Instalación

En Kali Linux:
```bash
sudo apt install smtp-user-enum
```

O desde GitHub:
```bash
git clone https://github.com/pentestmonkey/smtp-user-enum.git
cd smtp-user-enum
chmod +x smtp-user-enum.pl
```

---

## Modos Soportados

- `VRFY`: Verifica usuarios directamente → `VRFY juan`
- `EXPN`: Expande listas de correo → `EXPN staff`
- `RCPT`: Envía RCPT TO y analiza la respuesta

> *Nota:* La mayoría de servidores modernos bloquean VRFY y EXPN, pero RCPT aún puede funcionar.

---

## Uso Básico (modo RCPT)

```bash
smtp-user-enum -M RCPT -U users.txt -t <IP>
```

### Opciones
- `-M`: Modo (`VRFY`, `EXPN`, `RCPT`)
- `-U`: Diccionario de usuarios
- `-t`: IP objetivo
- `-p`: Puerto (25 por defecto)

### Ejemplo
```bash
smtp-user-enum -M RCPT -U /usr/share/seclists/Usernames/top-usernames-shortlist.txt -t 10.11.1.30 -p 25
```

---

## Validación Manual con Telnet

```bash
telnet 10.11.1.30 25
EHLO test.com
MAIL FROM:<a@a.com>
RCPT TO:<juan>
```

### Interpretación de Respuestas
- `250 OK` → usuario probablemente válido
- `550 No such user` → usuario no existe
- `553 Mailbox name not allowed` → formato incorrecto

---

## Casos de Uso OSCP

- Confirmar usuarios válidos antes de un password spraying
- Identificar nombres de usuario internos
- Reforzar resultados obtenidos por LDAP, SMB o IMAP

---

## Buenas Prácticas

- Evita escaneos agresivos que puedan activar alertas
- Usa diccionarios pequeños y realistas
- No asumas que todas las respuestas son fiables: analiza contexto

---
