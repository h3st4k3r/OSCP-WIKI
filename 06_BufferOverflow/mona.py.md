`mona.py` es un plugin para Immunity Debugger que automatiza tareas repetitivas durante la explotación de Buffer Overflows. Es fundamental en OSCP para trabajar con binarios de 32 bits en Windows.

Coloca `mona.py` en:
```
C:\Program Files\Immunity Inc\Immunity Debugger\PyCommands\
```

---

## Inicializar mona en un directorio específico

Dentro de Immunity Debugger:
```cmd
!mona config -set workingfolder C:\mona\%p
```

Esto organiza la salida por proceso.

---

## 1. Generar patrón cíclico

```cmd
!mona pattern_create 500
```

Usa este patrón como payload en tu script y provoca el crash.

---

## 2. Obtener offset del EIP

Tras el crash, copia el valor de EIP:
```cmd
!mona pattern_offset EIP_VALUE
```

Ejemplo:
```cmd
!mona pattern_offset 39694438
```

---

## 3. Buscar JMP ESP

Primero lista módulos cargados:
```cmd
!mona modules
```

Filtra uno que esté sin ASLR, Rebase ni SafeSEH y que no tenga DEP.

Después:
```cmd
!mona find -s "\xff\xe4" -m nombre.dll
```

Esto buscará instrucciones `JMP ESP` válidas.

---

## 4. Buscar badchars

Crea el listado de caracteres a probar:
```cmd
!mona bytearray -b "\x00"
```

Luego haz un dump de memoria en `ESP`:
```cmd
!mona compare -f C:\mona\vulnserv\bytearray.bin -a ESP
```

Repite quitando los badchars uno por uno hasta tener el listado limpio.

---

## 5. Buscar funciones útiles

Para buscar instrucciones específicas como `CALL ESP`, `PUSH ESP`, `JMP [ESP]`, etc.:
```cmd
!mona find -s "\xff\xe4" -m <dll>
```
Puedes cambiar `\xff\xe4` por la secuencia que te interese.

---

## Buenas prácticas OSCP

- Siempre limpia el working folder antes de nuevas pruebas:
```cmd
!mona clean
```
- Usa nombres de procesos claros (e.g. `vulnserv`) para tener directorios ordenados
- Verifica bien los módulos antes de confiar en una dirección JMP ESP

---
