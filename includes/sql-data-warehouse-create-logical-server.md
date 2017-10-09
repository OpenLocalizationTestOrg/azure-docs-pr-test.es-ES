### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Crear un nuevo servidor SQL lógico Hola portal de Azure

1. Haga clic en **Nuevo**, busque **servidor lógico**y, a continuación, pulse **ENTRAR**.

    ![buscar servidor lógico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. Seleccione **SQL Server (servidor lógico)** 

    ![seleccionar servidor lógico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Haga clic en **crear** hoja tooopen Hola de nuevo SQL Server (servidor lógico).

   <kbd>![abrir la hoja de servidor lógico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![hoja de servidor lógico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. En el cuadro de texto de nombre de servidor del módulo de SQL Server (servidor lógico) de hello, proporcione un nombre válido para el servidor lógico nuevo de Hola. Una marca de verificación verde indica que ha proporcionado un nombre válido.
    
    ![nuevo nombre de servidor](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Hello nombre completo para el nuevo servidor será < nombreDeSuServidor >. database.windows.net.
    >
    
4. En el cuadro de texto del inicio de sesión Hola de administración de servidor, proporcione un nombre de usuario de inicio de sesión de autenticación de SQL de Hola para este servidor. Este inicio de sesión se conoce como inicio de sesión principal del servidor de Hola. Una marca de verificación verde indica que ha proporcionado un nombre válido.
    
    ![inicio de sesión de administrador de SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. Hola **contraseña** y **Confirmar contraseña** cuadros de texto, proporcione una contraseña para la cuenta de inicio de sesión principal del servidor de Hola. Una marca de verificación verde indica que ha proporcionado una contraseña válida.
    
    ![contraseña del administrador de SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. Seleccione una suscripción en el que tiene permiso toocreate objetos.

    ![suscripción](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. En el cuadro de texto de grupo de recursos de hello seleccione **crear nuevo** y, a continuación, en el cuadro de texto de grupo de recursos de hello, proporcione un nombre válido para el nuevo grupo de recursos hello (también puede usar un grupo de recursos existente si ya ha creado uno para sí mismo). Una marca de verificación verde indica que ha proporcionado un nombre válido.

    ![nuevo grupo de recursos](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. Hola **ubicación** ubicación tooyour adecuado: por ejemplo, "Australia Oriental" del centro de cuadro de texto, seleccione una de datos.
    
    ![ubicación del servidor](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > Hola casilla **server tooaccess de permitir que los servicios de azure** no se puede cambiar en esta hoja. Puede cambiar esta configuración en la hoja de firewall del servidor de Hola. Para más información, consulte [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md) (Introducción a la seguridad).
    >
    
9. Haga clic en **Crear**.

    ![botón Crear](./media/sql-data-warehouse-create-logical-server/create.png)

