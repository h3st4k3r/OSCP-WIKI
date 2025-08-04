`rinetd` y `iptables` son útiles para establecer redirecciones de puertos simples en máquinas intermedias, especialmente cuando no puedes usar `ssh`, `socat` o `chisel`.

---

## 1. `rinetd` – Redirección TCP estática

### Instalación
```bash
sudo apt install rinetd
```

### Configuración
Edita el archivo:
```bash
sudo nano /etc/rinetd.conf
```

Sintaxis:
```
<IP_local> <puerto_local> <IP_remoto> <puerto_remoto>
```

Ejemplo:
```
0.0.0.0 8080 192.168.100.10 80
```
Esto redirige el puerto 8080 local hacia el puerto 80 del host interno `192.168.100.10`.

### Iniciar el servicio:
```bash
sudo systemctl restart rinetd
```

### Verificar
```bash
netstat -tuln | grep 8080
```

---

## Casos de Uso
- Redirección simple sin tunelado SSH
- Exposición de servicios internos a través de un host intermedio

---

## 2. `iptables` – NAT/Forwarding avanzado

Permite redirección a nivel de red si tienes control total del sistema y permisos para manipular reglas.

### Redirigir puerto local a otro host:
```bash
sudo iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.100.10:80
sudo iptables -t nat -A POSTROUTING -j MASQUERADE
```

Esto escucha en `:8080` y reenvía a `192.168.100.10:80`.

### Ver reglas activas
```bash
sudo iptables -t nat -L -n -v
```

### Borrar reglas
```bash
sudo iptables -t nat -F
```

---

## Buenas prácticas OSCP

- Úsalas solo si no tienes acceso a herramientas más flexibles como `socat` o `ssh`
- Asegúrate de tener permisos root
- Documenta las redirecciones con puertos, interfaces y objetivos

---
