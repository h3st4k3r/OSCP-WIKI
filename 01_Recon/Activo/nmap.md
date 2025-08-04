
Este apartado se centra exclusivamente en el uso de **Nmap**, una de las herramientas más potentes y versátiles que vienen preinstaladas en Kali Linux. Aprender a dominar Nmap es clave para el OSCP y para cualquier análisis serio.

---

## ¿Qué es Nmap?

Nmap (Network Mapper) es una herramienta de código abierto para descubrir hosts y servicios en una red mediante el envío de paquetes y el análisis de las respuestas.

---

## Escaneos comunes

### Escaneo completo de puertos TCP (todos los puertos)

```
nmap -sS -Pn -T4 -p- --min-rate=5000 -oN full_tcp.txt <objetivo>
```

- `-sS`: escaneo SYN (rápido y sigiloso)
- `-Pn`: sin ping, asume que el host está activo
- `-p-`: escanea todos los puertos (1-65535)
- `--min-rate`: velocidad mínima de envío de paquetes

---

### Escaneo de servicios y scripts NSE

```
nmap -sC -sV -p<puertos> -oN services.txt <objetivo>
```

- `-sC`: scripts NSE por defecto
- `-sV`: detección de versiones

> Primero haz el escaneo completo y luego usa los puertos abiertos con este segundo paso.

Ejemplo completo:

```
nmap -sS -Pn -T4 -p- --min-rate=5000 -oN full.txt <ip>
puertos=$(grep open full.txt | cut -d '/' -f1 | tr '\n' ',' | sed 's/,$//')
nmap -sC -sV -p$puertos -oN services.txt <ip>
```

---

### Escaneo rápido (top 1000 puertos TCP)

```
nmap -sS -Pn -T4 --top-ports 1000 -oN top1000.txt <objetivo>
```

### Escaneo UDP (más lento)

```
nmap -sU -T4 --top-ports 100 -oN udp_top100.txt <objetivo>
```

>  Requiere privilegios elevados y mucho tiempo.

---

## Scripts NSE útiles

### Buscar vulnerabilidades conocidas (requiere plugin `vulners`)

```
nmap -sV --script vulners -p<puertos> -oN cves.txt <objetivo>
```

### Buscar servicios FTP anónimos:

```
nmap -p21 --script=ftp-anon <objetivo>
```

### SMB enum básico:

```
nmap -p445 --script=smb-enum-shares,smb-enum-users <objetivo>
```

### HTTP Headers y títulos:

```
nmap -p80,443 --script=http-title,http-headers <objetivo>
```

---

## Trucos útiles

### Omitir DNS (cuando hay problemas de resolución)

```
nmap -n <objetivo>
```

### Salida en diferentes formatos:

```
nmap -oN salida.txt -oX salida.xml <objetivo>
```

### Escanear múltiples objetivos:

```
nmap -iL lista.txt -oN resultado.txt
```

---
