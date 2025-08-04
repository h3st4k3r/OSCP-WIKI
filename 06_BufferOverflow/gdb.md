`gdb` (GNU Debugger) es la herramienta principal para analizar binarios vulnerables en Linux. En el contexto del OSCP, se usa para depurar binarios de 32 bits con overflow y obtener control de EIP.

---

## Requisitos previos

- Asegúrate de usar una máquina con arquitectura de 32 bits o que soporte ejecución de binarios de 32 bits.
- Instala `gdb` si no está:
```bash
sudo apt install gdb
```
- Para mejor experiencia: instala `pwndbg` o `gef` (opcional pero recomendado)

---

## Lanzar el binario vulnerable

```bash
gdb ./vulnerable_binary
```

---

## Comandos básicos

```gdb
run                  # Ejecuta el binario
break main           # Pone un breakpoint en main
info registers       # Muestra valores de registros
x/32x $esp           # Muestra la pila en hexadecimal
x/s $esp             # Muestra la pila como string
x/i $eip             # Muestra la instrucción actual
pattern_create 200   # Si usas pwndbg (o usa pattern desde MSF)
disassemble main     # Ver desensamblado de main
```

---

## Encontrar offset del EIP

Usa un patrón cíclico generado con `pattern_create.rb` o pwndbg:
```bash
pattern_create 200 > pattern.txt
```

Lanza el binario, crashea con ese patrón, y luego recupera EIP:
```gdb
info registers
```

Después:
```bash
pattern_offset -q <valor_EIP>
```

---

## Verificar control de EIP

Envía payload con patrón que sobrescriba EIP con `BBBB` (`\x42` * 4). Verifica que EIP = 0x42424242:
```gdb
info registers
```

---

## Buscar instrucciones JMP ESP

```gdb
search-pattern '\xff\xe4'
```
O examina el binario con `objdump` y busca instrucciones útiles.

---

## Montar payload final

1. Padding hasta offset
2. Dirección `JMP ESP` (little endian)
3. NOP sled
4. Shellcode generado con `msfvenom`

---