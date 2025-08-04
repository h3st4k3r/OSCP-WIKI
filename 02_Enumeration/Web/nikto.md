`nikto` es una herramienta de escaneo web enfocada en la detección de vulnerabilidades conocidas, configuraciones inseguras, archivos expuestos y otros problemas comunes en servidores web. En OSCP, es útil como escaneo inicial para recolectar información rápida de cualquier objetivo HTTP/HTTPS.

---

## Instalación

```bash
sudo apt install nikto
```

---

## Uso Básico

```bash
nikto -h http://<IP>
```

### Ejemplo:
```bash
nikto -h http://10.11.1.23
```

---

## Opciones Útiles

- `-h`: host objetivo (URL o IP)
- `-p`: puerto específico
- `-ssl`: fuerza uso de HTTPS
- `-Tuning`: escaneo personalizado por tipo de test
- `-o`: archivo de salida
- `-Format`: formato del output (txt, html, xml)

### Escaneo HTTPS en puerto 443:
```bash
nikto -h https://10.11.1.23 -p 443 -ssl
```

### Salida a archivo:
```bash
nikto -h http://10.11.1.23 -o resultados_nikto.txt -Format txt
```

---

## Casos de Uso OSCP

- Detección de archivos `.bak`, `.txt`, `.php~` expuestos
- Identificación de versiones vulnerables de Apache, PHP, etc.
- Detectar formularios inseguros, headers mal configurados, directorios interesantes

---

## Buenas Prácticas

- Ejecutar Nikto después de `whatweb` o `webanalyze`
- No abusar de la opción `-Tuning 9` (es agresiva)
- Combinar con fuzzers o `gobuster/ffuf` tras descubrir rutas interesantes

---
