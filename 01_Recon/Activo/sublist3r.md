Sublist3r es una herramienta de enumeración de subdominios muy útil en la fase de reconocimiento, especialmente para identificar superficies expuestas de aplicaciones web dentro del ámbito de OSCP.

## Instalación

```bash
git clone https://github.com/aboul3la/Sublist3r.git
cd Sublist3r
pip install -r requirements.txt
```

Opcional: mover a PATH
```bash
sudo ln -s $(pwd)/sublist3r.py /usr/local/bin/sublist3r
```

## Uso Básico

```bash
python sublist3r.py -d ejemplo.com
```

## Guardar Resultados en Archivo

```bash
python sublist3r.py -d ejemplo.com -o subdominios.txt
```

## Número de Hilos (por defecto 10)

```bash
python sublist3r.py -d ejemplo.com -t 30
```

## Combinar con Resolución de DNS (manual)

```bash
for sub in $(cat subdominios.txt); do
    host $sub | grep "has address"
done
```

## Casos de Uso OSCP

- Descubrir subdominios que revelan servicios internos.
- Comenzar escaneos en subdominios que apuntan a IPs del laboratorio.
- Alimentar herramientas como `nmap`, `nuclei`, `ffuf`, etc.

## Buenas Prácticas

- Validar qué subdominios resuelven realmente.
- Comparar con datos de `crt.sh` o DNSDumpster para aumentar cobertura.
- No limitarse solo a Sublist3r: úsalo como punto de partida.

---
