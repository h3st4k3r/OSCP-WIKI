`CMSmap` es una herramienta de análisis de seguridad automatizado para sistemas de gestión de contenidos (CMS) como WordPress, Joomla y Drupal. En OSCP es útil para detectar configuraciones inseguras, vulnerabilidades y credenciales por defecto en aplicaciones web comunes.

---

## Instalación

```bash
git clone https://github.com/Dionach/CMSmap.git
cd CMSmap
sudo pip3 install -r requirements.txt
```

---

## Uso Básico por CMS

### WordPress
```bash
python3 cmsmap.py http://<IP>/wordpress/
```

### Joomla
```bash
python3 cmsmap.py http://<IP>/joomla/ -t joomla
```

### Drupal
```bash
python3 cmsmap.py http://<IP>/drupal/ -t drupal
```

---

## Opciones Útiles

- `-t`: tipo de CMS (wordpress, joomla, drupal)
- `-A`: escaneo agresivo (prueba de usuarios, contraseñas, plugins)
- `-u <usuario>`: usuario para fuerza bruta
- `-p <diccionario>`: diccionario de contraseñas

### Ejemplo fuerza bruta en WordPress
```bash
python3 cmsmap.py http://10.11.1.23/wordpress/ -t wordpress -u admin -p /usr/share/wordlists/rockyou.txt
```

---

## Resultados

CMSmap mostrará:
- Usuarios válidos
- Contraseñas exitosas
- Plugins instalados
- Versiones del CMS
- Vulnerabilidades conocidas (si se detectan)

---

## Casos de Uso OSCP

- Detección de credenciales por defecto o vulnerabilidades conocidas
- Reconocimiento de plugins/temas expuestos para WordPress
- Identificación de instalaciones de CMS mal configuradas

---

## Buenas Prácticas

- Confirmar el CMS antes (con `whatweb`, `webanalyze`, `wappalyzer`...)
- No usar `-A` en entornos donde puedes ser detectado fácilmente
- Complementar con `wpscan`, `droopescan`, `joomscan`, etc.

---
