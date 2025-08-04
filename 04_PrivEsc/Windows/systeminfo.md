`systeminfo` es una herramienta nativa de Windows que muestra información detallada sobre el sistema operativo. En OSCP, se usa para identificar vulnerabilidades potenciales asociadas al sistema operativo, como exploits de escalada local conocidos.

---

## Uso Básico

```cmd
systeminfo
```

Esto mostrará información como:
- Versión de Windows y build exacta
- Nombre del sistema
- Tipo de sistema (x86 o x64)
- Fecha de instalación
- Parche más reciente instalado

---

## Ejemplo de salida relevante

```
OS Name:                   Microsoft Windows 10 Pro
OS Version:                10.0.18362 N/A Build 18362
System Type:               x64-based PC
Hotfix(s):                 KB4497165, KB4503308
```

---

## Casos de Uso en OSCP

- Comparar la versión del sistema con bases de datos de exploits:
```bash
searchsploit Windows 10 18362
```

- Determinar si es vulnerable a EternalBlue, MS17-010, PrintNightmare, etc.
- Comprobar si es un sistema desactualizado sin parches críticos
- Identificar arquitectura para elegir payloads adecuados (x86 vs x64)

---

## Extra: exportar la salida a archivo

```cmd
systeminfo > info.txt
```

Después puedes transferirlo a tu máquina para análisis más cómodo.

---

## Buenas Prácticas

- Ejecutar `systeminfo` justo después de obtener shell
- Cruzar la información con `accesschk`, `whoami`, y `findstr` para contexto completo
- No fiarte solo del nombre del SO, revisa la versión y build exacta

---
