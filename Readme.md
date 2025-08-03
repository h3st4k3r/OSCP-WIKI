# OSCP-WIKI — Wiki Personal para la Preparación del OSCP

Este repositorio ha sido diseñado como un entorno de estudio estructurado, realista y altamente práctico para preparar el examen OSCP (Offensive Security Certified Professional), siguiendo una metodología manual, clara y centrada en lo esencial. No se incluyen herramientas o técnicas prohibidas en el examen, y se prioriza el uso de comandos, scripts y procedimientos aceptados por Offensive Security.

Nota: Durante el examen no se pueden usar automatizaciones, pero, para realizar CTFs si, para ello puedes encontrar este otro desarrollo y poder sacar información de forma automatizada resolviendo mucho antes los CTFs: https://github.com/h3st4k3r/ReconBreaker.

---

## Estructura del Repositorio

Cada carpeta representa una fase clave del ciclo de pentesting ofensivo, ordenada tal como se espera desarrollar una intrusión en el examen OSCP o en entornos similares.

### `00_CheatSheets`
Mini-guías de uso rápido para comandos o técnicas frecuentes. Pensado como acceso ultra-rápido bajo presión (priv esc, reverse shells, payloads).

### `01_Recon`
Reconocimiento activo y pasivo. Se documentan herramientas como `nmap`, `masscan`, `sublist3r`, `shodan`, `whatweb`, etc. Cada herramienta tiene su propio `.md` con sintaxis y ejemplos OSCP-style.

### `02_Enumeration`
Fase de enumeración por servicio: FTP, SMB, LDAP, RDP, Telnet, SNMP, etc. Enfoque directo, sin herramientas automáticas masivas. Casos de uso por protocolo.

### `03_Exploitation`
Herramientas y técnicas para explotar servicios identificados: uso de `msfconsole`, `evil-winrm`, `chisel`, shells reversas, servidores temporales (`socat`, `smbserver.py`), etc.

### `04_PrivEsc`
Escalada de privilegios local (Linux y Windows). Uso controlado de herramientas como `linpeas`, `winpeas`, `getcap`, `sudo -l`, `accesschk`, `gtfobins`, etc.

### `05_Pivoting`
Túneles, reenvíos de puertos, uso de `proxychains`, `plink`, `sshuttle`, `meterpreter portfwd`, etc. Guías prácticas para acceder a redes internas una vez comprometido un primer host.

### `06_BufferOverflow`
Pruebas controladas de Buffer Overflow: uso de `gdb`, `mona.py`, `immunity debugger`, `pwndbg`, `gef`, etc. Incluye crafting manual de exploits y fuzzing.

### `07_PostExploitation`
Extracción de información relevante tras comprometer un host: `wmic`, `tasklist`, `reg query`, `netstat`, `history`, `scp`, `rsync`, `strace`, `tcpdump`, etc. Pensado para consolidar el acceso, pivotar, y exfiltrar datos.

### `08_Notes-HTB`
Notas específicas de máquinas de Hack The Box o ejercicios similares. Espacio libre para práctica adicional y casos reales.

### `99_Tools_Install`
Scripts, instrucciones y dependencias necesarias para dejar el entorno de Kali listo para usar. Aquí van los comandos de instalación y configuración de herramientas frecuentes.

---

## Objetivo

Crear una guía operativa, offline y organizada, para resolver cualquier máquina OSCP sin depender de Internet. Todo debe poder ejecutarse, copiarse o adaptarse desde aquí. 

---

## Recomendaciones de uso

Si quieres utilizarlo para practicares recomendable:

- **Entrenar con esta wiki cerrada**: fuerza tu memoria, y solo consulta cuando sea necesario.
- **Actualizar constantemente**: si una herramienta cambia de sintaxis, reescribe su `.md`.
- **Evitar automatismos**: los apuntes están diseñados para guiar tu razonamiento, no para copiar y pegar sin pensar.

---

Este repositorio está vivo. Mejora, expande y adapta según tu experiencia. Que cada `.md` refleje lo que sabes hacer sin depender de nadie más.

