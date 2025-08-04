`httpx` es una potente herramienta desarrollada por ProjectDiscovery para detectar de forma masiva hosts activos con servicios HTTP/HTTPS. Es más avanzada que `httprobe`, ya que permite añadir validaciones, cabeceras, guardar respuestas, seguir redirecciones, detectar tecnologías y mucho más.

---

## ¿Para qué sirve?

- Comprobar si un host tiene un servicio web activo.
- Detectar redirecciones, códigos de estado, tecnologías, títulos de página, etc.
- Extraer información útil de cabeceras HTTP.
- Guardar respuestas completas (body, headers).
- Trabajar a gran escala con miles de hosts en segundos.

---

## Instalación

En Kali Linux puedes instalarlo con:

```
go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
```

Asegúrate de tener `$HOME/go/bin` en el PATH:

```
export PATH=$PATH:$HOME/go/bin
```

---

## Uso básico

```
cat hosts.txt | httpx
```

Salida:

```
https://admin.site.com
http://dev.site.com:8080
```

---

## Flags útiles

```
-title           Muestra el título HTML de la página
-status-code     Muestra el código de estado HTTP
-content-length  Muestra la longitud de la respuesta
-follow-redirects Sigue redirecciones
-tech-detect     Detecta tecnologías (similar a whatweb)
-method          Especifica el método HTTP (GET, POST...)
-port            Fuerza un puerto específico
-path            Añade un path personalizado
```

---

## Ejemplo típico

```
cat subs.txt | httpx -title -status-code -tech-detect -content-length -follow-redirects
```

Salida:

```
https://intranet.empresa.com [200] [Apache Tomcat] ["Login Portal"] [5231]
https://dev.empresa.com [302] [nginx] ["Redirecting"] [0]
```

---

## Otras opciones avanzadas

- `-random-agent` → Añade un User-Agent aleatorio
- `-retries` → Número de reintentos por host
- `-timeout` → Timeout de conexión
- `-store-response-dir` → Guarda las respuestas completas (útil para análisis forense)

---

## Workflow típico

```
subfinder -d domain.com | httpx -silent -status-code -title -tech-detect -o live_hosts.txt
```

Luego usar `nuclei`, `whatweb`, o pruebas manuales solo sobre hosts detectados activos.

---

## Diferencias con httprobe

|Característica|httprobe|httpx|
|---|---|---|
|Velocidad|Alta|Alta|
|Redirecciones|No|Sí|
|Detección tecnologías|No|Sí|
|Códigos HTTP|No|Sí|
|Salida personalizable|No|Sí|
|Soporte TLS profundo|Limitado|Alto|

---

## Limitaciones

- A mayor número de flags, más lenta será la ejecución.
- Algunas WAFs pueden bloquear los probes si no se configuran bien los headers.

---

## Cuándo usarlo

- Como mejora directa respecto a `httprobe`.
- En flujos de reconocimiento masivo.
- Para filtrar dominios antes de usar `nuclei`, `dirsearch`, `nikto`, etc.