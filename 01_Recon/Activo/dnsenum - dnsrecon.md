`dnsenum` y `dnsrecon` son dos herramientas potentes para enumeración DNS activa. Permiten obtener registros, transferencias de zona, subdominios, servidores DNS e información contextual sobre un dominio objetivo. Ambas están incluidas en Kali Linux.

---

## dnsenum

### Descripción

Herramienta clásica para enumeración DNS. Muy útil en entornos donde la resolución de subdominios es crítica o se sospecha de transferencias de zona mal configuradas.

### Uso básico

```
dnsenum domain.com
```

### Opciones recomendadas

```
dnsenum domain.com \
  --enum \
  --noreverse \
  --threads 10 \
  --dnsserver 8.8.8.8 \
  --output dnsenum.xml
```

### Qué hace:

- Recolecta registros A, NS, MX, TXT, SOA.
- Intenta transferencia de zona.
- Busca subdominios comunes.
- Genera un XML como salida.

### Salida típica:

```
| Hostname       | IP           |
|----------------|--------------|
| www.domain.com | 192.168.1.1  |
| mail.domain.com| 192.168.1.2  |
```

---

## dnsrecon

### Descripción

Herramienta más moderna y modular. Soporta modos activos y pasivos, integración con Shodan y búsqueda de registros SPF, DKIM, DMARC.

### Uso básico

```
dnsrecon -d domain.com
```

### Modos disponibles

```
-d      Dominio objetivo
-ns     Servidor DNS específico
-a      Modo "agresivo" (bruteforce + zone transfer + reverse)
-b      Usa Bing para buscar subdominios
-z      Fuerza intento de transferencia de zona
-g      GeoIP
-j      Salida JSON
```

### Ejemplo completo:

```
dnsrecon -d domain.com -a -j dnsrecon_output.json
```

### Ejemplo de fuerza bruta de subdominios

```
dnsrecon -d domain.com -D /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t brt
```

### Qué hace:

- Enumera subdominios vía diccionario.
- Detecta mal configuraciones DNS.
- Realiza PTR lookups inversos.
- Exporta en JSON.

---

## Comparativa rápida

|Herramienta|Ventajas|Desventajas|
|---|---|---|
|dnsenum|Simple y rápida|No exporta JSON, algo antigua|
|dnsrecon|Modular y moderna|Requiere más opciones/configuración|

---

## Recomendaciones de uso

- Usa ambas herramientas para obtener más cobertura.
- Lanza primero `dnsrecon` en modo agresivo. Si no hay resultados, prueba `dnsenum` con diccionario.
- Interpreta bien los errores: algunas transferencias fallan por diseño.

------
