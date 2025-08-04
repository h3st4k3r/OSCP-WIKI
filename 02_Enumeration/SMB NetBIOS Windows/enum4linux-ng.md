`enum4linux-ng` es una herramienta moderna para enumerar servicios SMB/NetBIOS/LDAP en entornos Windows desde sistemas Linux. Es una reescritura mejorada de `enum4linux`, y en OSCP es útil para recolectar usuarios, grupos, shares, políticas y más.

---

## Instalación

```bash
git clone https://github.com/cddmp/enum4linux-ng.git
cd enum4linux-ng
pip3 install -r requirements.txt
```

> Necesita Python 3 y `impacket` instalado previamente.

---

## Uso Básico (sin credenciales)

```bash
python3 enum4linux-ng.py -a 10.11.1.100
```

- `-a`: modo automático (todo lo posible sin credenciales)

---

## Uso con Credenciales

```bash
python3 enum4linux-ng.py -u usuario -p contraseña 10.11.1.100
```

También puedes usar hash NTLM:
```bash
python3 enum4linux-ng.py -u admin -H 1234567890ABCDEF1234567890ABCDEF:9a709a4f68c4b9c14d6eb9c4b7643dfc 10.11.1.100
```

---

## Opciones Útiles

- `--shares`: enumera recursos compartidos
- `--users`: enumera usuarios
- `--rid-brute`: realiza RID brute force (usuarios)
- `--password-policy`: muestra políticas de contraseña
- `--local-groups`: enumera grupos locales

Ejemplo:
```bash
python3 enum4linux-ng.py -u guest -p '' --shares --users 10.11.1.100
```

---

## Salida a Archivo

```bash
python3 enum4linux-ng.py -a 10.11.1.100 -o enum4_output.txt
```

---

## Casos de Uso OSCP

- Recolectar usuarios válidos para ataques con `hydra`, `crackmapexec`, etc.
- Enumerar shares accesibles sin credenciales o con usuarios limitados
- Obtener información útil del dominio: grupos, controladores, políticas

---

## Buenas Prácticas

- Ejecutar primero sin credenciales (`-a`), luego con lo que encuentres
- Combinar con `smbclient`, `rpcclient` o `crackmapexec` para acceso a shares
- Leer bien la política de contraseñas: puede indicar lockout o reuso

---