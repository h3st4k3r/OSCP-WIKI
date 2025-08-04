
`bloodhound-python` permite recolectar información de Active Directory directamente desde un entorno Linux o de forma remota, sin requerir ejecución interna como la herramienta GUI original. En OSCP es útil para analizar relaciones de dominio si tienes acceso a un entorno Windows unido al dominio.

---

## Instalación

```bash
git clone https://github.com/fox-it/bloodhound-python.git
cd bloodhound-python
pip install -r requirements.txt
```

Requiere `impacket`:
```bash
pip install impacket
```

---

## Uso Básico

```bash
python3 bloodhound-python -u <usuario> -p '<password>' -d <dominio> -dc <DC_IP> -c all
```

- `-u`: nombre de usuario válido en el dominio
- `-p`: contraseña o hash NTLM si has hecho pass-the-hash
- `-d`: nombre del dominio (ej. `corp.local`)
- `-dc`: dirección IP del controlador de dominio
- `-c all`: recolecta todo (`session`, `trusts`, `acl`, etc.)

---

## Guardar Resultados

Por defecto genera varios `.json` en el directorio actual:
- `computers.json`
- `groups.json`
- `users.json`
- `sessions.json`
- `acl.json`

Estos se importan en la GUI de BloodHound (Neo4j).

---

## Importar en BloodHound (GUI)

1. Abrir BloodHound GUI (`bloodhound` en Kali)
2. Login con Neo4j (default: neo4j / neo4j)
3. Cargar los `.json` desde la pestaña "Upload Data"
4. Analizar gráficamente relaciones, delegaciones, rutas de escalada, etc.

---

## Casos de Uso OSCP

- Detectar rutas de privilegio desde un usuario bajo hasta Domain Admin.
- Identificar sesiones abiertas, trusts interdominio, GPOs vulnerables.
- Buscar usuarios con privilegios especiales (`GetObject`, `AddMember`, etc.)

---

## Buenas Prácticas

- Ejecutar después de obtener credenciales válidas (hashes o plaintext).
- Asegúrate de tener visibilidad hacia el DC.
- Úsalo junto con `crackmapexec` para validar sesiones activas o shares expuestos.

---
