Estos tres comandos básicos proporcionan información clave sobre el entorno comprometido. Son totalmente válidos y necesarios en OSCP para orientar tu escalada de privilegios.

---

## 1. `uname -a`

```bash
uname -a
```

Muestra información del kernel:
```
Linux victim 4.4.0-21-generic #37-Ubuntu SMP x86_64 GNU/Linux
```

### ¿Por qué importa?
- Versión del kernel → Exploits locales posibles
- Arquitectura (`x86_64`, `i686`...)
- Distro aproximada

> Usa `searchsploit` o `exploitdb` para ver si esa versión tiene exploits conocidos:
```bash
searchsploit Linux Kernel 4.4
```

---

## 2. `id`

```bash
id
```

Muestra usuario, UID, GID y grupos:
```
uid=1000(user) gid=1000(user) groups=1000(user),27(sudo)
```

### ¿Por qué importa?
- Saber si el usuario actual está en grupos especiales: `sudo`, `adm`, `docker`, `lxd`, etc.
- `uid=0` = ya eres root

---

## 3. `env`

```bash
env
```

Muestra variables de entorno:

```
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
SHELL=/bin/bash
PWD=/home/user
HOME=/home/user
```

### ¿Por qué importa?
- Revisa si hay rutas personalizadas en `PATH`
- Algunas vulnerabilidades de `sudo` dependen de cómo esté configurado `PATH`
- Variables como `LD_PRELOAD`, `LD_LIBRARY_PATH` pueden ser vectores

---

## Casos de Uso OSCP

- Determinar si hay exploit de kernel local aplicable (`uname`)
- Ver si tienes acceso a `sudo` o `docker` (`id`)
- Identificar oportunidades de path hijacking o script injection (`env`)

---

## Buenas Prácticas

- Siempre empieza con estos tres comandos tras comprometer un Linux
- Combínalos con `sudo -l`, `getcap` y `find` para avanzar
- Documenta versiones y grupos del usuario

---
