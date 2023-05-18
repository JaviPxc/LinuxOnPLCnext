# Pasos previos
1. Tener instalado en el PC un __cliente SFTP__. Por ejemplo, [WinSCP](https://winscp.net/eng/download.php).
2. Tener instalado en el PC un __cliente SSH__. Por ejemplo, [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

# Consultar fecha y hora del controlador
1. Conéctese al controlador por __SSH__ a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Introducir este comando: ```date```.

![image](https://user-images.githubusercontent.com/46561573/155715630-8d60887e-36f3-4e2b-9b8b-909236bf1cf7.png)

# Consultar zona horaria del controlador
1. Conéctese al controlador por __SSH__ a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Introducir este comando: ```date```.
3. Introducir este comando: ```ls -l /etc/localtime```.

![image](https://user-images.githubusercontent.com/46561573/155715435-960db859-c088-4915-8a5b-2a82206468bf.png)

# Asignar fecha y hora manualmente
1. Conéctese al controlador por __SSH__ a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Introducir este comando: ```sudo date --set "YYYY-MM_DD HH:mm:ss"```. Por ejemplo, sudo date --set "2022-02-27 13:15:30".

![image](https://user-images.githubusercontent.com/46561573/155713530-af5ffc3c-3552-4233-92c2-5badf3a52fbb.png)

# Sincronizar el reloj con servidores NTP
La fecha y la hora del controlador pueden mantenerse actualizadas automáticamente si se sincroniza el equipo con algún servidor de tiempos. Para ello, es necesario configurar adecuadamente el fichero __ntp.conf__. Aquí se proporciona un ejemplo de configuración.

Esto mantendrá sincronizado el reloj (fecha y hora), pero es algo independiente de la zona horaria definida en el equipo (esto podrá sumar o restar horas en función de la zona horaria definida).

1. Descargar el [fichero subido al repositorio](files/ntp.conf).
2. Conéctese al controlador por __SFTP__ a través de su dirección IP e inicie sesión como usuario admin. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
3. Copiar el fichero __ntp.conf__ a __/opt/plcnext/__.
4. Conéctese al controlador por __SSH__ como admin.
5. Cambiar al usuario root. Consultar [acceso con usuario root](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Acceso_con_usuario_root.md).
6. Introducir este comando: ```mv /opt/plcnext/ntp.conf /etc/ntp.conf```.
7. Comprobar que el controlador tiene [acceso a internet](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Comprobar_acceso_a_internet.md).
8. Introducir este comando: ```/etc/init.d/ntpd restart``` para reiniciar el servicio ntp.
9. Introducir este comando: ```ntpq -p``` para ver la lista de servidores NTP con los que conecta el equipo. En cuanto esté sincronizado con un servidor, este aparecerá con un asterisco "*" delante.
10. Introducir este comando: ```date``` para ver la fecha del equipo.

# Cambiar la zona horaria
1. Conéctese al controlador por __SSH__ a través de su dirección IP e inicie sesión como usuario admin. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Introducir este comando: ```ls -l /etc/localtime```. Para comprobar la zona horaria actual.
3. Cambiar al usuario root. Consultar [acceso con usuario root](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Acceso_con_usuario_root.md).
5. Introducir este comando: ```unlink /etc/localtime```. Para dejar utilizar la zona horaria actual.
6. Introducir este comando: ```ls -l /etc/localtime```. Para comprobar que no hay referencia a una zona horaria específica.
7. Introducir este comando: ```ln -sfn  /usr/share/zoneinfo/<NUEVA_ZONA_HORARIA> /etc/localtime```. Por ejemplo, sln -sfn  /usr/share/zoneinfo/Europe/Madrid /etc/localtime.
8. Introducir este comando: ```ls -l /etc/localtime```. Para comprobar que se está haciendo referencia a la nueva zona horaria.
9. Introducir este comando: ```date```. Para comprobar en el reloj que se está haciendo referencia a la nueva zona horaria.

![image](https://user-images.githubusercontent.com/46561573/155716886-bf1e09fa-2034-4df7-b115-86db8ffa2ec9.png)

_NOTA:_ La zona horaria correspondiente a __UTC__ es __/usr/share/zoneinfo/Universal__.
    
    
    
    
    
    
 
