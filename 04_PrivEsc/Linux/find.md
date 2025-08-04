`find` es una de las herramientas más simples y potentes para buscar ficheros con permisos inseguros, binarios SUID/SGID o scripts con potencial para escalar privilegios. En OSCP es completamente válida y muy útil.

---

## Buscar binarios SUID

```bash
find / -perm -4000 -type f 2>/dev/null
```

- `-4000`: bit SUID (ejecuta como propietario)
- `-type f`: solo archivos
- `2>/dev/null`: oculta errores de acceso

> Revisa cada resultado con [GTFOBins](https://gtfobins.github.io) si es un binario del sistema.

---

## Buscar binarios SGID

```bash
find / -perm -2000 -type f 2>/dev/null
```

Menos común pero también útil. Ejecutan con el grupo del archivo.

---

## Buscar archivos con permisos de escritura por cualquier usuario

```bash
find / -writable -type f ! -path "/proc/*" 2>/dev/null
```

Puede revelar scripts o binarios modificables por el usuario actual.

---

## Buscar archivos con permisos 777 (inseguros)

```bash
find / -type f -perm -0777 2>/dev/null
```

También puedes buscar directorios 777, peligrosos si se usan para crons:
```bash
find / -type d -perm -0777 2>/dev/null
```

---

## Buscar archivos por propietario (ej. root)

```bash
find / -user root -type f 2>/dev/null
```

Útil para detectar ficheros interesantes si se combinan con permisos de escritura.

---

## Buscar archivos recientes (crons o temporales)

```bash
find / -type f -mmin -10 2>/dev/null
```

Archivos modificados en los últimos 10 minutos. Puedes descubrir scripts lanzados por cron.

---

## Casos de Uso OSCP

- Encontrar SUID/SUID misconfigurados para abusar (ej. `find`, `vim`, `nano`, `python`)
- Detectar scripts mal protegidos o editables por el usuario
- Inspeccionar rutas de crons o backups en ejecución

---

## Buenas Prácticas

- Usa `find` siempre al principio junto con `sudo -l` y `id`
- Filtra resultados con `| grep` para reducir ruido
- Documenta rutas sospechosas para probar con GTFOBins

---
