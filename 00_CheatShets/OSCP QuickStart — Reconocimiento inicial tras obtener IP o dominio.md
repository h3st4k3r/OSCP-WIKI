Guía rápida para lanzar las acciones iniciales al recibir una IP o dominio en un entorno OSCP/CTF. No incluye comandos básicos; solo lo que realmente conviene ejecutar o preparar al instante.

---

## 1. Crear estructura base del objetivo

```bash
mkdir -p ~/oscp/targets/10.11.1.123/{nmap,www,loot,exploits}
cd ~/oscp/targets/10.11.1.123
```

---

## 2. Resolver nombre si es dominio

```bash
host target.htb
nslookup target.htb
```

Agregar a /etc/hosts:
```bash
echo "10.11.1.123 target.htb" | sudo tee -a /etc/hosts
```

---

## 3. Escaneo Nmap

Escaneo inicial:
```bash
nmap -sC -sV -Pn -oN nmap/init.txt 10.11.1.123
```

Full TCP scan:
```bash
nmap -p- -T4 --min-rate=1000 -oN nmap/allports.txt 10.11.1.123
```

Extraer puertos y escaneo detallado:
```bash
ports=$(grep -oP '\d+/tcp' nmap/allports.txt | cut -d '/' -f1 | tr '\n' ',' | sed 's/,$//')
nmap -sC -sV -p$ports -oN nmap/targeted.txt 10.11.1.123
```

---

## 4. Si hay web (puerto 80, 443, 8080, etc)

Fingerprint y reconocimiento:
```bash
whatweb http://10.11.1.123
webanalyze -host http://10.11.1.123
theharvester -d target.htb -b all
```

Fuzzing inicial:
```bash
gobuster dir -u http://10.11.1.123 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 40 -o loot/web.txt
```

Screenshot:
```bash
echo "http://10.11.1.123" | httpx -screenshot -sc -title -o loot/httpx.txt
```

---

## 5. DNS (si aplica)

```bash
dnsenum target.htb
dnsrecon -d target.htb
```

---

## 6. Subdominios (si aplica)

```bash
sublist3r -d target.htb -o loot/subs.txt
```

---

## 7. Shodan (si dominio o IP pública)

```bash
shodan host 10.11.1.123
```

---

## 8. Hosts vivos (si tienes /24)

```bash
fping -a -g 10.11.1.0/24 2>/dev/null
```

---

## 9. Escaneo rápido de puertos masivo

```bash
masscan -p1-65535 10.11.1.123 --rate=1000 -e tun0 -oG loot/masscan.gnmap
```

---

## 10. Si puerto 21, 25, 110, 139, 445, 3389...

Marcar para enumeración específica posterior (con sus herramientas por servicio)

---

## 11. Preparar servidor HTTP / SMB local

```bash
python3 -m http.server 8080
impacket-smbserver share $(pwd) -smb2support
```

---

## 12. Si descubrimos CMS o backend

```bash
whatweb, nuclei, cmsmap, wpscan, joomscan
```

---

## 13. Toma de notas

```bash
echo "[+] target.htb | 10.11.1.123" >> ~/oscp/index.txt
```

---
