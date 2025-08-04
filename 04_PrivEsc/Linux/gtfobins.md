GTFOBins es una base de datos online que documenta formas de abusar de binarios Unix comunes para obtener ejecución de comandos, lectura/escritura de archivos, o incluso escalada a root, si están mal configurados (por ejemplo, con SUID o acceso vía `sudo`).

---

## Acceso

Web oficial: [https://gtfobins.github.io](https://gtfobins.github.io)

---

## Casos de Uso en OSCP

1. **SUID Binaries**: si un binario tiene el bit SUID y está listado en GTFOBins, puede ser explotable.
   - Ejemplo:
     ```bash
     find / -perm -4000 -type f 2>/dev/null
     ```
     Si aparece `/usr/bin/vim`, búscalo en GTFOBins.

2. **sudo -l**: si puedes ejecutar algún binario como root sin contraseña, búscalo también.
   - Ejemplo:
     ```bash
     sudo -l
     ```
     Si puedes correr `/usr/bin/less`, revisa su entrada en GTFOBins.

3. **Comandos disponibles**: si el sistema tiene restricciones de entorno (como shells limitadas), algunos binarios listados permiten escapar a una shell completa.

---

## Categorías en GTFOBins

Cada binario suele tener varias secciones:
- `Shell`: para spawnear una shell
- `SUID`: cómo abusar del binario si tiene bit SUID
- `sudo`: cómo usarlo si es ejecutable con sudo
- `File read/write`: leer o escribir ficheros
- `Limited SUID`: algunas formas requieren condiciones extra

---

## Ejemplo práctico: `less` con sudo

```bash
sudo less /etc/passwd
```
Dentro de `less`, puedes hacer:
```bash
!bash
```
Y obtienes una shell con permisos de root.

---

## Buenas Prácticas en OSCP

- Siempre revisar binarios con SUID en GTFOBins
- Lo mismo para binarios listados en `sudo -l`
- Usa `which <binario>` para confirmar rutas
- Si no tienes internet, prepárate con una copia local offline o markdown de GTFOBins

---
