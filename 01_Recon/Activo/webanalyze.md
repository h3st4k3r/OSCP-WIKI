Webanalyze es una herramienta ligera escrita en Go que permite identificar tecnologías utilizadas en aplicaciones web (similar a Wappalyzer). Muy útil durante la fase de reconocimiento web en el OSCP.

---

## Instalación

### Opción 1: Usar el binario

```bash
wget https://github.com/janmarek/webanalyze/releases/latest/download/webanalyze-linux-amd64.tar.gz
tar -xvzf webanalyze-linux-amd64.tar.gz
sudo mv webanalyze /usr/local/bin/
```

### Opción 2: Compilar desde código

```bash
git clone https://github.com/janmarek/webanalyze.git
cd webanalyze
go build
sudo mv webanalyze /usr/local/bin/
```

## Descargar el archivo de tecnologías (requerido)

```bash
webanalyze -update
```

Esto descargará el archivo `apps.json` necesario para detectar tecnologías.

---

## Uso Básico

```bash
webanalyze -host http://10.11.1.10
```

## Escaneo Masivo desde Lista de URLs

```bash
cat urls.txt | webanalyze -apps apps.json -crawl -hosts - > tech_results.txt
```

## Flags Útiles

- `-crawl`: sigue redirecciones y analiza contenido cargado dinámicamente.
- `-hosts`: permite escanear múltiples dominios desde stdin.
- `-apps apps.json`: usa archivo local (más rápido y offline).

---

## Casos de Uso OSCP

- Detectar versiones vulnerables de CMS, frameworks o librerías JS.
- Elegir payloads más efectivos para fuzzing o explotación (gobuster, nuclei).
- Filtrar tecnologías específicas para campañas dirigidas (ej: sólo Joomla).

---

## Ejemplo de Flujo

```bash
# Obtener subdominios
python sublist3r.py -d ejemplo.com -o sub.txt

# Resolver y verificar
for d in $(cat sub.txt); do echo http://$d; done > urls.txt

# Analizar tecnologías
cat urls.txt | webanalyze -apps apps.json -crawl -hosts - > webtech.txt
```

---
