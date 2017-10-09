agente de escucha del grupo de disponibilidad de Hello es un nombre de red y dirección IP que Hola SQL Server escucha de grupo de disponibilidad en. escucha de grupo de disponibilidad de hello toocreate, Hola siguientes:

1. <a name="getnet"></a>Obtener nombre de Hola Hola red del recurso de clúster.

    a. Utilice RDP tooconnect toohello máquina virtual de Azure que hospeda la réplica principal de Hola. 

    b. Abra el Administrador de clústeres de conmutación por error.

    c. Seleccione hello **redes** nodo y nombre de red del clúster de Hola de nota. Use este nombre en hello `$ClusterNetworkName` variable Hola script de PowerShell. Hola siguiente nombre de red del clúster de imagen hello es **1 de red de clúster**:

   ![Nombre de red del clúster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Agregar punto de acceso de cliente de Hola.  
    punto de acceso de cliente de Hello es el nombre de red de Hola que las aplicaciones utilizan las bases de datos de tooconnect toohello en un grupo de disponibilidad. Crear punto de acceso de cliente de hello en el Administrador de clústeres de conmutación por error.

    a. Expanda el nombre del clúster de hello y, a continuación, haga clic en **Roles**.

    b. Hola **Roles** panel, grupo de disponibilidad de hello contextual nombre y, a continuación, seleccione **Agregar recurso** > **punto de acceso de cliente**.

   ![Punto de acceso cliente](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. Hola **nombre** cuadro, cree un nombre para este nuevo agente de escucha. 
   nombre de Hello para el nuevo agente de escucha de hello es el nombre de red de Hola que las aplicaciones utilizan tooconnect toodatabases en grupo de disponibilidad de SQL Server de Hola.
   
    d. Haga clic en toofinish crear el agente de escucha de hello, **siguiente** dos veces y, a continuación, haga clic en **finalizar**. No detenga el agente de escucha de Hola o recurso en línea en este momento.

3. <a name="congroup"></a>Configurar el recurso IP de Hola Hola grupo de disponibilidad.

    a. Haga clic en hello **recursos** ficha y, a continuación, expanda el punto de acceso de cliente de Hola que creó.  
    punto de acceso de cliente de Hello está sin conexión.

   ![Punto de acceso cliente](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Haga clic en recurso IP de hello y, a continuación, haga clic en Propiedades. Tenga en cuenta Hola nombre de dirección IP de Hola y usarla en hello `$IPResourceName` variable Hola script de PowerShell.

    c. En **Dirección IP**, haga clic en **Dirección IP estática**. Establecer la dirección IP de Hola que hello igual de direcciones que usa cuando se establece la dirección del equilibrador de carga de hello en hello portal de Azure.

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Asegúrese de recurso de grupo de disponibilidad de SQL Server de hello depende del punto de acceso de cliente de Hola.

    a. En el Administrador de clústeres de conmutación por error, haga clic en **Roles** y, después, en el grupo de disponibilidad.

    b. En hello **recursos** ficha **otros recursos**, haga clic en grupo de recursos de disponibilidad de hello y, a continuación, haga clic en **propiedades**. 

    c. En la ficha dependencias de hello, agregue el nombre de Hola Hola acceso punto (agente de escucha de hello) del recurso de cliente.

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. Haga clic en **Aceptar**.

5. <a name="listname"></a>Hacer que el acceso de cliente de hello elija recursos depende de la dirección IP de Hola.

    a. En el Administrador de clústeres de conmutación por error, haga clic en **Roles** y, después, en el grupo de disponibilidad. 

    b. En hello **recursos** pestaña, haga clic en recurso de punto de acceso de cliente de hello en **nombre del servidor**y, a continuación, haga clic en **propiedades**. 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Haga clic en hello **dependencias** ficha. Compruebe que la dirección IP de hello es una dependencia. Si no es así, establecer una dependencia en la dirección IP de Hola. Si hay varios recursos de la lista, compruebe que las direcciones IP Hola tienen o no AND, las dependencias. Haga clic en **Aceptar**. 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **poner en conexión**. 

    >[!TIP]
    >Puede validar ese Hola dependencias están configuradas correctamente. En el Administrador de clústeres de conmutación por error, vaya a tooRoles, haga clic en grupo de disponibilidad de hello, haga clic en **más acciones**y, a continuación, haga clic en **Mostrar informe de dependencias**. Cuando las dependencias de hello estén configuradas correctamente, grupo de disponibilidad de hello es dependiente de nombre de red de Hola y nombre de red de hello es dependiente de la dirección IP de Hola. 


6. <a name="setparam"></a>Establecer parámetros de clúster de hello en PowerShell.
    
    a. Copie Hola después tooone de secuencia de comandos de PowerShell de las instancias de SQL Server. Actualice las variables de Hola para su entorno.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Establecer parámetros de clúster de hello ejecutando Hola script de PowerShell en uno de los nodos de clúster de Hola.  

    > [!NOTE]
    > Si las instancias de SQL Server se encuentran en regiones independientes, debe script de PowerShell de hello toorun dos veces. Hola la primera vez, utilice hello `$ILBIP` y `$ProbePort` desde la primera área de Hola. Hola segunda vez, utilice hello `$ILBIP` y `$ProbePort` de región del segundo Hola. nombre de red del clúster de Hola y nombre de recurso IP de clúster de Hola se Hola mismo. 
