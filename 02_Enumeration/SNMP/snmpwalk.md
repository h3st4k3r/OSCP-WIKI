`snmpwalk` permite consultar árboles de OIDs completos a través del protocolo SNMP. Es una herramienta poderosa para extraer grandes cantidades de información desde dispositivos con SNMP habilitado (routers, switches, impresoras, servidores). En OSCP es clave para sacar usuarios, procesos, interfaces, rutas y más.

---

## Instalación

```bash
sudo apt install snmp
```

---

## Uso Básico

```bash
snmpwalk -v1 -c public <IP>
```

- `-v1`: usa SNMP versión 1
- `-c public`: comunidad SNMP (por defecto suele ser `public`)

### Ejemplo:
```bash
snmpwalk -v1 -c public 10.11.1.23
```

---

## Uso por MIBs/OIDs Específicos

### Obtener información del sistema:
```bash
snmpwalk -v1 -c public <IP> 1.3.6.1.2.1.1
```

### Interfaces de red:
```bash
snmpwalk -v1 -c public <IP> 1.3.6.1.2.1.2.2.1.2
```

### Usuarios (depende del dispositivo):
```bash
snmpwalk -v1 -c public <IP> 1.3.6.1.4.1
```

---

## Exportar la Salida

```bash
snmpwalk -v1 -c public <IP> > snmp_full_output.txt
```

---

## Casos de Uso OSCP

- Ver rutas de red internas (`ipRouteTable`)
- Extraer nombres de host, sistema operativo y tiempo activo
- Ver interfaces, usuarios, procesos y servicios
- Encontrar contraseñas o rutas ocultas en banners SNMP

---

## Buenas Prácticas

- Confirmar la comunidad con `onesixtyone` primero
- No escanear OID completos si sabes lo que buscas: ve directo
- Usa `grep` para extraer info puntual (`grep -i user`, `grep -i passwd`, etc.)

---
