`ncrack` es una herramienta de fuerza bruta desarrollada por los creadores de Nmap, optimizada para realizar ataques de autenticación a alta velocidad sobre múltiples protocolos. Es útil en OSCP para validar credenciales contra SSH, RDP, FTP, HTTP, VNC, SMB y más.

---

## Instalación

```bash
sudo apt install ncrack
```

---

## Uso Básico

```bash
ncrack -p <puerto> -U users.txt -P pass.txt <IP>
```

### Ejemplo:
```bash
ncrack -p 22 -U users.txt -P rockyou.txt 10.11.1.10
```

---

## Módulos Soportados

- SSH (`-p 22`)
- RDP (`-p 3389`)
- FTP (`-p 21`)
- HTTP (básico y digest, solo si es autenticación estándar)
- VNC (`-p 5900`)
- SMB (`-p 445`) *limitado*

---

## Ataque Contra un Servicio Específico

### RDP
```bash
ncrack -p rdp -U users.txt -P pass.txt 10.11.1.20
```

### SSH
```bash
ncrack -p ssh -U users.txt -P pass.txt 10.11.1.30
```

### FTP
```bash
ncrack -p ftp -U users.txt -P pass.txt 10.11.1.40
```

---

## Resultados

Los logins válidos se mostrarán en la salida estándar:
```
Discovered credentials on 10.11.1.10 22/tcp: admin / password123
```

Usa `-oN` para guardar:
```bash
ncrack -p ssh -U users.txt -P pass.txt 10.11.1.10 -oN resultados.txt
```

---

## Casos de Uso OSCP

- Verificar accesos sobre servicios detectados en reconocimiento
- Alternativa a `hydra` y `medusa` si hay problemas con ciertos protocolos
- Muy eficaz contra RDP y SSH por su velocidad y tolerancia a errores

---

## Buenas Prácticas

- Filtrar usuarios previamente para reducir intentos
- No abusar de servicios sensibles (usa `-gcl` para limitar conexiones simultáneas)
- Usar `-f` para detener tras el primer éxito

---
