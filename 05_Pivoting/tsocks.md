`tsocks` es una alternativa ligera a `proxychains` que permite enrutar aplicaciones TCP a través de un proxy SOCKS. Aunque menos versátil y menos mantenida, sigue siendo útil en entornos OSCP si `proxychains` no funciona como esperas.

---

## Instalación

```bash
sudo apt install tsocks
```

---

## Configuración

Edita el archivo principal:
```bash
sudo nano /etc/tsocks.conf
```

Ejemplo de configuración:
```
server = 127.0.0.1
server_type = 5
server_port = 1080
```

---

## Uso básico

```bash
tsocks <comando>
```

Ejemplos:
```bash
tsocks curl http://192.168.100.10

tsocks smbclient -L 192.168.100.10 -N
```

> No funciona con herramientas que usen raw sockets como `nmap -sS`

---

## Casos de Uso OSCP

- Ejecutar herramientas básicas sobre SOCKS proxy sin usar proxychains
- Escenarios donde `proxychains` da errores o tienes conflictos con su config
- Entornos con aplicaciones ligeras tipo `ftp`, `curl`, `wget`, `smbclient`, etc.

---

## Diferencias con `proxychains`

- `tsocks` es más limitado y menos compatible
- No permite múltiples proxies ni rotación
- Más simple y directo para comandos individuales

---

## Verificación

Comprueba con `tcpdump` o `netstat` que el tráfico pasa por el puerto 1080.

---
