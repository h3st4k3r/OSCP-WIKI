`vncviewer` permite conectarse a escritorios remotos que exponen el protocolo VNC (puerto 5900+). En OSCP, se puede usar para obtener acceso completo a sistemas mal configurados o con credenciales débiles.

---

## Instalación

```bash
sudo apt install tigervnc-viewer
```

Este comando instala `vncviewer` como cliente VNC.

---

## Detectar Servicios VNC

### Con Nmap
```bash
nmap -p 5900 --script vnc-info,vnc-title <IP>
```

- `vnc-info`: extrae información sobre la implementación VNC
- `vnc-title`: intenta obtener el título del escritorio remoto

---

## Conexión a un Servidor VNC

```bash
vncviewer <IP>:<display>
```

> El display `:1` corresponde al puerto 5901, `:2` a 5902, etc.

### Ejemplo
```bash
vncviewer 10.11.1.20:1
```

Si no se requiere contraseña, te conectará directamente. Si la pide, prueba credenciales por defecto o fuerza bruta si está permitido.

---

## Fuerza Bruta con `hydra`

```bash
hydra -s 5900 -V -P /usr/share/wordlists/rockyou.txt -t 4 <IP> vnc
```

---

## Extraer Captura del Escritorio (si es posible)

Algunas configuraciones permiten conexión sin interacción. Puedes grabar o capturar pantalla con herramientas externas.

---

## Casos de Uso OSCP

- Acceso remoto completo a sistemas vulnerables
- Interacción gráfica sin necesidad de shell
- Extracción de credenciales visibles o archivos en pantalla

---

## Buenas Prácticas

- Si te conectas, graba y documenta toda la sesión
- No modifiques nada salvo que esté permitido
- Verifica si hay protección por contraseña o autenticación débil

---
