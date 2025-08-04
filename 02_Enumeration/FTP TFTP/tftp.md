TFTP (Trivial File Transfer Protocol) opera por UDP en el puerto 69 y no requiere autenticación. Es común encontrarlo mal configurado en entornos antiguos o embebidos. Su simplicidad lo hace un objetivo clave durante OSCP.

---

## Detección con Nmap

```bash
nmap -sU -p69 --script=tftp-enum <IP>
```

> Es UDP, por lo tanto usa `-sU`. Añade `-Pn` si no responde a ping.

---

## Conexión Manual con Cliente TFTP

```bash
tftp <IP>
```

Una vez dentro:

```text
tftp> get test.txt
tftp> get ../../windows/win.ini
tftp> quit
```

No hay comandos de listado (`ls`), así que debes adivinar o usar diccionarios.

---

## Fuerza Bruta de Archivos (con script)

### Script Bash simple:
```bash
for file in $(cat wordlist.txt); do
  echo "get $file" | tftp <IP> && echo "[+] $file exists"
done
```

Usa diccionarios como:
- `/usr/share/wordlists/dirb/common.txt`
- Custom: `passwd`, `config.txt`, `win.ini`, `backup.tar`, etc.

---

## Usar atftp (cliente alternativo más robusto)

```bash
sudo apt install atftp
atftp --verbose <IP>
get config.txt
```

---

## Casos de Uso OSCP

- Descarga de archivos críticos sin autenticación.
- Acceso a backups, configuraciones o scripts.
- Descubrir rutas internas de sistemas Windows o Linux.

---

## Buenas Prácticas

- Intentar primero rutas conocidas: `/etc/passwd`, `win.ini`, `config.txt`, `backup.zip`.
- Documentar todo lo que puedas recuperar con hash + fecha.
- No subir archivos (`put`) en entornos controlados salvo que esté permitido.

---