1. Mientras la máquina virtual de toohello conectado con Escritorio remoto, busque **Configuration Manager**:

    ![Abrir SSCM](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. En el Administrador de configuración de SQL Server, en el panel de la consola de hello, expanda **configuración de red de SQL Server**.

1. En el panel de la consola de hello, haga clic en **protocolos para MSSQLSERVER** (nombre de instancia predeterminado de Hola.) En el panel de detalles de hello, haga clic en **TCP** y haga clic en **habilitar** si aún no está habilitado.

    ![Habilitar TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. En el panel de la consola de hello, haga clic en **Services de SQL Server**. En el panel de detalles de hello, haga clic en  **SQL Server (*nombre de instancia*) ** (instancia predeterminada de hello es **SQL Server (MSSQLSERVER)**) y, a continuación, haga clic en **reiniciar** , toostop y reiniciar la instancia de Hola de SQL Server.

    ![Reiniciar el motor de base de datos](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Cierre el Administrador de configuración de SQL Server.

Para obtener más información acerca de cómo habilitar los protocolos de hello motor de base de datos de SQL Server, vea [habilitar o deshabilitar un protocolo de red de servidor](http://msdn.microsoft.com/library/ms191294.aspx).
