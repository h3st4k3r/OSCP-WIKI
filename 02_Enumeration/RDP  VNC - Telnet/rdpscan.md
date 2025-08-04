`rdpscan` es una herramienta ligera diseñada para detectar si un host es vulnerable a la falla de ejecución remota en RDP conocida como BlueKeep (CVE-2019-0708). También permite identificar servicios RDP activos en una red durante la fase de enumeración en OSCP.

---

## Instalación

### 1. Clonar el repositorio
```bash
git clone https://github.com/robertdavidgraham/rdpscan.git
cd rdpscan
make
```

Esto generará un binario llamado `rdpscan`.

> Requiere `make` y entorno Linux. También puedes usar el binario precompilado si estás en Windows o WSL.

---

## Uso Básico

```bash
./rdpscan <IP>
```

Este comando analiza si la IP especificada tiene el puerto RDP abierto y si es vulnerable a BlueKeep.

---

## Escanear Múltiples Hosts

```bash
./rdpscan -f ips.txt
```

- `ips.txt` debe contener una IP por línea.

---

## Interpretar Resultados

- `RDP Supported`: el puerto 3389 está abierto y responde
- `VULNERABLE`: potencialmente vulnerable a BlueKeep (ojo con falsos positivos)
- `SAFE`: parche aplicado o RDP no expuesto

---

## Casos de Uso OSCP

- Detectar servicios RDP activos durante reconocimiento interno
- Confirmar exposición de RDP en máquinas Windows
- Verificar máquinas vulnerables a BlueKeep en labs tipo OSCP

---

## Buenas Prácticas

- Usar después de confirmar que el puerto 3389 está abierto (`nmap -p3389`)
- No confiar ciegamente en la vulnerabilidad reportada: requiere validación manual
- Complementar con herramientas como `xfreerdp` para intentar conexión

---

### Alternativas
Si `rdpscan` no funciona en tu sistema, puedes usar:
- `nmap -p3389 --script rdp*` para scripts NSE
- `xfreerdp /v:<IP>` para conexión real

---
