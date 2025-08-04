`pwndbg` y `gef` son entornos extendidos para `gdb` que mejoran la experiencia al analizar binarios vulnerables, especialmente durante prácticas de buffer overflow en Linux (OSCP-style).

Ambos proporcionan autocompletado, inspección de memoria mejorada, análisis de registros, búsqueda de instrucciones útiles y utilidades para crear patrones.

---

## Instalación

### Requisitos previos:
```bash
sudo apt install gdb python3-pip git
```

### Instalar `pwndbg`
```bash
git clone https://github.com/pwndbg/pwndbg.git
cd pwndbg
./setup.sh
```

### Instalar `gef`
```bash
echo source ~/gef.py >> ~/.gdbinit
wget -O ~/gef.py https://gef.blah.cat/py
```

> Solo instala uno a la vez para evitar conflictos. Se recomienda `pwndbg` por su integración más directa con OSCP.

---

## Funcionalidades clave

### `pattern_create` y `pattern_offset`

```bash
pattern_create 200
pattern_offset 0x41414141
```

### Buscar instrucciones útiles
```bash
search '\xff\xe4'   # Buscar JMP ESP
```

### Ver registros y pila
```bash
context              # Vista completa (registros, stack, memoria, desensamblado)
info registers       # Registros básicos
x/32x $esp           # Hex dump de pila
x/s $esp             # String dump
```

### Análisis dinámico
- `next`, `step`, `continue`: para navegar ejecución
- `disassemble main`: ver ensamblado
- `break <func>`: breakpoint
- `run`, `r`: ejecutar

---

## Diferencias principales
| Característica        | pwndbg         | gef           |
|------------------------|----------------|---------------|
| Interfaz visual stack | Sí             | Sí            |
| Plugins externos      | Limitado       | Modular       |
| Estilo visual         | Color claro    | Más sobrio    |
| Uso en OSCP           | Recomendado    | Opcional      |

---

## Buenas prácticas OSCP
- Usa siempre una copia local del binario y márcalo como ejecutable
- Usa `set disassembly-flavor intel` para ver instrucciones estilo Intel
- Usa `context` constantemente para revisar el estado general
- Limpia `~/.gdbinit` si cambias entre `pwndbg` y `gef`

---
