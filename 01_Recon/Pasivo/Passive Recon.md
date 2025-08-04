
Este apartado incluye técnicas y herramientas para obtener información del objetivo sin interactuar directamente con él. Ideal para preparar ataques sin levantar alertas.

---

## WHOIS y DNS

```
whois domain.com
nslookup domain.com
dig domain.com ANY +noall +answer
dig AXFR @ns1.domain.com domain.com
```

## Motores de Búsqueda (Google Dorking)

```
site:domain.com
intitle:index.of domain.com
filetype:pdf domain.com
```

## Certificados y Subdominios

```
curl -s https://crt.sh/?q=%.domain.com&output=json | jq .
assetfinder --subs-only domain.com
amass enum -passive -d domain.com
subfinder -d domain.com -all
```

## Correos y Brechas

```
theHarvester -d domain.com -b all
# También útil: netlas.io, hunter.io, dehashed.com
```

## Fingerprinting desde fuentes abiertas

```
curl -s http://<IP> | strings | grep -iE 'powered by|version|server'
```

## Metadatos de documentos públicos

```
docx2txt file.docx -
exiftool file.pdf
```

## Recursos Web Útiles (manual)

- https://shodan.io
- https://censys.io
- https://netlas.io
- https://crt.sh
- https://publicwww.com
---