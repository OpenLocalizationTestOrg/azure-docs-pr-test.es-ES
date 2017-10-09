### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Abrir los puertos TCP en firewall de Windows hello para instancia predeterminada de Hola de hello motor de base de datos
1. Conectar la máquina virtual de toohello con Escritorio remoto. Para obtener instrucciones detalladas sobre cómo conectar toohello VM, consulte [abrir una VM de SQL con Escritorio remoto](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. Una vez iniciada la sesión, en la pantalla de inicio de bienvenida, escriba **WF.msc**y, a continuación, presione ENTRAR.
   
    ![Iniciar Hola programa de Firewall](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. Hola **Firewall de Windows con seguridad avanzada**, en el panel izquierdo de Hola, haga clic en **reglas de entrada**y, a continuación, haga clic en **nueva regla** en el panel de acciones de Hola.
   
    ![Nueva regla](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. Hola **entrada Asistente para nueva regla** cuadro de diálogo **tipo de regla**, seleccione **puerto**y, a continuación, haga clic en **siguiente**.
5. Hola **protocolo y puertos** cuadro de diálogo, Hola predeterminadas **TCP**. Hola **puertos locales específicos** cuadro y, a continuación, Hola de tipo número de puerto de instancia de Hola de hello motor de base de datos (**1433** para la instancia predeterminada de Hola o de su elección para el puerto privado de hello en el paso de punto de conexión de hello).
   
    ![Puerto TCP 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. Haga clic en **Siguiente**.
7. Hola **acción** cuadro de diálogo, seleccione **Permitir conexión hello**y, a continuación, haga clic en **siguiente**.
   
    **Nota de seguridad:** selección **Permitir conexión Hola si es segura** puede proporcionar seguridad adicional. Seleccione esta opción si desea tooconfigure opciones de seguridad adicionales en su entorno.
   
    ![Permitir conexiones](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. Hola **perfil** cuadro de diálogo, seleccione **público**, **privada**, y **dominio**. A continuación, haga clic en **Siguiente**.
   
    **Nota de seguridad:** si selecciona **pública** permite acceso a través de internet de Hola. Cuando sea posible, seleccione un perfil más restrictivo.
   
    ![Perfil público](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. Hola **nombre** cuadro de diálogo, escriba un nombre y una descripción para esta regla y, a continuación, haga clic en **finalizar**.
   
    ![Nombre de la regla](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

Abra puertos adicionales para otros componentes cada vez que sea necesario. Para obtener más información, consulte [configurar Firewall de Windows de hello tooAllow acceso a SQL Server](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>Configurar SQL Server toolisten en hello protocolo TCP

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>Configuración de SQL Server para autenticación de modo mixto
Hola motor de base de datos de SQL Server no puede usar la autenticación de Windows sin el entorno de dominio. tooconnect toohello motor de base de datos desde otro equipo, configure SQL Server para la autenticación de modo mixto. La autenticación de modo mixto permite la autenticación de SQL Server y la autenticación de Windows.

> [!NOTE]
> Si ha configurado una red virtual de Azure con un entorno de dominio configurado, es posible que no sea necesario configurar la autenticación de modo mixto.
> 
> 

1. Mientras la máquina virtual de toohello conectado, en la página de inicio de hello, escriba **SQL Server Management Studio** y haga clic en el icono de hello seleccionado.
   
    primera vez que abra Management Studio debe crear el entorno de Management Studio de los usuarios de Hola Hola. Esta operación puede tardar unos minutos.
2. Management Studio presenta hello **conectar tooServer** cuadro de diálogo. Hola **nombre del servidor** cuadro, escriba un nombre Hola de hello máquina virtual tooconnect toohello motor de base de datos con el Explorador de objetos de hello (en lugar del nombre de la máquina virtual de hello también puede usar **(local)** o un único punto como hello **nombre del servidor**). Seleccione **autenticación de Windows**y dejar  ***your_VM_name*\your_local_administrator** en hello **nombre de usuario** cuadro. Haga clic en **Conectar**.
   
    ![Conectar tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. En el Explorador de objetos de SQL Server Management Studio, haga clic en hello nombre de instancia de Hola de SQL Server (nombre de máquina virtual de hello) y, a continuación, haga clic en **propiedades**.
   
    ![Propiedades del servidor](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. En hello **seguridad** página, en **autenticación de servidor**, seleccione **modo autenticación de Windows y SQL Server**y, a continuación, haga clic en **Aceptar** .
   
    ![Seleccionar el modo de autenticación](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. En el cuadro de diálogo de hello SQL Server Management Studio, haga clic en **Aceptar** tooacknowledge Hola requisito toorestart SQL Server.
6. En el Explorador de objetos, haga clic con el botón derecho en el servidor y, a continuación, haga clic en **Reiniciar**. (También se debe reiniciar Agente SQL Server si está en ejecución).
   
    ![Reiniciar](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. En el cuadro de diálogo de hello SQL Server Management Studio, haga clic en **Sí** tooagree que desea toorestart SQL Server.

### <a name="create-sql-server-authentication-logins"></a>Creación de inicios de sesión para la autenticación de SQL Server
tooconnect toohello motor de base de datos desde otro equipo, debe crear al menos un inicio de sesión de autenticación de SQL Server.

1. En el Explorador de objetos de SQL Server Management Studio, expanda la carpeta de Hola de instancia del servidor hello en el que desea que el nuevo inicio de sesión de toocreate Hola.
2. Menú contextual hello **seguridad** carpeta, seleccione demasiado**nuevo**y seleccione **inicio de sesión...** .
   
    ![Nuevo inicio de sesión](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. Hola **inicio de sesión - nuevo** cuadro de diálogo de hello **General** página, escriba el nombre de Hola de nuevo usuario de Hola Hola **nombre de inicio de sesión** cuadro.
4. Seleccione **Autenticación de SQL Server**.
5. Hola **contraseña** cuadro, escriba una contraseña para hello nuevo usuario. Vuelva a escribir la contraseña en hello **Confirmar contraseña** cuadro.
6. Seleccione opciones de cumplimiento de la contraseña de hello necesarios (**exigir directivas de contraseñas**, **exigir expiración de contraseña**, y **usuario debe cambiar la contraseña en el siguiente inicio de sesión**). Si usa este inicio de sesión por sí mismo, no es necesario toorequire un cambio de contraseña en el siguiente inicio de sesión de Hola.
7. De hello **base de datos predeterminada** , seleccione una base de datos predeterminada para el inicio de sesión de Hola. **maestro** es Hola predeterminado para esta opción. Si aún no ha creado una base de datos de usuario, deje este conjunto demasiado**principal**.
   
    ![Propiedades de inicio de sesión](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Si se trata de hello primer inicio de sesión que está creando, puede que desee toodesignate este inicio de sesión como administrador de SQL Server. Si es así, en hello **Roles de servidor** página, verificación **sysadmin**.
   
   > [!NOTE]
   > Los miembros del rol fijo de servidor sysadmin hello tienen control completo de hello motor de base de datos. Deberá restringir cuidadosamente la suscripción en este rol.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Haga clic en Aceptar.

Para ver más información acerca de los inicios de sesión de SQL Server, consulte [Crear un inicio de sesión](http://msdn.microsoft.com/library/aa337562.aspx).

