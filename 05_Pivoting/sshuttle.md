`sshuttle` es una herramienta muy útil para realizar pivoting transparente a nivel de red. Redirige automáticamente todo el tráfico IP hacia una red interna, usando una máquina intermedia a la que tengas acceso SSH.

Funciona como una VPN parcial, sin necesidad de configurar rutas manuales ni tunelado de puertos. Es ideal para pentesters en escenarios OSCP donde el pivot tiene conexión SSH.

---

## Instalación

En Kali Linux ya viene instalado. Si no:
```bash
sudo apt install sshuttle
```

---

## Uso básico

```bash
sshuttle -r <usuario>@<ip_intermedia> <red_destino>/<máscara>
```

### Ejemplo:
```bash
sshuttle -r user@10.10.10.10 192.168.100.0/24
```

Esto enruta todo el tráfico dirigido a `192.168.100.0/24` a través de `10.10.10.10`.

---

## Otras opciones útiles

- `-vv`: modo verbose
- `--dns`: tuneliza también peticiones DNS
- `-x`: excluir rangos

Ejemplo completo:
```bash
sshuttle -r user@10.10.10.10 192.168.100.0/24 --dns -vv
```

---

## Requisitos

- Acceso SSH a la máquina intermedia
- Python en la máquina remota
- Tu usuario SSH debe tener permisos para lanzar procesos (no funciona con shells limitadas)

---

## Casos de Uso en OSCP

- Escanear redes internas sin redirigir puertos manualmente
- Usar herramientas como `nmap`, `smbclient`, `winexe`, `curl` directamente sin `proxychains`
- Enumeración masiva desde Kali como si estuvieras dentro de la red interna

---

## Verificación

Después de levantar el túnel, prueba con un ping o escaneo:
```bash
ping 192.168.100.10
nmap -sS -Pn -n 192.168.100.0/24
```

---
