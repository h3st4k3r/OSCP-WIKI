`imapenum` es una herramienta útil para enumerar cuentas válidas en un servidor IMAP (puerto 143) mediante respuesta de error. En entornos OSCP, puede ayudarte a identificar usuarios válidos para futuros ataques como password spraying o explotación de correo web.

---

## Instalación

`imapenum` no siempre viene en Kali por defecto. Puedes instalarlo desde el repo:

```bash
git clone https://github.com/stasinopoulos/imapenum.git
cd imapenum
sudo chmod +x imapenum.rb
```

Requiere Ruby:
```bash
sudo apt install ruby
```

---

## Uso Básico

```bash
./imapenum.rb -U users.txt -w test -i <IP> -p 143
```

- `-U`: diccionario de usuarios
- `-w`: contraseña fija (puede ser falsa, se usa solo para provocar respuesta)
- `-i`: IP del servidor objetivo
- `-p`: puerto IMAP (143 por defecto)

El objetivo es identificar qué usuarios existen por su comportamiento de error:
- **Usuario no válido**: error genérico
- **Usuario válido + contraseña incorrecta**: error distinto

---

## Ejemplo

```bash
./imapenum.rb -U /usr/share/seclists/Usernames/top-usernames-shortlist.txt -w fakepass -i 10.11.1.20 -p 143
```

---

## Validar Manualmente con Telnet

```bash
telnet <IP> 143

a login usuario1 fakepass
```

Respuestas típicas:
- `NO LOGIN failed.` → usuario puede existir
- `BAD` → formato incorrecto o usuario no existe

---

## Casos de Uso OSCP

- Identificar usuarios válidos para usar en ataques contra otros servicios (SSH, SMB...)
- Detección de cuentas activas expuestas en correo
- Combinación con password spraying si se permite login (usar `hydra` o `ncrack`)

---

## Buenas Prácticas

- No hacer bruteforce directo contra IMAP salvo que esté permitido
- Correlacionar usuarios válidos con otros vectores
- Mantener bajo el número de intentos para evitar lockout

---