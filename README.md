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

```text
VMware_Clean.bat
