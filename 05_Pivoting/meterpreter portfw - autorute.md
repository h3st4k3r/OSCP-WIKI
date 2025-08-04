En entornos OSCP donde el uso de Metasploit está permitido (máquina de bono o entorno lab), puedes aprovechar las funciones internas de Meterpreter para pivoting.

Las dos funciones clave son:
- `portfwd`: redirige puertos desde tu máquina local al objetivo a través de la sesión Meterpreter
- `autoroute`: enruta tráfico hacia redes internas accesibles por la máquina comprometida

---

## `portfwd` – Redirección de Puertos

```bash
portfwd add -l <puerto_local> -p <puerto_remoto> -r <ip_objetivo>
```

- `-l`: puerto local en tu Kali
- `-p`: puerto remoto en la red interna
- `-r`: IP interna accesible desde la máquina comprometida

### Ejemplo:

Tienes sesión Meterpreter en una máquina que puede ver `192.168.100.10:3389` (RDP):
```bash
portfwd add -l 13389 -p 3389 -r 192.168.100.10
```

Desde tu Kali:
```bash
rdesktop 127.0.0.1:13389
```

---

## `portfwd` – Ver, eliminar

Ver puertos activos:
```bash
portfwd list
```

Eliminar:
```bash
portfwd delete -l 13389
```

---

## `autoroute` – Acceso a redes internas

Permite enrutar tráfico a través de la máquina comprometida si tiene acceso a otra red:
```bash
run post/multi/manage/autoroute RHOST=192.168.100.0 NETMASK=255.255.255.0
```

O bien:
```bash
run autoroute -s 192.168.100.0/24
```

Ver rutas añadidas:
```bash
run autoroute -p
```

---

## Requiere el uso de `route` y `proxychains` para aprovecharlo

Una vez has hecho `autoroute`, puedes iniciar un socks proxy:
```bash
run auxiliary/server/socks_proxy
```

Y luego usar `proxychains` en tu máquina Kali para hacer nmap, curl, smbclient, etc. contra la red interna.

---

## Casos de Uso en OSCP

- Pivotear hacia una segunda red interna
- Escanear máquinas inaccesibles directamente
- Exfiltrar datos o lanzar shells reversos desde sistemas internos

---

## Buenas prácticas

- No abuses de Metasploit: solo se permite en máquinas específicas
- Asegúrate de limpiar rutas y proxies si terminas la sesión
- Documenta cada salto y puerto usado

---
