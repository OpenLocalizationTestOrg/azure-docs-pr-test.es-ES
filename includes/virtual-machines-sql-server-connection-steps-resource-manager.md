### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Configuración de una etiqueta de DNS para la dirección IP pública Hola

tooconnect toohello motor de base de datos de SQL Server de hello Internet, considere la posibilidad de crear una etiqueta de DNS para la dirección IP pública. Puede conectarse mediante la dirección IP, pero Hola etiqueta DNS crea un registro que sea más fácil tooidentify y resúmenes Hola subyacente la dirección IP pública.

> [!NOTE]
> Etiquetas de DNS no son necesarias si piensa tooonly conectar toohello SQL Server instancia dentro de hello misma red Virtual o solo localmente.

toocreate una etiqueta de DNS, seleccione primero **máquinas virtuales** en el portal de Hola. Seleccione su toobring de VM de SQL Server sus propiedades.

1. En información general de máquina virtual de hello, seleccione su **dirección IP pública**.

    ![dirección ip pública](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. En Propiedades de hello para la dirección IP pública, expanda **configuración**.

1. Escriba un nombre para la etiqueta DNS. Este nombre es un registro que pueden ser utilizados tooconnect tooyour VM de SQL Server por nombre en lugar de por dirección IP directamente.

1. Haga clic en hello **guardar** botón.

    ![etiqueta dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Conectar toohello motor de base de datos desde otro equipo

1. En un equipo conectado toohello internet, abra SQL Server Management Studio (SSMS). Si no tiene SQL Server Management Studio, puede descargarla [aquí](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

1. Hola **conectar tooServer** o **conectar tooDatabase motor** cuadro de diálogo, editar hello **nombre del servidor** valor. Escriba la dirección IP de Hola o nombre DNS completo de la máquina virtual de hello (determinado en la tarea anterior de hello). También puede agregar una coma y proporcionar el puerto TCP de SQL Server. Por ejemplo: `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. Hola **autenticación** cuadro, seleccione **autenticación de SQL Server**.

1. Hola **inicio de sesión** cuadro, escriba un nombre Hola de un inicio de sesión SQL válido.

1. Hola **contraseña** cuadro, escriba la contraseña de inicio de sesión de Hola Hola.

1. Haga clic en **Conectar**.

    ![conexión ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)