# Pasos previos
1. Tener instalado en el PC un __cliente SFTP__. Por ejemplo, [WinSCP](https://winscp.net/eng/download.php).
2. Tener instalado en el PC un __cliente SSH__. Por ejemplo, [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
3. Tener instalado en el PC un __editor de texto__. Por ejemplo, [Notepad++](https://notepad-plus-plus.org/downloads/).

# Editar fichero interfaces
1. Crear un fichero llamado __interfaces__ y abrir con el editor Notepad++.
2. A continuación se muestra un fichero de ejemplo donde:
  - Se asigna a la interfaz eth0 una IP por DHCP. Por esta puerta de enlace enroutará el equipo.
  - Se asigna a la interfaz eth0 una IP fija, 192.168.1.52, sin puerta de enlace.
  - Se asigna a la interfaz eth0 una IP fija, 10.70.10.52, sin puerta de enlace.

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

# Copiar el fichero interfaces al PLC
1. Conéctese al controlador por __SSH__ a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Introducir este comando: ```ping -c4 8.8.8.8```. Si responde al ping, el PLC tiene acceso a internet.
3. Introducir este comando: ```ping -c4 www.google.com```. Si responde al ping, el PLC tiene acceso a internet y además es capaz de resolver nombres por DNS.
4. Si no hay conexión a internet, comprobar:
  4.1. Introducir este comando: ```ip a s dev eth0``` para comprobar la configuración de IPs del PLCnext.
  4.2. Introducir este comando: ```ip r``` para comprobar la puerta de enlace (gateway) del PLCnext.
