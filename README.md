# 🖥️ Práctica Windows con PowerShell

Este documento describe la práctica en **Windows PowerShell**, paso a paso, con los comandos corregidos y explicados.

---

## 🔹 1. Ir al directorio personal  
Ejecuta: `cd` y luego `pwd`.  
Debe mostrar algo como:  
`C:\Users\Lenovo`  

---

## 🔹 2. Crear la carpeta principal  
Ejecuta: `mkdir Practica_Windows` y luego `cd Practica_Windows`.  

---

## 🔹 3. Crear subcarpetas  
Ejecuta: `mkdir Documentos, Backup`  
Verificar con: `ls`  
Debe mostrar: **Backup** y **Documentos**.  

---

## 🔹 4. Crear y editar archivo  
Ejecuta: `cd Documentos`  
Crear archivo: `echo "Hola, este es mi primer archivo en Windows" > nota.txt`  
Abrir con: `notepad nota.txt`  

---

## 🔹 5. Copiar y renombrar  
Ejecuta:  
- `Copy-Item nota.txt ..\Backup\`  
- `Rename-Item nota.txt nota_final.txt`  
Verificar con: `ls` (debe aparecer **nota_final.txt**).  

---

## 🔹 6. Ver contenido  
Ejecuta: `Get-Content nota_final.txt`  

---

## 🔹 7. Cambiar permisos  
En Windows se usan **icacls**:  
$usuario = $env:USERNAME
icacls nota_final.txt /inheritance:r /grant ($usuario + ":(R)")

La salida debe mostrar que se procesó el archivo correctamente.  

---

## 🔹 8. Buscar archivo en todo el home  
Ejecuta:  
- `cd ~`  
- `Get-ChildItem -Recurse -Filter "nota_final.txt"`  

---

## 🔹 9. Filtrar contenido (buscar palabra dentro del archivo)  
Ejecuta:  
`Select-String -Path "$HOME\Practica_Windows\Documentos\nota_final.txt" -Pattern "Windows"`  

La salida debe mostrar la línea donde aparece la palabra buscada.  

---

## 🔹 🔟 Procesos  
1. Ver procesos activos con: `Get-Process`  
2. Abrir proceso de prueba (ejemplo con Notepad): `Start-Process notepad`  
3. Matar proceso:  
   - `Stop-Process -Id [ID]`  
   - o `Stop-Process -Name notepad -Force`  

---

## 🔹 1️⃣1️⃣ Instalar y usar un paquete  
En Windows se puede usar **Chocolatey** o **pip**.  

Con Chocolatey:  
- `choco install cowsay -y`  
- `cowsay "Ejercicio completado!"`  

Con Python:  
- `pip install cowsay`  
- `python -m cowsay "Ejercicio completado!"`  

---

## 🔹 1️⃣2️⃣ Crear script final  
Ejecuta: `cd $HOME\Practica_Windows`  
Crear archivo con: `notepad mis_comandos.ps1`  

Dentro escribe:  

Script de práctica en Windows

New-Item -ItemType Directory -Force -Name Logs
Get-Date | Out-File Logs\fecha.txt
"Ejercicio completado!" | Out-File Logs\mensaje.txt

Guardar y cerrar.  

Dar permisos de ejecución (si no está activado):  
`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`  

Ejecutar el script:  
`.\mis_comandos.ps1`  

---

✅ Con esto la práctica queda **completa y sin errores**, adaptada totalmente a **Windows PowerShell**.  
