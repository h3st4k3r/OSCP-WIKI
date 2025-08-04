`rpcclient` es una herramienta del paquete Samba que permite interactuar con servicios RPC expuestos por sistemas Windows. En OSCP es extremadamente útil para enumerar usuarios, grupos, shares y políticas si se tiene acceso (incluso como usuario nulo).

---

## Instalación (si no lo tienes)

```bash
sudo apt install smbclient
```

`rpcclient` viene incluido con `samba` o `smbclient`.

---

## Conexión Básica como Usuario Nulo

```bash
rpcclient -U "" <IP>
```

O con credenciales:
```bash
rpcclient -U 'usuario%contraseña' <IP>
```

---

## Comandos Útiles en rpcclient

Una vez dentro del prompt:

### Enumerar usuarios
```bash
enumdomusers
```

### Enumerar grupos
```bash
enumdomgroups
```

### Listar miembros de un grupo específico
```bash
querygroupmem <RID>
```

### Obtener nombre de un grupo por RID
```bash
querygroup <RID>
```

### Buscar política de contraseña
```bash
getdompwinfo
```

### Ver SID del dominio
```bash
lsaquery
```

### Ver shares disponibles
```bash
netshareenum
```

---

## Enumeración Directa sin Entrar en Prompt

```bash
rpcclient -U "" -c enumdomusers <IP>
```

Puedes usar `-c` para lanzar comandos en línea sin abrir la shell interactiva.

---

## Casos de Uso OSCP

- Enumerar usuarios desde el servicio RPC sin credenciales
- Ver políticas de contraseñas, SID, grupos y miembros
- Extraer información útil para ataques SMB, LDAP o cracking offline

---

## Buenas Prácticas

- Probar acceso como usuario nulo antes de usar credenciales
- Combinar salida con `enum4linux-ng` o `crackmapexec` para validar
- Registrar los RIDs asignados: pueden revelar jerarquías o cuentas privilegiadas

---
