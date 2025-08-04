Dynamic Port Forwarding con SSH crea un proxy SOCKS que enruta todo el tráfico a través de una máquina intermedia comprometida. Esto te permite hacer pivoting sin necesidad de especificar cada puerto o destino. Ideal para entornos OSCP donde se permite SSH.

---

## Sintaxis básica

```bash
ssh -D <puerto_local> <usuario>@<ip_intermedia>
```

Ejemplo:
```bash
ssh -D 1080 user@10.10.10.10
```

Esto levanta un proxy SOCKS en tu máquina (localhost:1080), enroutando el tráfico a través de `10.10.10.10`.

---

## Opciones útiles

- `-N`: no ejecutar shell remota
- `-f`: enviar proceso a segundo plano
- `-C`: activar compresión

Ejemplo completo:
```bash
ssh -D 1080 -f -N user@10.10.10.10
```

---

## Verificación

Puedes verificar si el puerto está abierto:
```bash
netstat -tunlp | grep 1080
```

---

## Casos de uso en OSCP

- Crear un único proxy flexible para herramientas como navegador, proxychains, etc.
- Explorar redes internas sin especificar destino final
- Evitar configuración explícita de túneles por cada puerto

---

Este modo no necesita redirección de puertos específicos como en `-L` o `-R`, y es ideal para recon y exploración cuando solo tienes SSH en la máquina intermedia.