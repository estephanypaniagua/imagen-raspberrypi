# imagen-raspberrypi
Pasos para realizar una imagen personalizada(.img) para utilizarlo en un raspberry pi desde un Windows 10

Basado en [este tutorial][1].

## Requerimientos
- Windows 10 con WSL2 ([guía de instalación de WSL][2])
- Raspberry Pi Imager ([instalador del programa][4])
- Win32 disk imager ([instalador del programa][3])

## Pasos
### Insertar el Micro SD y instalar Raspberry Pi OS
![image](https://user-images.githubusercontent.com/28768405/123881689-e207e280-d90a-11eb-99ed-6960dfe24a69.png)

Se debe instalar el Raspberry Pi OS, Lite o el sistema operativo que desee en la memoria, seleccionando el OS, la memoria y dando click en write.

### Expulsar la Micro SD, insertarla en el Raspberry Pi y arrancar el sistema

### Instale y configure los programas y las configuraciones personalizadas

Se debe ser cuidadoso en este paso, configurar todo lo necesario y verificar el correcto funcionamiento del sistema ya que la imagen que se creará replicará exactamente lo configurado y desarrollado.

### Insertar la Micro SD y clonar

Insertar la memoria Micro SD a la computadora

![image](https://user-images.githubusercontent.com/28768405/123882738-0cf33600-d90d-11eb-9a6d-3059678f66da.png)

Verificar el nombre del disco que da a la memoria, en el caso que se muestra es el E. Luego se procede a abrir el programa Win32 disk imager

![image](https://user-images.githubusercontent.com/28768405/123882791-2ac09b00-d90d-11eb-9d4e-3f816289e97b.png)

Se verifica que device tenga el disco que contiene a la Micro SD, luego en image file se pone la ubicación y el nombre que se desea para la imagen a crear y se procede a dar read. La imagen que se creará tiene el tamaño de la memoria, por lo que luego debe ser reducida al tamaño real que debería ocupar. 

### Cambiar el tamaño de la imagen con Pishrink

Se debe ingresar al Ubuntu instalado apartir del WSL2 y ejecutar los siguientes comandos

``` yml
sudo apt-get install gparted
wget https://raw.githubusercontent.com/Drewsif/PiShrink/master/pishrink.sh
sudo chmod 777 pishrink.sh
sudo mv pishrink.sh /usr/local/bin/
```
Luego se procede a cerrar y abrir nuevamente el WSL2. Se utilizará raspberry_prueba.img como el nombre de la imagen creada con Win32 disk imager y prueba.img como el resultado final con Pishrink

``` yml
cp /mnt/c/windows/ruta/de/la/imagen/raspberry_prueba.img /home/nombre_del_usuario
chmod 777 raspberry_prueba.img
pishrink.sh raspberry_prueba.img prueba.img
chmod 777 prueba.img
cp prueba.img /mnt/c/windows/ruta/deseada/
```

### Extraer la memoria, y utilizar la imagen en nuevas memorias

Colocar alguna memoria que se desea utilizar y con ayuda del Raspberry Pi Imager instalar la imagen creada en la memoria. Finalmente colocar la memoria en el Raspberry Pi y inicializar. Finalmente solo se debe realizar este paso con todos los Raspberrys en los que se desee replicar el desarrollo.

<!-- Enlaces -->
[1]: https://www.youtube.com/watch?v=g0U7etKSkJ0
[2]: https://docs.microsoft.com/en-us/windows/wsl/install-win10
[3]: https://sourceforge.net/projects/win32diskimager/
[4]: https://www.raspberrypi.org/software/
