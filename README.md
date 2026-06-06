# VMware Workstation Pro Clean Uninstaller

Script BAT para realizar una limpieza profunda de VMware Workstation Pro en Windows cuando la desinstalación queda incompleta o cuando se desea hacer una instalación limpia desde cero.

El script automatiza la eliminación de servicios, procesos, drivers, adaptadores, claves de registro, tareas programadas, reglas de firewall y carpetas residuales relacionadas con VMware Workstation Pro.

---

## Objetivo

Este proyecto tiene como objetivo facilitar una reinstalación limpia de VMware Workstation Pro eliminando rastros residuales que pueden generar errores durante una nueva instalación.

---

## Características

- Detiene procesos relacionados con VMware.
- Ejecuta desinstaladores registrados si existen.
- Elimina servicios residuales de VMware y VMnet.
- Limpia drivers conocidos de VMware.
- Elimina adaptadores y dispositivos VMware cuando es posible.
- Limpia claves de registro relacionadas.
- Elimina carpetas residuales en:
  - `Program Files`
  - `Program Files (x86)`
  - `ProgramData`
  - `AppData`
  - `Temp`
- Elimina reglas de firewall relacionadas con VMware.
- Elimina tareas programadas relacionadas.
- Limpia referencias de VMware en la variable `PATH`.
- Genera backup de claves de registro antes de eliminarlas.
- Genera archivo de log de la ejecución.
- No elimina máquinas virtuales por defecto.

---

## Archivo principal

```text
VMware_Clean.bat
```

---

## Requisitos

- Windows 10 o Windows 11.
- Permisos de administrador.
- PowerShell disponible en el sistema.
- VMware Workstation Pro cerrado antes de ejecutar el script.
- Máquinas virtuales apagadas antes de iniciar la limpieza.

---

## Uso

1. Descarga el archivo:

```text
VMware_Clean.bat
```

2. Haz clic derecho sobre el archivo.

3. Selecciona:

```text
Ejecutar como administrador
```

4. Cuando el script solicite confirmación, escribe:

```text
LIMPIAR
```

5. Espera a que finalice el proceso.

6. Reinicia Windows antes de instalar nuevamente VMware Workstation Pro.

---

## Validación posterior

Después de reiniciar, abre CMD como administrador y ejecuta:

```bat
sc query type= service state= all | findstr /i "vmware vmnet"
reg query "HKLM\SOFTWARE\VMware, Inc."
reg query "HKLM\SOFTWARE\WOW6432Node\VMware, Inc."
where vmware.exe
```

Si no aparecen servicios, claves o binarios relacionados, el sistema quedó listo para una instalación limpia.

---

## Logs y backups

Durante la ejecución, el script crea una carpeta similar a:

```text
C:\VMware_Cleanup_YYYYMMDD_HHMMSS
```

Dentro se generan:

```text
VMware_Cleanup.log
RegistryBackup\
```

El directorio `RegistryBackup` contiene copias `.reg` de las claves eliminadas, cuando estas existían.

---

## Protección de máquinas virtuales

Por seguridad, el script no elimina las máquinas virtuales del usuario.

La variable interna se encuentra configurada así:

```powershell
$RemoveVirtualMachines = $false
```

Solo debe cambiarse a `true` si se desea eliminar manualmente la carpeta:

```text
C:\Users\<usuario>\Documents\Virtual Machines
```

---

## Advertencia

Este script modifica servicios, drivers, archivos del sistema y claves de registro. Úsalo únicamente si entiendes el impacto de una limpieza profunda.

Antes de ejecutarlo se recomienda:

- Cerrar VMware Workstation Pro.
- Apagar todas las máquinas virtuales.
- Crear un punto de restauración.
- Respaldar máquinas virtuales importantes.
- Revisar el script antes de usarlo en equipos productivos.

---

## Casos de uso

Este script puede ser útil cuando:

- VMware Workstation Pro no se desinstala correctamente.
- La instalación nueva falla por residuos de versiones anteriores.
- Persisten servicios como `VMnetDHCP`, `VMware NAT Service` o `VMAuthdService`.
- Quedan adaptadores virtuales VMnet después de desinstalar.
- Se requiere una instalación limpia desde cero.

---

## Descripción corta del repositorio

```text
BAT script for deep cleaning VMware Workstation Pro remnants on Windows before performing a clean installation.
```

---

## Topics sugeridos

```text
vmware
vmware-workstation
windows
batch-script
powershell
cleanup
uninstaller
sysadmin
virtualization
maintenance
```

---

## Disclaimer

Este proyecto se proporciona con fines administrativos y de mantenimiento.

El uso del script es responsabilidad del usuario. No se ofrece garantía sobre su funcionamiento en todos los entornos.

Se recomienda probarlo primero en un entorno controlado antes de ejecutarlo en equipos críticos.

---

## Autor

Desarrollado por Erick O.

GitHub: `@eocalampa`
