`ldapsearch` permite consultar servidores LDAP (como Active Directory) desde un entorno Linux. En OSCP, es útil cuando tienes acceso a un DC y cuentas válidas (o acceso anónimo) para enumerar usuarios, grupos, políticas y objetos del dominio.

---

## Instalación (si no lo tienes ya)

```bash
sudo apt install ldap-utils
```

---

## Sintaxis General

```bash
ldapsearch -x -H ldap://<DC_IP> -D '<usuario>' -w '<password>' -b '<base_dn>'
```

- `-x`: usa autenticación simple (no SASL)
- `-H`: URI del servidor LDAP (usa `ldap://` o `ldaps://`)
- `-D`: usuario en formato `CN=user,OU=unit,DC=corp,DC=local`
- `-w`: contraseña del usuario
- `-b`: base DN para búsqueda

---

## Ejemplo Real

```bash
ldapsearch -x -H ldap://10.11.1.5 -D 'user1@corp.local' -w 'password123' -b 'DC=corp,DC=local'
```

## Enumerar Usuarios

```bash
ldapsearch -x -H ldap://<IP> -D 'user@domain' -w 'pass' -b "DC=domain,DC=local" "(objectClass=user)" sAMAccountName
```

## Enumerar Grupos

```bash
ldapsearch -x -H ldap://<IP> -D 'user@domain' -w 'pass' -b "DC=domain,DC=local" "(objectClass=group)" cn
```

## Buscar Información de un Usuario Específico

```bash
ldapsearch -x -H ldap://<IP> -D 'user@domain' -w 'pass' -b "DC=domain,DC=local" "(sAMAccountName=juanperez)"
```

---

## Enumeración Anónima

Si el servidor lo permite:

```bash
ldapsearch -x -H ldap://<IP> -b "DC=domain,DC=local"
```

---

## Casos de Uso OSCP

- Enumerar usuarios para password spraying o AS-REP roasting.
- Descubrir rutas jerárquicas del dominio.
- Identificar nombres completos, correos, grupos y descripciones útiles.

---

## Buenas Prácticas

- Siempre probar acceso anónimo primero.
- Usar filtros para limitar la salida (`sAMAccountName=*`, `objectClass=user`...).
- Exportar resultados a fichero para posterior parsing (`> salida.ldif`).

---
