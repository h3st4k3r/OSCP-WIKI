El *Remote Port Forwarding* permite redirigir el tráfico desde una máquina remota hacia tu equipo local, útil cuando el objetivo (por ejemplo, un servicio interno) solo es accesible desde la máquina comprometida.

Se usa especialmente cuando:
- No puedes acceder directamente al servicio desde Kali
- Pero tienes una shell SSH (o reverse shell con túnel)

---

## Sintaxis básica

```bash
ssh -R <puerto_remoto>:<host_objetivo>:<puerto_objetivo> <usuario>@<IP_local>
```

- `<puerto_remoto>`: puerto abierto en la máquina remota (víctima)
- `<host_objetivo>`: IP del objetivo (normalmente `localhost` en Kali)
- `<puerto_objetivo>`: servicio local que quieres exponer

---

## Ejemplo práctico

Tu máquina Kali tiene un servidor web en el puerto 8000, y quieres que la víctima lo pueda acceder:
```bash
ssh -R 8888:127.0.0.1:8000 user@victima
```

Desde la víctima:
```bash
curl http://127.0.0.1:8888
```

Esto reenvía el puerto 8000 de Kali a 127.0.0.1:8888 en la máquina remota.

---

## Uso en pivoting OSCP

Puedes usarlo para:
- Exponer servicios de tu Kali (como `smbserver.py`, `http.server`, etc.)
- Descargar binarios desde Kali aunque la víctima no tenga acceso directo
- Lanzar reverse shells hacia servicios que solo escucha Kali (como un `nc -lvnp`)

---

## Consideraciones técnicas

- Asegúrate de que el `sshd_config` permite `GatewayPorts yes` si necesitas exponer el puerto fuera del host remoto
- Algunos firewalls pueden bloquear puertos de escucha en el host remoto

---

## Alternativa con `plink.exe` (en Windows remoto)

```cmd
plink.exe -ssh user@<Kali_IP> -R 8888:127.0.0.1:8000 -N
```

Desde la máquina Windows comprometida se puede acceder al contenido servido en Kali.

---

## Buenas prácticas

- Usa puertos no privilegiados (mayores a 1024) para evitar conflictos
- Verifica con `netstat -an` si el túnel está activo
- Usa `-N` si solo quieres el túnel sin shell

---
