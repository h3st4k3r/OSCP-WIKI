`windapsearch` es una herramienta ligera escrita en Python para realizar búsquedas LDAP en Active Directory desde un sistema Linux. Está pensada para ser rápida, simple y útil en fases de enumeración en OSCP cuando se cuenta con credenciales de dominio.

---

## Instalación

```bash
git clone https://github.com/ropnop/windapsearch.git
cd windapsearch
pip install -r requirements.txt
```

---

## Uso Básico

```bash
python3 windapsearch.py -u 'user' -p 'password' -d 'corp.local' --dc-ip 10.11.1.5
```

Este comando realizará una consulta básica al DC y listará usuarios.

---

## Consultas Comunes

### Enumerar Todos los Usuarios
```bash
python3 windapsearch.py -u user -p password -d corp.local --dc-ip 10.11.1.5 --full-users
```

### Enumerar Grupos
```bash
python3 windapsearch.py -u user -p password -d corp.local --dc-ip 10.11.1.5 --groups
```

### Buscar Administradores de Dominio
```bash
python3 windapsearch.py -u user -p password -d corp.local --dc-ip 10.11.1.5 --da
```

### Mostrar Objetos Personalizados (ej: DNSAdmins)
```bash
python3 windapsearch.py -u user -p password -d corp.local --dc-ip 10.11.1.5 --filter '(memberOf=CN=DNSAdmins,CN=Users,DC=corp,DC=local)'
```

---

## Parámetros Útiles

- `--dc-ip`: IP del controlador de dominio
- `--full`: salida detallada de objetos
- `--asreproast`: muestra usuarios vulnerables a AS-REP Roasting
- `--kerberoast`: busca cuentas SPN para Kerberoasting
- `--json`: salida en JSON (útil para scripts)

---

## Casos de Uso OSCP

- Recolectar usuarios y grupos del dominio tras comprometer credenciales.
- Detectar cuentas vulnerables a ataques offline (`--asreproast`, `--kerberoast`).
- Buscar rutas de privilegios (input para BloodHound o análisis manual).

---

## Buenas Prácticas

- Siempre usar conexión segura o en entorno controlado.
- Usar `--json` si vas a parsear la salida con JQ o scripts.
- Complementar con `ldapsearch` si necesitas consultas más personalizadas.

---