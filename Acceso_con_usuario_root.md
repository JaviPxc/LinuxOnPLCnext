# PASOS PREVIOS
1. Tener instalado en el PC un __cliente SFTP__. Por ejemplo, [WinSCP](https://winscp.net/eng/download.php).
2. Tener instalado en el PC un __cliente SSH__. Por ejemplo, [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

# ENCLACES RELACIONADOS
[PLCnext help. User rights](https://www.plcnext.help/te/Operating_System/Root_rights.htm#Setting_a_root_user_password)

# Establecer una contraseña de usuario root
1. Conéctese al controlador a través de su dirección IP e inicie sesión como usuario __admin__. La contraseña por defecto para el usuario admin está impresa en la carcasa del controlador.
2. Introducir este comando: __sudo passwd root__.
3. Introducir la contraseña de admin para autorizar este comando.
4. Introducir una nueva contraseña para el usuario root (mínimo 5 caracteres, preferiblemente compuestos por letras mayúsculas y minúsculas más números).
5. Confirmar la nueva contraseña introduciéndola de nuevo.
![image](https://user-images.githubusercontent.com/46561573/155708183-e24c24a3-8b50-4a9b-bd1a-3bc3b22e96fa.png)



# Como permitir que el usuario root se conecte por SSH o SFTP
