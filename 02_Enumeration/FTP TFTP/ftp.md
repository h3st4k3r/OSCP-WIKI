El protocolo FTP (puerto 21 TCP) es común en entornos OSCP y puede revelar accesos anónimos, archivos sensibles o credenciales reutilizadas. Esta guía cubre técnicas básicas y útiles para su enumeración.

---

## Detección Inicial con Nmap

```bash
nmap -p21 -sV --script=ftp-anon,ftp-bounce,ftp-syst,ftp-vsftpd-backdoor <IP>
```

## Conexión Manual con el Cliente FTP

```bash
ftp <IP>
```

Prueba usuario `anonymous` sin contraseña o con `anonymous@domain.com`:

```text
Name: anonymous
Password: (empty or anonymous@domain.com)
```

Una vez dentro:

```ftp
ls
cd <dir>
get <file>
```

## Enumeración con `nmap` + NSE

### Escaneo específico
```bash
nmap -p21 --script=ftp-* <IP>
```

### Scripts útiles:
- `ftp-anon`: detecta acceso anónimo
- `ftp-bounce`: prueba vulnerabilidad de bounce attack
- `ftp-syst`: identifica sistema operativo remoto
- `ftp-vsftpd-backdoor`: detecta backdoor en vsFTPd 2.3.4

## Enumeración con `hydra` (Fuerza bruta de credenciales)

```bash
hydra -l ftp -P /usr/share/wordlists/rockyou.txt ftp://<IP>
```

O con usuario específico:
```bash
hydra -L users.txt -P passwords.txt ftp://<IP>
```

## Uso de `curl` para FTP

```bash
curl ftp://anonymous:anonymous@<IP>/ --list-only
curl ftp://user:pass@<IP>/archivo.txt -o archivo.txt
```

## Montar el servidor FTP remotamente (solo si es accesible y tiene permisos)

```bash
sudo mount -t ftpfs ftp://<IP>/ /mnt/ftp
```

> Requiere paquete `curlftpfs` y cuidado con permisos. No recomendado sin aislamiento.

## Casos de Uso OSCP

- Lectura de archivos `.txt`, `.conf`, `.bak`, etc.
- Acceso a scripts con credenciales duras o información sensible.
- Confirmación de acceso anónimo para escalar a otro servicio (ej: contraseñas FTP válidas para SSH).

## Buenas Prácticas

- Validar primero si hay acceso anónimo.
- Nunca modificar ni subir archivos.
- Siempre guardar hash del archivo (`sha256sum`) para pruebas.

---
