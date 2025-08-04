`aquatone` es una herramienta de reconocimiento que permite obtener una visión rápida y visual de múltiples aplicaciones web, realizando capturas de pantalla y recolectando metadatos HTTP desde una lista de dominios o IPs con servicios web expuestos.

---

## Instalación

En Kali Linux, puede no venir por defecto. Puedes instalarlo así:

```
sudo apt install chromium-driver -y
wget https://github.com/michenriksen/aquatone/releases/download/v1.7.0/aquatone_linux_amd64_1.7.0.zip
unzip aquatone_linux_amd64_1.7.0.zip
chmod +x aquatone
sudo mv aquatone /usr/local/bin/
```

Verifica que esté disponible:

```
aquatone -h
```

---

## Requisitos

- Tener instalado Chromium o Google Chrome (para las capturas).
    
- Lista previa de URLs o IPs con servicios HTTP/HTTPS detectados (ej. con `httpx`, `nmap`, etc.).
    

---

## Flujo de trabajo típico

### 1. Detectar servicios web

```
nmap -p80,443,8080 --open -oG webscan.txt <rango>
grep "/open" webscan.txt | cut -d ' ' -f2 > ips_web.txt
```

### 2. Verificar servicios vivos (httpx)

```
cat ips_web.txt | httpx -silent > web_urls.txt
```

### 3. Usar Aquatone

```
cat web_urls.txt | aquatone
```

Esto creará una carpeta `aquatone/` con:

- Capturas de pantalla por host.
- Respuesta HTTP.
- Metadatos.
- Informe final en HTML (`aquatone_report.html`).

---

## Opciones útiles

```
aquatone -ports 80,443,8080 -out aquatone_results
```

```
cat urls.txt | aquatone -scan-timeout 5000 -screenshot-timeout 10000
```

- `-ports`: define puertos HTTP(S) a analizar (por defecto incluye los comunes).
- `-out`: carpeta de salida.
- `-scan-timeout`: tiempo para detectar el servicio.
- `-screenshot-timeout`: tiempo de espera para tomar captura (útil en sitios lentos).

---

## Buenas prácticas

- Úsalo después de descubrir múltiples hosts web.
- Filtra resultados con `httpx` antes de usarlo.
- Puedes integrarlo en scripts para generar informes automáticos.
- Compatible con `gowitness`, aunque más visual y más sencillo.

---

## ¿Por qué usarlo?

- Rapidez para reconocer superficies web.
- Ideal en CTFs, OSCP y pentests internos.
- Permite priorizar sin revisar manualmente cada host.

---

## Alternativas

- `gowitness` (similar pero más raw)
- `eyewitness` (más completo, pero más pesado y lento)

---

## Ejemplo en contexto

```
naabu -host 10.10.10.10 -p 80,443 | httpx -silent | aquatone
```

Este comando encadena descubrimiento → verificación HTTP → capturas visuales, ideal para entornos OSCP.

---

## Archivos generados

```
aquatone/
├── aquatone_report.html
├── screenshots/
│   └── http_10.10.10.10.png
├── headers/
├── html/
└── json/
```

---