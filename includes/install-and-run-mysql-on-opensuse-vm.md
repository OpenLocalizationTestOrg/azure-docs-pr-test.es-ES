
1. privilegios de tooescalate, tipo:
   
        sudo -s
   
    Especifique la contraseña.
2. tooinstall edición Community de MySQL Server, escriba:
   
        zypper install mysql-community-server
   
    Espere hasta que MySQL se descargue e instale.
3. tooset MySQL toostart cuando arranca el sistema de hello, escriba:
   
        insserv mysql
4. Iniciar el demonio de MySQL hello (mysqld) manualmente con este comando:
   
        rcmysql start
   
    estado de hello toocheck de hello daemon de MySQL, escriba:
   
        rcmysql status
   
    Hola toostop daemon de MySQL, escriba:
   
        rcmysql stop
   
   > [!IMPORTANT]
   > Después de la instalación, la contraseña de raíz de MySQL de Hola está vacía de forma predeterminada. Se recomienda ejecutar **mysql\_secure\_installation**, un script que ayuda a proteger MySQL. Hola script le indicará que contraseña de la raíz de toochange Hola MySQL, quitar cuentas de usuario anónimo, deshabilitar los inicios de sesión raíz remota, quitar las bases de datos de prueba y volver a cargar la tabla de privilegios de Hola. Se recomienda que responda Sí tooall de estas opciones y cambiar la contraseña de la raíz de Hola.
   > 
   > 
5. Escriba este script de Hola toorun script de instalación de MySQL:
   
        mysql_secure_installation
6. Inicie sesión en tooMySQL:
   
        mysql -u root -p
   
    Escribir contraseña de raíz de MySQL hello (que cambió en el paso anterior de hello) y se mostrarán con un símbolo del sistema donde puede emitir toointeract de instrucciones SQL con la base de datos de Hola.
7. toocreate un nuevo usuario de MySQL, ejecute el siguiente de hello en hello **mysql >** símbolo del sistema:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Tenga en cuenta que Hola puntos y coma (;) al final de Hola de hello líneas son cruciales para finalizar los comandos de Hola.
8. toocreate una base de datos y conceder hello `mysqluser` permisos de usuario en el mismo, Hola problema después de comandos:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Tenga en cuenta que las contraseñas y nombres de usuario de base de datos solo se usan scripts de conexión de base de datos de toohello.  Nombres de cuenta de usuario de base de datos no representa necesariamente las cuentas de usuario real en el sistema de Hola.
9. toolog en desde otro equipo, escriba:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    donde `ip-address` es Hola dirección IP del equipo de Hola desde el que se va a conectar tooMySQL.
10. Hola tooexit utilidad de administración de base de datos de MySQL, escriba:
    
        quit

## <a name="add-an-endpoint"></a>Agregación de un extremo
1. Después de instala MySQL, deberá tooconfigure un tooaccess de punto de conexión MySQL de forma remota. Inicie sesión en toohello [portal de Azure clásico][AzurePortal]. Haga clic en **máquinas virtuales**, haga clic en nombre de saludo de la nueva máquina virtual y, a continuación, haga clic en **extremos**.
2. Haga clic en **agregar** final Hola de página Hola.
3. Agregar un punto de conexión con el nombre "MySQL" con el protocolo **TCP**, y **público** y **privada** puertos conjunto demasiado "3306".
4. tooremotely conectarse toohello virtual machine desde su equipo, escriba:
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Por ejemplo, con la máquina virtual de hello que hemos creado en este tutorial, escriba este comando:
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
