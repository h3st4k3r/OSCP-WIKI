
Nabuu es una herramienta de escaneo escrita en Rust que combina velocidad con una salida clara y moderna. Aunque no es parte del kit oficial de OSCP, puede ayudarte en labs y pruebas con resultados rápidos y organizados.

## Instalación

### Requisitos
- Tener `cargo` instalado (parte de Rust):

```bash
sudo apt install cargo
```

### Instalar Nabuu

```bash
cargo install nabuu
```

Una vez instalado, debería estar disponible como `~/.cargo/bin/nabuu`. Puedes moverlo a `/usr/local/bin` si quieres:

```bash
sudo mv ~/.cargo/bin/nabuu /usr/local/bin/
```

## Uso Básico

```bash
nabuu 10.11.1.0/24
```

Esto escanea el rango de red para detectar hosts activos por defecto con puertos comunes (top 1000 TCP).

## Especificar Puertos

```bash
nabuu -p 80,443,8080 10.11.1.0/24
```

## Escaneo Completo de Puertos

```bash
nabuu -p 1-65535 10.11.1.10
```

## Aumentar Concurrencia

```bash
nabuu -t 500 -p 80,443 10.11.1.0/24
```

- `-t`: número de hilos concurrentes. Útil para mejorar la velocidad.

## Salida en JSON (útil para parsing)

```bash
nabuu -p 22,80 -o json 10.11.1.0/24 > results.json
```

## Exportar a nmap

Nabuu no genera directamente una salida nmapeable, pero puedes usar `jq` para extraer IPs:

```bash
jq -r '.[].ip' results.json > ips.txt
```

Y luego escanear con nmap:

```bash
for ip in $(cat ips.txt); do
    nmap -sC -sV -p- $ip -oN nmap_$ip.txt
done
```

## Casos de Uso OSCP

- Reconocimiento rápido con buena legibilidad.
- Integración con pipelines o herramientas personalizadas en Rust/Bash.
- Detección de hosts activos y servicios expuestos en pocos segundos.

## Buenas Prácticas

- Confirmar hallazgos críticos con `nmap` o `netcat`.
- No abusar del número de hilos (`-t`) en entornos sensibles.
- Guardar resultados en JSON para parseo y documentación.

---

