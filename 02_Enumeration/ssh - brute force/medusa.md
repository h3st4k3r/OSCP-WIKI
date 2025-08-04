`medusa` es una herramienta de fuerza bruta rápida y flexible, similar a `hydra`, pero con soporte modular para muchos protocolos. En OSCP, se usa para verificar credenciales en servicios como SSH, FTP, RDP, SMB, VNC, etc.

---

## Instalación

```bash
sudo apt install medusa
```

---

## Uso Básico

```bash
medusa -h <IP> -u <usuario> -P <lista_contraseñas> -M <módulo>
```

### Ejemplo:
```bash
medusa -h 10.11.1.10 -u admin -P /usr/share/wordlists/rockyou.txt -M ssh
```

---

## Opciones Comunes

- `-h`: IP del objetivo
- `-H`: archivo con múltiples IPs
- `-u`: usuario único
- `-U`: lista de usuarios
- `-p`: contraseña única
- `-P`: lista de contraseñas
- `-M`: módulo (protocolo)
- `-n`: puerto (si no es el estándar)
- `-e ns`: prueba contraseña igual al usuario (n), contraseña vacía (s)
- `-f`: para al encontrar un éxito

---

## Ejemplos por Servicio

### SSH
```bash
medusa -h 10.11.1.10 -U users.txt -P pass.txt -M ssh
```

### FTP
```bash
medusa -h 10.11.1.10 -U users.txt -P pass.txt -M ftp
```

### RDP
```bash
medusa -h 10.11.1.10 -U users.txt -P pass.txt -M rdp
```

### SMB
```bash
medusa -h 10.11.1.10 -U users.txt -P pass.txt -M smbnt
```

---

## Resultados

Muestra los logins válidos en consola. También puedes guardar la salida:
```bash
medusa -h <IP> -U users.txt -P pass.txt -M ssh -O resultados.txt
```

---

## Casos de Uso OSCP

- Verificar cuentas con diccionarios tras enumerar usuarios
- Detectar contraseñas por defecto o repetidas
- Alternativa rápida a `hydra` si este falla o se bloquea

---

## Buenas Prácticas

- Filtrar usuarios antes de atacar
- Usar `-f` para evitar lockouts innecesarios
- Usar con cuidado en servicios sensibles

---
