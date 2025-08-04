`nbtscan` es una herramienta simple y rápida para enumerar nombres NetBIOS en una red local. Útil en OSCP para identificar nombres de máquina, grupos de trabajo, direcciones MAC y más, especialmente en redes Windows.

---

## Instalación

```bash
sudo apt install nbtscan
```

---

## Uso Básico

```bash
nbtscan 10.11.1.0/24
```

Esto escaneará la subred y mostrará:
- Nombre NetBIOS de la máquina
- Dirección IP
- Dirección MAC
- Grupo de trabajo o dominio

---

## Opciones Útiles

- `-v`: salida detallada
- `-r`: escaneo por rangos (más eficiente)
- `-f <file>`: escanear IPs desde archivo

### Ejemplo con más detalle:
```bash
nbtscan -v 10.11.1.0/24
```

---

## Interpretación de Resultados

- `[00h]`: nombre del host
- `[20h]`: indica que el host tiene servicios compartidos (File/Print)
- `[1Ch]`: controlador de dominio

---

## Casos de Uso OSCP

- Detectar máquinas Windows activas en red local
- Identificar hosts con shares sin necesidad de credenciales
- Obtener nombre del dominio o grupo de trabajo (útil para ataques SMB, LDAP...)

---

## Buenas Prácticas

- Usarlo como primer paso antes de enumeración SMB más pesada
- Complementar con `enum4linux-ng` y `smbclient`
- Anotar los nombres de host: suelen estar vinculados a cuentas reales o funciones (ej. `DC01`, `FSERVER`, etc.)

---
