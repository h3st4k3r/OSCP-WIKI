`snmp-check` es una herramienta de enumeración SNMP que permite obtener información detallada de un host usando una comunidad SNMP válida. Es útil en OSCP cuando encuentras el puerto UDP/161 abierto y quieres recolectar información de red, usuarios, procesos, etc.

---

## Instalación

```bash
sudo apt install snmp-check
```

---

## Uso Básico

```bash
snmp-check -c public <IP>
```

- `-c`: comunidad SNMP (por defecto suele ser `public`)
- `<IP>`: IP del objetivo

### Ejemplo:
```bash
snmp-check -c public 10.11.1.23
```

---

## Información que Puede Mostrar

- Nombre del host y descripción
- Lista de interfaces de red
- Rutas IP
- Usuarios activos
- Procesos en ejecución
- Shares
- Servicios

---

## Opciones Útiles

```bash
snmp-check -t 10.11.1.23 -c public -v 1
```

- `-t`: objetivo
- `-v`: versión SNMP (normalmente 1)

---

## Casos de Uso OSCP

- Descubrir hosts con información sensible expuesta por SNMP
- Enumerar usuarios del sistema
- Detectar procesos y servicios vulnerables
- Ver interfaces y rutas internas de red

---

## Buenas Prácticas

- Validar previamente la comunidad con `onesixtyone`
- Complementar con `snmpwalk` para más granularidad
- Revisar cuidadosamente cada sección del output: a menudo hay oro

---
