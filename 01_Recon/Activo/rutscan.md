
Rutscan es un escáner de puertos escrito en Rust, ligero, rápido y minimalista. Está diseñado para realizar escaneos concurrentes de forma eficiente. Útil para detectar servicios en hosts específicos durante la fase de reconocimiento en el OSCP.

## Instalación

```bash
git clone https://github.com/utkusen/rutscan.git
cd rutscan
cargo build --release
sudo cp target/release/rutscan /usr/local/bin/
```

Asegúrate de tener `cargo` instalado:
```bash
sudo apt install cargo
```

## Uso Básico

```bash
rutscan 10.11.1.10
```

Esto escaneará los puertos comunes en el host indicado.

## Escaneo de Puertos Específicos

```bash
rutscan 10.11.1.10 -p 22,80,443
```

## Escaneo de Rango de Puertos

```bash
rutscan 10.11.1.10 -p 1-1000
```

## Escaneo de Múltiples Hosts

```bash
echo "10.11.1.10\n10.11.1.11" > hosts.txt
rutscan -f hosts.txt
```

## Salida Silenciosa

```bash
rutscan 10.11.1.10 -s
```

## Aumentar Concurrencia

```bash
rutscan 10.11.1.10 -t 500
```

## Combinar con Nmap

```bash
rutscan 10.11.1.10 -p 21,22,80,139 > ports.txt
nmap -sC -sV -p $(cut -d ':' -f2 ports.txt | tr '\n' ',' | sed 's/,$//') 10.11.1.10
```

## Casos de Uso OSCP

- Escaneo rápido para enumerar servicios.
- Útil cuando necesitas una alternativa ligera a nmap/masscan.
- Puedes integrarlo en scripts personalizados de reconocimiento.

## Buenas Prácticas

- No saturar la red con `-t` demasiado alto.
- Confirmar hallazgos con escaneos de versión (`nmap -sV`).
- Guardar resultados y organizar por host.

---
