`wpscan` es la herramienta de referencia para analizar sitios WordPress. Permite enumerar usuarios, plugins, temas, vulnerabilidades conocidas y credenciales débiles. En OSCP, es útil cuando detectas un WordPress como vector web para el foothold.

---

## Instalación

```bash
sudo apt install wpscan
```

> Si da problemas de API, crea una cuenta gratuita en https://wpscan.com y obtén tu API key para vulnerabilidades.

---

## Uso Básico

```bash
wpscan --url http://<IP>/wordpress/ --enumerate u
```

- `--enumerate u`: enumera usuarios
- `--url`: URL del sitio WordPress

---

## Otras Opciones Útiles

### Enumerar plugins y vulnerabilidades (requiere API key):
```bash
wpscan --url http://<IP>/wordpress/ --enumerate vp --api-token <API_KEY>
```

### Fuerza bruta de login:
```bash
wpscan --url http://<IP>/wordpress/ --passwords rockyou.txt --usernames admin
```

### Especificar agente y proxy:
```bash
wpscan --url http://<IP>/wordpress/ --proxy http://127.0.0.1:8080 --user-agent "Mozilla/5.0"
```

---

## Resultados

WPScan detectará:
- Usuarios válidos
- Plugins y versiones
- Temas
- Vulnerabilidades asociadas
- Archivos sensibles

---

## Casos de Uso OSCP

- Identificar usuarios para fuerza bruta con `hydra`
- Detectar plugins desactualizados con CVEs explotables
- Enumerar archivos de backup, debug o configuración

---

## Buenas Prácticas

- Siempre validar que es WordPress antes (con `whatweb`, `cmsmap`...)
- Usar `--random-user-agent` para evitar detección
- Guardar resultados con `--output informe.txt`

---
