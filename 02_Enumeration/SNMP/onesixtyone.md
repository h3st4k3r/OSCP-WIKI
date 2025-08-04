`onesixtyone` es una herramienta rápida para escaneo de servicios SNMP (UDP/161) en grandes rangos. En OSCP se usa para detectar dispositivos que responden a SNMP y obtener información útil con otras herramientas como `snmpwalk`.

---

## Instalación

```bash
sudo apt install onesixtyone
```

---

## Uso Básico

```bash
onesixtyone -c community.txt <IP>
```

- `-c`: archivo con posibles comunidades SNMP (por defecto `public`, `private`...)

### Ejemplo:
```bash
onesixtyone -c /usr/share/seclists/Discovery/SNMP/snmp-onesixtyone.txt 10.11.1.0/24
```

> Prueba con comunidad `public` siempre primero. Es la más común.

---

## Formato de community.txt

Ejemplo de contenido:
```
public
private
test
monitor
```

---

## Interpretación de Resultados

Salida típica:
```
[10.11.1.23] v1 public
```
Indica que el host 10.11.1.23 responde con SNMPv1 usando comunidad `public`.

---

## Casos de Uso OSCP

- Detección rápida de servicios SNMP abiertos en red interna
- Obtener comunidades SNMP válidas (para usar luego en `snmpwalk`)
- Identificar routers, switches, impresoras o servidores mal configurados

---

## Buenas Prácticas

- Lanza `onesixtyone` antes que `snmpwalk` para ver qué hosts responden
- Usa diccionarios razonables, no abusivos
- Complementa con `nmap -sU -p161` y `snmp-check`

---
