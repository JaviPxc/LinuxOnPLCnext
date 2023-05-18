# Pasos previos
1. Tener instalado en el PC un __cliente SFTP__. Por ejemplo, [WinSCP](https://winscp.net/eng/download.php).
2. Tener instalado en el PC un __cliente SSH__. Por ejemplo, [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
3. Tener instalado en el PC un __editor de texto__. Por ejemplo, [Notepad++](https://notepad-plus-plus.org/downloads/).

# Editar fichero interfaces
1. Descargar el fichero [__interfaces__](files/interfaces) subido al repositorio y utilizarlo como plantilla. Crear un fichero llamado  y abrir con el editor Notepad++.
2. El fichero de ejemplo se asignan a la interfaz de red eth0:
   - Una IP por DHCP. Por esta puerta de enlace enroutará el equipo.
   - Una IP fija, 192.168.1.52, sin puerta de enlace.
   - Una IP fija, 10.70.10.52, sin puerta de enlace.

```
# /etc/network/interfaces -- configuration file for ifup(8), ifdown(8)

# The loopback interface
auto lo
iface lo inet loopback

# Wired or wireless interfaces
# DHCP IP given by the router. Default gateway.
auto eth0
iface eth0 inet dhcp

# Internal static IP. No gateway.
iface eth0 inet static
    address 192.168.1.52
    netmask 255.255.255.0
    gateway 0.0.0.0
    dns-nameservers 8.8.8.8 8.8.4.4

# Extra static IP. No gateway
iface eth0 inet static
    address 10.70.10.52
    netmask 255.255.255.0
    gateway 0.0.0.0
    dns-nameservers 8.8.8.8 8.8.4.4

# ensp is a adapter for the left side extension (for axcf1152 you probably never use that interface, but with axcf2152 could be).
auto enp1s0
iface enp1s0 inet static
    address 192.168.2.10
    netmask 255.255.255.0
    gateway 192.168.2.1
    dns-nameservers 8.8.8.8 8.8.4.4
```

3. El fichero debe tener el caracter __fin de línea en formato Linux__.
   - Notepad++ permite mostrar los caracteres fin de linea y cambiar el formato entre Windows(CRLF)-Linux(LF). 
    ![image](https://github.com/JaviPxc/LinuxOnPLCnext/assets/46561573/191c7472-d26b-4ee2-aec3-a9545972b3c1)
    ![image](https://github.com/JaviPxc/LinuxOnPLCnext/assets/46561573/84fe1d5c-24eb-4acd-96f1-e1d23b228b4b)

# Copiar el fichero interfaces al PLC
1. Conéctese al controlador por __SFTP__ a través de su dirección IP e inicie sesión como usuario admin. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Copiar el fichero __interfaces__ a __/opt/plcnext/__.
3. Conéctese al controlador por __SSH__ como admin.
4. Cambiar al usuario root. Consultar [acceso con usuario root](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Acceso_con_usuario_root.md).
5. Introducir este comando: ```mv /etc/network/interfaces /etc/network/interfaces_ori```. Almacenar una copia del fichero original.
6. Introducir este comando: ```mv /opt/plcnext/interfaces /etc/network/interfaces```.
7. Introducir este comando: ```reboot```. Reiniciar el PLC para que cargue la nueva configuración de red.

