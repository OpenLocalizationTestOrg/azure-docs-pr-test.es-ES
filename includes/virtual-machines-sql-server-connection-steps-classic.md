### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Determinar el nombre DNS de Hola de máquina virtual de Hola
tooconnect toohello motor de base de datos de SQL Server desde otro equipo, debe conocer Hola sistema de nombres de dominio (DNS) nombre de máquina virtual de Hola. (Esto es nombre Hola Hola usa internet tooidentify virtual Hola máquina. Puede usar la dirección IP de hello, pero puede cambiar la dirección IP de hello cuando Azure mueve recursos por redundancia o mantenimiento. nombre DNS de Hello será estable porque puede ser redirigido tooa nueva dirección IP.)  

1. En el Portal de Azure de hello (o del paso anterior de hello), seleccione **máquinas virtuales (clásicas)**.
2. Seleccione la máquina virtual de SQL.
3. En hello **Máquina Virtual** hoja, Hola copia **nombre DNS** para la máquina virtual de Hola.
   
    ![Nombre DNS](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Conectar toohello motor de base de datos desde otro equipo
1. En un equipo conectado toohello internet, abra SQL Server Management Studio.
2. Hola **conectar tooServer** o **conectar tooDatabase motor** cuadro de diálogo hello **nombre del servidor** cuadro, escriba el nombre DNS de Hola de máquina virtual de hello (determinada en hello tarea anterior) y un número de puerto de extremo público en formato de Hola de *DNSName, portnumber* como **mysqlvm.cloudapp.net,57500**.
   
    ![Conectar mediante SSMS](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Si no recuerda el número de puerto de extremo público de Hola que creó anteriormente, puede encontrarlo en hello **extremos** área de hello **Máquina Virtual** hoja.
   
    ![Public Port](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. Hola **autenticación** cuadro, seleccione **autenticación de SQL Server**.
4. Hola **inicio de sesión** cuadro, escriba un nombre Hola de un inicio de sesión que creó en una tarea anterior.
5. Hola **contraseña** cuadro, escriba la contraseña de inicio de sesión de Hola que cree en una tarea anterior Hola.
6. Haga clic en **Conectar**.

