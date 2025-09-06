# Tarea 3

Esta práctica tiene como objetivo aprender a usar comandos básicos de **PowerShell** en Windows, similares a los que se usan en Linux.

---

## 1. Ir al directorio personal
En este primer paso se accede al directorio inicial del usuario con el comando cd ~ y se comprueba la ubicación utilizando pwd. Esto permite comenzar desde la carpeta base, lo que resulta práctico para mantener un punto de partida claro dentro del sistema de archivos.
```powershell
cd ~
pwd
```
Captura:
![Tarea 3](1.1.jpg)  

## 2. Crear la carpeta principal
Se crea una nueva carpeta llamada Practica_Windows y se entra en ella. El propósito de esta acción es disponer de un espacio exclusivo de trabajo, lo que ayuda a mantener organizados los archivos de la práctica y evitar que se mezclen con otros documentos del sistema.
```powershell
mkdir Practica_Windows
cd Practica_Windows
```
Captura:
![Tarea 3](1.2.jpg)  

## 3. Crear subcarpetas
En esta parte se generan dos directorios adicionales llamados Documentos y Backup, y se listan con el comando correspondiente. La intención es estructurar el trabajo separando los archivos principales de sus copias de seguridad, lo que facilita el orden y la protección de la información.
```powershell
mkdir Documentos, Backup
ls
```
Captura:
![Tarea 3](3.jpg)  

## 4. Crear y editar archivo
Dentro de la carpeta Documentos se construye un archivo de texto llamado nota.txt con un mensaje sencillo y luego se abre en Notepad. Esto sirve para crear documentación o archivos de prueba de manera rápida, y resulta útil para tomar notas o registrar información básica.
```powershell
cd Documentos
echo "Hola, este es mi primer archivo en Windows" > nota.txt
notepad nota.txt
```
Captura:
![Tarea 3](4.jpg)  

## 5. Copiar y renombrar
El archivo creado se copia a la carpeta Backup y el original dentro de Documentos se renombra como nota_final.txt. De esta manera se conserva un respaldo y se establece una versión diferenciada, lo cual es aplicable en tareas de manejo de archivos y control de cambios.
```powershell
Copy-Item nota.txt ..\Backup\
Rename-Item nota.txt nota_final.txt
ls
```
Captura:
![Tarea 3](5.jpg)  

## 6. Ver contenido
Mediante el comando Get-Content se muestra en pantalla el texto almacenado en nota_final.txt. Esta instrucción permite revisar lo que contiene un archivo sin necesidad de abrir un editor gráfico, siendo una herramienta práctica para consultar información de forma rápida y directa.
```powershell
Get-Content nota_final.txt
```
Captura:
![Tarea 3](6.jpg)  

## 7. Cambiar permisos
Con la ayuda del comando icacls se modifican los permisos de nota_final.txt, primero limitando el acceso a lectura y luego habilitando control total. Esta operación es importante porque define los privilegios de los usuarios sobre un archivo, y se utiliza en tareas de seguridad y administración.
```powershell
icacls nota_final.txt /inheritance:r /grant $env:USERNAME:R
(Otorgar permisos de lectura/escritura)
icacls nota_final.txt /inheritance:r /grant $env:USERNAME:F
```
Captura:
![Tarea 3](7.jpg)  

## 8. Buscar archivo en todo el home
En este paso se localiza el archivo nota_final.txt dentro de todo el directorio personal usando Get-ChildItem -Recurse. Este procedimiento permite encontrar documentos sin necesidad de recordar la ruta exacta, lo que resulta muy útil cuando se trabaja con gran cantidad de carpetas.
```powershell
cd ~
Get-ChildItem -Recurse -Filter "nota_final.txt"
```
Captura:
![Tarea 3](8.jpg)  
## 9. Filtrar contenido (buscar palabra dentro del archivo)
Aquí se utiliza Select-String para identificar la palabra Windows dentro del archivo nota_final.txt. La finalidad es localizar información específica en un documento, lo que puede aplicarse en la revisión de registros, búsqueda de fallos o análisis de grandes volúmenes de texto.
```powershell
Select-String -Path ~/Practica_Windows/Documentos/nota_final.txt -Pattern "Windows"
```
Captura:
![Tarea 3](9.jpg)  

## 10 Procesos
Se visualizan los procesos activos mediante Get-Process, se abre Notepad en segundo plano con Start-Process y se finaliza su ejecución con Stop-Process. Esta práctica enseña cómo gestionar programas en ejecución y es de gran utilidad para controlar aplicaciones que consumen recursos o se bloquean.
Ver procesos:
```powershell
Get-Process
```
Captura:
![Tarea 3](10.1.jpg)  
Crear proceso en segundo plano:
```powershell
Start-Process notepad -PassThru
```
Captura:
![Tarea 3](10.2.jpg)  
Matar proceso (usar el PID):
```powershell
Stop-Process -Id <PID>
```
Captura:
![Tarea 3](10.3.jpg)  

## 11 Instalar y usar un paquete
En este apartado se instala el programa cowsay con winget y se ejecuta mostrando un mensaje. El objetivo es aprender la forma de instalar software directamente desde la terminal, lo cual resulta ventajoso para automatizar la gestión y despliegue de aplicaciones en Windows.
```powershell
winget install cowsay
cowsay "Ejercicio completado!"
```
Captura:
![Tarea 3](11.1.jpg)  
![Tarea 3](11.2.jpg) 
## 12 Crear script final
Finalmente, se elabora un script llamado mis_comandos.ps1 que crea una carpeta de registros, guarda la fecha actual en un archivo y ejecuta cowsay. Luego se configuran los permisos de ejecución y se corre el script. Este proceso permite automatizar tareas repetitivas y sirve para mantenimiento o respaldo automático.
Crear script:

```powershell
cd ~/Practica_Windows
notepad mis_comandos.ps1
```
Captura:

![Tarea 3](12.1.jpg)  

Dentro del archivo escribe:

```powershell
New-Item -ItemType Directory -Force -Name Logs
Get-Date | Out-File Logs/fecha.txt
cowsay "Ejercicio completado!"
```
Captura:

![Tarea 3](12.2.jpg)  

![Tarea 3](12.3.jpg) 
Guardar y cerrar.

Dar permisos de ejecución:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```
Captura:
![Tarea 3](12.4.jpg)  

Ejecutar:
```powershell
.\mis_comandos.ps1
```
Captura:

![Tarea 3](12.5.jpg)  
