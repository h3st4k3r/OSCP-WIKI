
Shodan es un motor de búsqueda para dispositivos conectados a Internet. Mediante su API puedes realizar reconocimiento activo (dentro de límites legales y éticos) obteniendo información útil para OSCP, especialmente sobre servicios expuestos públicamente.

---

## Requisitos

- Tener una cuenta en https://account.shodan.io
- Obtener tu API Key desde https://account.shodan.io

---

## Instalación del Cliente CLI

```bash
pip install -U shodan
```

## Configurar la API Key

```bash
shodan init TU_API_KEY
```

---

## Búsquedas Básicas

### Buscar IP con información completa:
```bash
shodan host 10.11.1.10
```

### Buscar dispositivos con puerto 22 abierto:
```bash
shodan search "port:22"
```

### Buscar por servicio o software expuesto:
```bash
shodan search "apache"
shodan search "nginx country:ES"
```

### Buscar por organización o ASN:
```bash
shodan search "org:'Telefonica'"
```

---

## Uso Avanzado con Scripts

### Listar IPs de dispositivos con RDP expuesto:
```bash
shodan search --fields ip_str "port:3389" > rdp_targets.txt
```

### Búsqueda masiva de un rango:
```bash
shodan scan submit --priority 1 10.11.1.0/24
```

> Necesita cuenta de nivel Enterprise para scans activos. De lo contrario, usa `shodan host` individualmente.

---

## Integración con Scripts de Reconocimiento

```bash
for ip in $(cat targets.txt); do
    echo "[+] $ip"
    shodan host $ip
    echo "------"
done
```

### Parseo y filtrado JSON

```bash
shodan host 10.11.1.10 --raw | jq
```

---

## Casos de Uso OSCP

- Identificar software y versiones expuestas sin necesidad de escaneo.
- Correlacionar servicios detectados con vulnerabilidades conocidas.
- Confirmar si una máquina está pública o solo interna.

## Buenas Prácticas

- Nunca escanear o abusar fuera del entorno permitido.
- Respetar los Términos de Uso de Shodan.
- Usar `jq` o grep para extraer lo necesario y no depender de demasiada información externa.

---
