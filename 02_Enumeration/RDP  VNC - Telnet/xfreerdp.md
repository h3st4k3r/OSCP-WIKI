`xfreerdp` es un cliente RDP de línea de comandos para conectarse a escritorios remotos Windows. En OSCP es útil cuando detectas el puerto 3389 abierto y quieres comprobar acceso con credenciales válidas o confirmar configuración insegura.

---

## Instalación

En Kali Linux ya está instalado. Si no:
```bash
sudo apt install freerdp2-x11
```

---

## Conexión Básica

```bash
xfreerdp /v:<IP> /u:<usuario> /p:<contraseña>
```

### Ejemplo
```bash
xfreerdp /v:10.11.1.100 /u:admin /p:admin123
```

---

## Opciones Útiles

- `/cert:ignore`: ignora advertencias de certificados
- `/dynamic-resolution`: ajusta resolución a pantalla
- `/clipboard`: habilita portapapeles
- `/drive:share,/ruta`: comparte carpeta local con la sesión remota

### Ejemplo con varias opciones
```bash
xfreerdp /v:10.11.1.100 /u:admin /p:admin123 /cert:ignore /dynamic-resolution /clipboard
```

---

## Conexión sin Contraseña (prueba rápida)

```bash
xfreerdp /v:10.11.1.100 /u:usuario
```

Si el servidor permite acceso sin contraseña o por contraseña vacía, se conectará.

---

## Brute Force con Hydra (para probar antes de usar xfreerdp)

```bash
hydra -t 4 -V -f -l administrator -P /usr/share/wordlists/rockyou.txt rdp://10.11.1.100
```

Una vez encontrada una combinación válida, úsala con `xfreerdp`.

---

## Casos de Uso OSCP

- Acceder gráficamente a una máquina Windows comprometida
- Extraer archivos usando portapapeles o carpetas compartidas
- Ver información de usuario en pantalla (correo, contraseñas, etc.)

---

## Buenas Prácticas

- Siempre añadir `/cert:ignore` para evitar bloqueos por SSL
- Graba la sesión si hay información sensible en pantalla
- No modifiques nada salvo que esté permitido

---
