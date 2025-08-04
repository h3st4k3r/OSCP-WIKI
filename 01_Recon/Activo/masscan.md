
Masscan es una herramienta de escaneo de puertos extremadamente rápida, ideal para la fase de reconocimiento en OSCP. Su sintaxis se parece a nmap, pero su motor es más cercano a scanrand. Aquí tienes una guía práctica.

## Instalación

En Kali Linux, puedes instalarlo con:
```bash
sudo apt update && sudo apt install masscan
```

O bien clonar y compilar:
```bash
git clone https://github.com/robertdavidgraham/masscan
cd masscan
make
```

## Uso Básico

```bash
sudo masscan -p80,443 10.11.1.0/24 --rate=1000
```

- `-p80,443`: puertos a escanear.
- `10.11.1.0/24`: rango de red objetivo.
- `--rate=1000`: velocidad de paquetes por segundo (ajusta según tu red).

> ⚠️ **Importante**: Masscan necesita privilegios de root y puede causar bloqueos si se abusa de la tasa de envío.

## Escaneo de Todos los Puertos

```bash
sudo masscan -p1-65535 10.11.1.0/24 --rate=500
```

## Guardar Resultados

```bash
sudo masscan -p22,80,443 10.11.1.0/24 -oG masscan_results.txt
```

- `-oG`: guarda en formato grepable.

## Leer los resultados e integrarlos con nmap

```bash
grep 'Ports' masscan_results.txt | cut -d ' ' -f 2 > ips.txt

for ip in $(cat ips.txt); do
    nmap -sC -sV -p- $ip -oN nmap_$ip.txt
done
```

## Escaneo Silencioso (menos detectable)

```bash
sudo masscan -p80 10.11.1.0/24 --rate=100 --source-port 4444
```

- `--source-port`: ayuda a evadir firewalls básicos.

## Casos de Uso en OSCP

- Detección rápida de hosts vivos.
- Enumeración de servicios antes de usar nmap.
- Preparar targets para Hydra, Gobuster, etc.

## Buenas Prácticas

- No escanear rangos completos sin permiso.
- Usar `--rate` bajo en redes sensibles.
- Confirmar resultados con nmap.

---

