# Pasos previos
1. Tener instalado en el PC un __cliente SFTP__. Por ejemplo, [WinSCP](https://winscp.net/eng/download.php).
2. Tener instalado en el PC un __cliente SSH__. Por ejemplo, [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

# Establecer una contraseña de usuario root
1. Conéctese al controlador a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Introducir este comando: ```sudo passwd root```.
3. Introducir la contraseña de admin para autorizar este comando.
4. Introducir una nueva contraseña para el usuario root (mínimo 5 caracteres, preferiblemente compuestos por letras mayúsculas y minúsculas más números).
5. Confirmar la nueva contraseña introduciéndola de nuevo.
![image](https://user-images.githubusercontent.com/46561573/155708183-e24c24a3-8b50-4a9b-bd1a-3bc3b22e96fa.png)

# Utilizar el usuario root
1. Conéctese al controlador a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Cambiar al usuario root con el comando ```su -``` y la contraseña de root.
3. Realizar las actividades que necesitan permisos del usuario root.
4. Una vez que haya ejecutado todas las actividades como usuario root, volver a cambiar al rol de usuario anterior (por ejemplo, admin) utilizando el comando ```exit```.

# Eliminar la contraseña de root
Si la contraseña de root ya no es necesaria, elimínela. Esto evitará que usuarios no autorizados modifiquen el firmware.
1. Conéctese al controlador a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. En la interfaz de línea de comandos o shell, introduzca este comando: ```sudo passwd -d root```.
El usuario root sigue presente en el controlador, pero antes de volver a utilizarlo hay que establecer una nueva contraseña.

# Inicio de sesión SSH o SFTP como usuario root
El inicio de sesión __SSH__ como usuario __root__ no está permitido por razones de seguridad. Sin embargo, hay algunos casos en los que el inicio de sesión SSH como usuario root es necesario para realizar comandos que están reservados para el usuario root bajo una conexión SSH segura.

Para iniciar la sesión como usuario root, se debe establecer previamente la contraseña del usuario root.

Para activar o desactivar el inicio de sesión directo a través de SSH para el usuario root, hay que configurarlo en el archivo __sshd_config__ como se muestra aquí:

## Activación del inicio de sesión SSH como usuario root
1. Conéctese al controlador a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Iniciar sesión como usuario root.
3. Abrir el archivo ``` /etc/ssh/sshd_config```. (por ejemplo, con el editor vim o nano).
4. En la sección __# Authentication:__, activar la entrada quitnado el comentario __PermitRootLogin yes__.
```
# Authentication:

#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

#RSAAuthentication yes
#PubkeyAuthentication yes
```
5. Reiniciar el servicio SSH con __/etc/init.d/sshd restart__.


## Desactivación del inicio de sesión SSH como usuario root
1. Conéctese al controlador a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. [Iniciar sesión como usuario root](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Acceso_con_usuario_root.md#utilizar-el-usuario-root).
3. Abrir el archivo ``` /etc/ssh/sshd_config```. (por ejemplo, con el editor vim o nano).
4. En la sección __# Authentication:__, desactivar la entrada poniendo de nuevo un comentario __#PermitRootLogin yes__.
 ```
# Authentication:

#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

#RSAAuthentication yes
#PubkeyAuthentication yes
```
5. Reiniciar el servicio SSH con __/etc/init.d/sshd restart__.


## Enlaces relacionados
[PLCnext help. User rights](https://www.plcnext.help/te/Operating_System/Root_rights.htm#Setting_a_root_user_password)

[PLCnext help. SSH login as root user](https://www.plcnext.help/te/Operating_System/SSH_login_as_root_user.htm)
