`fierce` es una herramienta clásica de reconocimiento DNS, diseñada para mapear infraestructuras ocultas a través de nombres públicos. Puede revelar subdominios mal configurados, transferencias de zona abiertas, y rangos internos filtrados por errores de configuración DNS.

Disponible por defecto en Kali Linux.

---

## ¿Para qué sirve?

- Descubrir subdominios accesibles públicamente.
- Detectar posibles IPs internas filtradas.
- Probar transferencias de zona.
- Auditar dominios grandes con múltiples registros dispersos.

---

## Ejecución básica

```
fierce -dns dominio.com
```

Esto:

- Enumera subdominios conocidos.
- Intenta resolverlos.
- Muestra IPs públicas o internas.

---

## Parámetros útiles

```
-dns       Dominio objetivo (obligatorio)
-wordlist  Lista personalizada de subdominios
-ns        Servidor DNS a consultar
-delay     Tiempo entre peticiones (útil para no ser bloqueado)
-file      Guarda el resultado en un archivo
-search    Usa Google para encontrar subdominios (experimental)
```

---

## Ejemplo práctico

```
fierce -dns empresa.local -wordlist /usr/share/seclists/Discovery/DNS/namelist.txt -file fierce_output.txt
```

---

## Salida típica

```
Found subdomain: vpn.empresa.local -> 10.10.10.1
Found subdomain: dev.empresa.local -> 172.16.0.23
Attempting zone transfer on ns1.empresa.local... Failed.
```

En este ejemplo se detectan IPs internas — una pista de mal diseño.

---

## Limitaciones

- No resuelve si los DNS no responden correctamente.
- No soporta muchos formatos de salida (solo texto).
- Google search está obsoleta o muy lenta.

---

## Cuándo usarla

- Justo después de `dnsenum` o `dnsrecon`, como paso complementario.
- Cuando hay sospecha de exposición de red interna.
- En auditorías de dominios complejos.

---

## Consejo práctico

Guarda la salida y combínala con herramientas como `amass` o `nmap` para verificar los hallazgos:

```
cat fierce_output.txt | grep -Eo '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' | sort -u | while read ip; do nmap -sV $ip; done
```

---

