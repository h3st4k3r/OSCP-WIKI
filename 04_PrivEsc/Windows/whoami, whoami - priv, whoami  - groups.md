Los comandos `whoami`, `whoami /priv` y `whoami /groups` permiten identificar el contexto actual del usuario en el sistema Windows comprometido. Son fundamentales en OSCP para detectar posibles vectores de escalada de privilegios o abuso de tokens.

---

## 1. `whoami`

```cmd
whoami
```

Muestra el usuario actual. Ejemplo:
```
nt authority\local service
```

Esto te dice si estás bajo una cuenta del sistema, de dominio o un usuario común. También puedes detectar si ya estás en SYSTEM.

---

## 2. `whoami /priv`

```cmd
whoami /priv
```

Muestra los privilegios asignados al token del usuario:
```
Privilege Name                Description                               State
===========================  ========================================= ========
SeShutdownPrivilege          Shut down the system                      Disabled
SeDebugPrivilege             Debug programs                            Enabled
SeImpersonatePrivilege       Impersonate a client after authentication Enabled
```

### ¿Qué buscar?
- `SeImpersonatePrivilege` → útil para ataques como **PrintSpoofer**, **Potato attacks**
- `SeDebugPrivilege` → potencial abuso de procesos
- `SeAssignPrimaryTokenPrivilege` → ejecución con otros tokens

> Si están en **Enabled**, pueden explotarse directamente.

---

## 3. `whoami /groups`

```cmd
whoami /groups
```

Muestra los grupos a los que pertenece el usuario actual:

```
Group Name                            SID                                           Attributes
==================================== ============================================= =================
Administrators                        S-1-5-32-544                                   Mandatory, Enabled by default, Enabled group
Remote Desktop Users                  S-1-5-32-555                                   Mandatory, Enabled by default, Enabled group
```

### ¿Qué buscar?
- `Administrators` → ya eres admin
- `Backup Operators`, `Remote Desktop Users`, `IIS_IUSRS`, etc.
- Grupos que tengan acceso a servicios o archivos restringidos

---

## Casos de Uso OSCP

- Confirmar si estás en un contexto privilegiado
- Ver si puedes lanzar ataques de token impersonation
- Saber si tienes permisos extendidos para lectura/escritura en directorios del sistema

---

## Buenas Prácticas

- Ejecutar los tres comandos tras comprometer cualquier máquina Windows
- Combinar con `accesschk` y `systeminfo` para un análisis completo
- Usar esta información para guiar el uso de herramientas como `PrintSpoofer`, `JuicyPotato`, o `runas`

---