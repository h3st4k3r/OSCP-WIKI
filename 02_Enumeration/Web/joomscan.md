`JoomScan` es una herramienta específica para escanear sitios Joomla en busca de vulnerabilidades conocidas, configuraciones inseguras, versiones y componentes peligrosos. En OSCP es útil para reconocer fallos comunes en CMS Joomla durante la fase de explotación web.

---

## Instalación

```bash
git clone https://github.com/OWASP/joomscan.git
cd joomscan
perl joomscan.pl
```

> Requiere `perl` instalado (viene por defecto en Kali Linux)

---

## Uso Básico

```bash
perl joomscan.pl -u http://<IP>/joomla/
```

---

## Opciones Útiles

- `-u`: URL objetivo
- `--ec`: omite comprobación de actualización
- `--ts`: no mostrar banner
- `--timeout <segundos>`: tiempo máximo de espera

### Ejemplo completo:
```bash
perl joomscan.pl -u http://10.11.1.23/joomla/ --ec --ts
```

---

## Qué Detecta

- Versión de Joomla
- Archivos y directorios inseguros
- Configuraciones por defecto
- Vulnerabilidades asociadas a versión/componentes

---

## Resultados

Se muestran directamente en consola: versión, fallos detectados y enlaces de referencia a exploits o CVEs conocidos.

---

## Casos de Uso OSCP

- Verificar versión Joomla y buscar CVEs conocidos
- Detectar credenciales por defecto o configuraciones peligrosas
- Identificar vectores iniciales para XSS, RCE o file inclusion

---

## Buenas Prácticas

- Confirmar que se trata de Joomla con `whatweb`, `wappalyzer` o `webanalyze`
- Usar junto a `cmsmap` o `droopescan` para mejores resultados
- Anotar versión y extensiones detectadas para fuzzing o CVE lookup

---
