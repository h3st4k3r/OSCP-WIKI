`httprobe` es una herramienta sencilla y rápida escrita en Go, diseñada para tomar una lista de hosts y verificar qué dominios tienen servicios HTTP o HTTPS activos. Es especialmente útil en fases de reconocimiento activo cuando se han recolectado muchos subdominios y queremos filtrar los que son accesibles por web.

---

## ¿Para qué sirve?

- Verificar automáticamente si un dominio o subdominio responde por HTTP o HTTPS.
- Comprobar rápidamente múltiples hosts sin necesidad de escanear puertos manualmente.
- Filtrar solo servicios web válidos para pruebas posteriores (gobuster, nikto, etc).

---

## Instalación

En Kali Linux puedes instalarlo con:

```
go install github.com/tomnomnom/httprobe@latest
```

Y añadir `$HOME/go/bin` a tu PATH si no lo has hecho:

```
export PATH=$PATH:$HOME/go/bin
```

---

## Uso básico

```
cat hosts.txt | httprobe
```

Esto leerá todos los dominios del fichero `hosts.txt` y mostrará solo los que respondan por HTTP o HTTPS.

Ejemplo:

```
$ cat hosts.txt
admin.domain.com
test.domain.com
mail.domain.com

$ cat hosts.txt | httprobe
http://admin.domain.com
https://test.domain.com
```

---

## Flags útiles

```
-c            Número de conexiones simultáneas (por defecto: 50)
-p            Puertos personalizados (ej: "80,8080,443")
-method       Método HTTP (GET por defecto)
-tlstimeout   Timeout para SSL/TLS handshake
```

---

## Ejemplo con puertos personalizados

```
cat hosts.txt | httprobe -p http:8080 -p https:8443
```

Este comando probará los puertos 8080 y 8443 en lugar de los estándares.

---

## Combinaciones típicas en flujo de trabajo

```
cat all_subs.txt | sort -u | httprobe > live_webs.txt
```

Esto filtra y guarda solo los subdominios con respuesta web activa. Luego puedes usar `gobuster`, `nuclei` o `whatweb` sobre ellos:

```
cat live_webs.txt | while read url; do whatweb $url; done
```

---

## Ventajas

- Extremadamente rápido.
- Muy útil para grandes volúmenes de subdominios (output de amass, subfinder, etc).
- Permite focalizar pruebas posteriores.

---

## Limitaciones

- No detecta aplicaciones que responden con errores personalizados (403, 503).
- No incluye cabeceras o fingerprinting (usa whatweb para eso).

---

## Cuándo usarlo

- Justo después de herramientas de subdomain discovery (`subfinder`, `amass`, `assetfinder`, etc).
- Antes de `gobuster`, `dirsearch`, `nuclei`, `nikto` o pruebas manuales.

---
