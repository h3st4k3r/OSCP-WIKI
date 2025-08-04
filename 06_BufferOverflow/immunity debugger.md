`Immunity Debugger` es una herramienta gráfica para depurar binarios Windows, usada en OSCP para analizar y explotar vulnerabilidades de tipo Buffer Overflow en binarios de 32 bits.

---

## 1. Instalación

Descárgalo desde: https://www.immunityinc.com/products/debugger/

Ejecuta como administrador en una VM Windows (preferentemente XP o 7 de 32 bits). Añade también el plugin `mona.py`.

### Instalar `mona.py`

Coloca el archivo `mona.py` en:
```
C:\Program Files\Immunity Inc\Immunity Debugger\PyCommands\
```

---

## 2. Abrir el binario

Abre `Immunity Debugger`, luego:
```
File → Open → vulnerable.exe
```

Presiona `F9` para ejecutar el binario.

---

## 3. Fuzzing inicial (fuera de ID)

Desde Kali, crea un script Python para enviar cadenas crecientes hasta provocar el crash.

Una vez provocado el crash, revisa EIP:
```
View → CPU → Registros → EIP
```

---

## 4. Determinar offset

Genera un patrón:
```bash
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 500
```
Envía el patrón como payload, luego copia el valor de EIP en crash y ejecuta:
```bash
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -q 39694438
```
(Sustituye por el valor real de EIP)

---

## 5. Buscar dirección JMP ESP

En Immunity (con `mona.py`):
```
!mona modules
```
Busca módulos sin ASLR, sin DEP y con `Rebase` y `SafeSEH` desactivados.

Luego:
```
!mona find -s "\xff\xe4" -m <modulo.dll>
```
Esto encuentra direcciones `JMP ESP` que puedes usar.

---

## 6. Probar el control de EIP

Modifica el script para poner la dirección `JMP ESP` donde corresponde y verifica que EIP salta correctamente.

---

## 7. Añadir shellcode y ejecutar

Genera shellcode con `msfvenom`, usa NOP sled, y lánzalo. Revisa si se abre una shell reverse.

---

## Consejos OSCP

- Usa snapshots entre pasos para evitar repetir desde cero
- Documenta cada valor encontrado (offset, badchars, dirección JMP ESP)
- Revisa siempre los registros: `EIP`, `ESP`, `EBP`, `EAX`, etc.
- Trabaja con calma. El examen espera que lo hagas manual, sin exploits prehechos.