# VMware Workstation Pro Clean Uninstaller

Script BAT para realizar una limpieza profunda de VMware Workstation Pro en Windows cuando la desinstalación queda incompleta o se desea hacer una instalación limpia desde cero.

El script automatiza la eliminación de servicios, procesos, drivers, adaptadores, claves de registro, tareas programadas, reglas de firewall y carpetas residuales relacionadas con VMware Workstation Pro.

## Objetivo

Este proyecto tiene como objetivo facilitar una reinstalación limpia de VMware Workstation Pro eliminando rastros residuales que pueden generar errores durante una nueva instalación.

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

## Archivo principal

VMware_Clean.bat


## Requisitos
Windows 10 o Windows 11.
Permisos de administrador.
PowerShell disponible en el sistema.
VMware Workstation Pro cerrado antes de ejecutar el script.

## Uso
Descarga el archivo:
VMware_Clean.bat

Haz clic derecho sobre el archivo.
Selecciona:
Ejecutar como administrador
Cuando el script solicite confirmación, escribe:

## LIMPIAR
Espera a que finalice el proceso.
Reinicia Windows antes de instalar nuevamente VMware Workstation Pro.
Validación posterior

Después de reiniciar, abre CMD como administrador y ejecuta:

sc query type= service state= all | findstr /i "vmware vmnet"
reg query "HKLM\SOFTWARE\VMware, Inc."
reg query "HKLM\SOFTWARE\WOW6432Node\VMware, Inc."
where vmware.exe

Si no aparecen servicios, claves o binarios relacionados, el sistema quedó listo para una instalación limpia.

Logs y backups

Durante la ejecución, el script crea una carpeta similar a:

C:\VMware_Cleanup_YYYYMMDD_HHMMSS

Dentro se generan:

VMware_Cleanup.log
RegistryBackup\

El directorio RegistryBackup contiene copias .reg de las claves eliminadas, cuando estas existían.

Protección de máquinas virtuales

Por seguridad, el script no elimina las máquinas virtuales del usuario.

La variable interna se encuentra configurada así:

$RemoveVirtualMachines = $false

Solo debe cambiarse a true si se desea eliminar manualmente la carpeta:

C:\Users\<usuario>\Documents\Virtual Machines
Advertencia

Este script modifica servicios, drivers, archivos del sistema y claves de registro. Úsalo únicamente si entiendes el impacto de una limpieza profunda.

Antes de ejecutarlo se recomienda:

Cerrar VMware Workstation Pro.
Apagar todas las máquinas virtuales.
Crear un punto de restauración.
Respaldar máquinas virtuales importantes.
Revisar el script antes de usarlo en equipos productivos.
Casos de uso

Este script puede ser útil cuando:

VMware Workstation Pro no se desinstala correctamente.
La instalación nueva falla por residuos de versiones anteriores.
Persisten servicios como VMnetDHCP, VMware NAT Service o VMAuthdService.
Quedan adaptadores virtuales VMnet después de desinstalar.
Se requiere una instalación limpia desde cero.
