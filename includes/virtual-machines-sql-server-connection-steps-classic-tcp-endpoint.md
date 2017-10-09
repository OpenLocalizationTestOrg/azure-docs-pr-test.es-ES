### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Crear un extremo TCP para la máquina virtual de Hola
En SQL Server del orden tooaccess de hello internet, la máquina virtual de Hola debe tener un toolisten de punto de conexión para la comunicación TCP entrante. Este paso de configuración de Azure, dirige TCP puerto tráfico tooa el puerto TCP entrante que es un equipo virtual toohello accesible.

> [!NOTE]
> Si va a conectar en hello mismo servicio o de red virtual en la nube, no es necesario toocreate un extremo accesible públicamente. En ese caso, podría continuar toohello siguiente paso. Para obtener más información, consulte: [Escenarios de conexión](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).
> 
> 

1. En el Portal de Azure hello, seleccione **máquinas virtuales (clásicas)**.
2. Luego seleccione la máquina virtual de SQL Server.
3. Seleccione **extremos**y, a continuación, haga clic en hello **agregar** situado en la parte superior de Hola de hoja de puntos de conexión de Hola.
   
    ![Pasos que se deben seguir en el portal para la creación del punto de conexión](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. En hello **Agregar extremo** hoja, proporcionar un **nombre** como SQLEndpoint.
5. Seleccione **TCP** para hello **protocolo**.
6. En **Puerto público**, especifique un número de puerto como **57500**.
7. Para **puerto privado**, especifique el puerto de escucha de SQL Server, cuyo valor predeterminado es demasiado**1433**.
8. Haga clic en **Aceptar** el punto de conexión de toocreate Hola.

