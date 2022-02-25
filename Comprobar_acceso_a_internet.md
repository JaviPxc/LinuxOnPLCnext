# Pasos previos
1. Tener instalado en el PC un __cliente SFTP__. Por ejemplo, [WinSCP](https://winscp.net/eng/download.php).
2. Tener instalado en el PC un __cliente SSH__. Por ejemplo, [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).


# Comprobar que el controlador está conectado a internet
1. Conéctese al controlador por __SSH__ a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Introducir este comando: ```ping -c4 8.8.8.8```. Si responde al ping, el PLC tiene acceso a internet.
3. Introducir este comando: ```ping -c4 www.google.com```. Si responde al ping, el PLC tiene acceso a internet y además es capaz de resolver nombres por DNS.
4. Si no hay conexión a internet, comprobar:
  4.1. Introducir este comando: ```ip a s dev eth0``` para comprobar la configuración de IPs del PLCnext.
  4.2. Introducir este comando: ```ip r``` para comprobar la puerta de enlace (gateway) del PLCnext.
