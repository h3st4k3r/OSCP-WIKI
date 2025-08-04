
Nuclei es un escáner de vulnerabilidades basado en plantillas, rápido y altamente personalizable. Ideal para la fase de enumeración y explotación en pruebas de penetración como OSCP (especialmente en máquinas con servicios HTTP expuestos).

## Instalación

```bash
sudo apt install golang
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

Agregar `$HOME/go/bin` al PATH si no está:
```bash
echo 'export PATH=$PATH:$HOME/go/bin' >> ~/.bashrc
source ~/.bashrc
```

## Descargar Plantillas

```bash
nuclei -update
```

Para plantillas más agresivas (solo si tienes permiso):
```bash
nuclei -ut -ud templates/ --token YOUR_GITHUB_TOKEN
```

## Escaneo Básico

```bash
nuclei -u http://10.11.1.10
```

## Escaneo Masivo

```bash
cat urls.txt | nuclei -t cves/ -o nuclei_results.txt
```

- `urls.txt`: lista de URLs descubiertas con herramientas como `ffuf`, `feroxbuster`, etc.
- `-t cves/`: usa solo plantillas CVE.

## Filtros por Severidad

```bash
nuclei -l urls.txt -s critical,high,medium -o filtered.txt
```

## Escaneo por Categoría

```bash
nuclei -l urls.txt -t exposures/ -o exp.txt
```

## Modo Silencioso + JSON

```bash
nuclei -l urls.txt -json -silent -o report.json
```

## Buenas Prácticas en OSCP

- Filtrar resultados falsos positivos.
- Usar después de enumerar servicios HTTP con `nmap`, `whatweb`, `ffuf`, etc.
- Nunca escanear fuera del entorno autorizado.

## Ejemplo de Pipeline Web Recon

```bash
nmap -p80,443,8080 -sV -oG webscan.txt 10.11.1.0/24
cat webscan.txt | grep open | awk '{print $2}' | while read ip; do
  echo "http://$ip" >> urls.txt
  echo "https://$ip" >> urls.txt
done
nuclei -l urls.txt -s critical,high -o nuclei_web.txt
```

---
