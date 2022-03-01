# Pasos previos
1. Tener instalado en el PC un __cliente SFTP__. Por ejemplo, [WinSCP](https://winscp.net/eng/download.php).
2. Tener instalado en el PC un __cliente SSH__. Por ejemplo, [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
3. Tener 2 Gb de espacio en disco disponibles.

# Como instalar apt-get en PLCnext
1. Conéctese al controlador por __SSH__ a través de su dirección IP e inicie sesión como usuario admin. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Cambiar al usuario root. Consultar [acceso con usuario root](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Acceso_con_usuario_root.md).
3. Comprobar que el controlador tiene [acceso a internet](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Comprobar_acceso_a_internet.md).
4. Introducir este comando: ```dpkg --print-architecture```. Para confirmar la arquitectura del equipo donde se va a instalar apt-get.
5. Introducir este comando:

    5.1: EPC 1502 o EPC 1522 (amd64): ```curl https://raw.githubusercontent.com/JaviPxc/LinuxOnPLCnext/main/apt-installer/apt-installer-amd64.sh?token=GHSAT0AAAAAABRVSUW7MGIDYJLCK55X6AP6YQ4XLBA -o apt-installer.sh```.
   
    5.2: AXC F 3152 (i386): ```curl https://raw.githubusercontent.com/JaviPxc/LinuxOnPLCnext/main/apt-installer/apt-installer-x86.sh?token=GHSAT0AAAAAABRVSUW6MJF7NX2NIHG6MC3EYQ4WRBQ -o apt-installer.sh```.
  
    5.3: AXC F 1152 o AXC F 2152 (armel): ```curl https://raw.githubusercontent.com/JaviPxc/LinuxOnPLCnext/main/apt-installer/apt-installer.sh?token=GHSAT0AAAAAABRVSUW6ZMEVR2BICL5DYAAWYQ4WSEQ -o apt-installer.sh```.

6. Introducir este comando: ```chmod 755 apt-installer.sh```
7. Introducir este comando: ```sed -i 's/\r$//' apt-installer.sh```
8. Introducir este comando: ```bash apt-installer.sh```

_OPCIONAL_: Se pueden editar los ficheros **apt-installer.sh** para modificar por ejemplo la ruta donde se van a instalar todos los paquetes _.deb_.

## Enlaces relacionados
[PLCnext Community. Installing apt-get package manager on plcnext](https://www.plcnext-community.net/makersblog/installing-apt-get-package-manager-on-plcnext/)
[Github PxC Spain. Ficheros apt-installer.sh](https://github.com/JaviPxc/LinuxOnPLCnext/tree/main/apt-installer)
[Github Belgium. Original apt installer repository](https://github.com/pxcbe/apt-installer/)



Now all the files will be downloaded and installed, keep an eye out for any errors that might occur, normally there should be 2 in the beginning of the script but no need to worry about those. After this is done you’re ready to use apt(-get) to install some packages. 

And that’s all there is to it, below you can find some help if you run into some problems common problems i found.

if however apt(-get) update is giving you trouble use either of these commands as a workaround:

apt-get update --allow-unauthenticated
apt-get update --allow-insecure-repositories

If packages give errors on dependencies or configurations use:

rm /var/lib/dpkg/info/*Name_off_package_in_error*
dpkg --configure -D 777 Name_off_package_in_error
apt -f install

After using this run this to make sure the package has been installed correctly:

apt install Name_off_package_in_error

Then check if the original package has been installed and works.
