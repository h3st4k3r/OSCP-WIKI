WhatWeb es una herramienta de reconocimiento web que identifica tecnologías, frameworks, CMS y servidores web con rapidez. Es ideal para la fase inicial de reconocimiento en OSCP, especialmente cuando se encuentra un servicio HTTP expuesto tras escaneos con Nmap o Masscan.

---

## Instalación

### En Kali Linux
WhatWeb viene preinstalado. Si no:
```bash
sudo apt install whatweb
```

### Desde GitHub
```bash
git clone https://github.com/urbanadventurer/WhatWeb.git
cd WhatWeb
sudo ruby whatweb --update
```

---

## Uso Básico

```bash
whatweb http://10.11.1.10
```

## Escaneo Silencioso

```bash
whatweb -q http://10.11.1.10
```

## Modo Verbose (más detalles)

```bash
whatweb -v http://10.11.1.10
```

## Escaneo de Lista de URLs

```bash
whatweb -i urls.txt -v > resultados.txt
```

## Modo Aggressive

```bash
whatweb -a 3 http://10.11.1.10
```

- `-a 3`: usa detección agresiva. Ojo: puede ser más ruidoso.

## Mostrar Plugins Detectados

```bash
whatweb -l
```

---

## Casos de Uso OSCP

- Detectar software expuesto vulnerable.
- Extraer encabezados HTTP, cookies, banners.
- Afinar tus ataques (específicos por CMS o tecnología).

## Buenas Prácticas

- Úsalo tras descubrir servicios HTTP con `nmap`.
- Combínalo con `nuclei`, `webanalyze` o `ffuf` para campañas más completas.
- No abusar de modo agresivo en entornos sensibles.

---
