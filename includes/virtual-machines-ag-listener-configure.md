<span data-ttu-id="20aa8-101">agente de escucha del grupo de disponibilidad de Hello es un nombre de red y dirección IP que Hola SQL Server escucha de grupo de disponibilidad en.</span><span class="sxs-lookup"><span data-stu-id="20aa8-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="20aa8-102">escucha de grupo de disponibilidad de hello toocreate, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="20aa8-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="20aa8-103"><a name="getnet"></a>Obtener nombre de Hola Hola red del recurso de clúster.</span><span class="sxs-lookup"><span data-stu-id="20aa8-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="20aa8-104">a.</span><span class="sxs-lookup"><span data-stu-id="20aa8-104">a.</span></span> <span data-ttu-id="20aa8-105">Utilice RDP tooconnect toohello máquina virtual de Azure que hospeda la réplica principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="20aa8-106">b.</span><span class="sxs-lookup"><span data-stu-id="20aa8-106">b.</span></span> <span data-ttu-id="20aa8-107">Abra el Administrador de clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="20aa8-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="20aa8-108">c.</span><span class="sxs-lookup"><span data-stu-id="20aa8-108">c.</span></span> <span data-ttu-id="20aa8-109">Seleccione hello **redes** nodo y nombre de red del clúster de Hola de nota.</span><span class="sxs-lookup"><span data-stu-id="20aa8-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="20aa8-110">Use este nombre en hello `$ClusterNetworkName` variable Hola script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20aa8-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="20aa8-111">Hola siguiente nombre de red del clúster de imagen hello es **1 de red de clúster**:</span><span class="sxs-lookup"><span data-stu-id="20aa8-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![Nombre de red del clúster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="20aa8-113"><a name="addcap"></a>Agregar punto de acceso de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="20aa8-114">punto de acceso de cliente de Hello es el nombre de red de Hola que las aplicaciones utilizan las bases de datos de tooconnect toohello en un grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="20aa8-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="20aa8-115">Crear punto de acceso de cliente de hello en el Administrador de clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="20aa8-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="20aa8-116">a.</span><span class="sxs-lookup"><span data-stu-id="20aa8-116">a.</span></span> <span data-ttu-id="20aa8-117">Expanda el nombre del clúster de hello y, a continuación, haga clic en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="20aa8-118">b.</span><span class="sxs-lookup"><span data-stu-id="20aa8-118">b.</span></span> <span data-ttu-id="20aa8-119">Hola **Roles** panel, grupo de disponibilidad de hello contextual nombre y, a continuación, seleccione **Agregar recurso** > **punto de acceso de cliente**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Punto de acceso cliente](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="20aa8-121">c.</span><span class="sxs-lookup"><span data-stu-id="20aa8-121">c.</span></span> <span data-ttu-id="20aa8-122">Hola **nombre** cuadro, cree un nombre para este nuevo agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="20aa8-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="20aa8-123">nombre de Hello para el nuevo agente de escucha de hello es el nombre de red de Hola que las aplicaciones utilizan tooconnect toodatabases en grupo de disponibilidad de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="20aa8-124">d.</span><span class="sxs-lookup"><span data-stu-id="20aa8-124">d.</span></span> <span data-ttu-id="20aa8-125">Haga clic en toofinish crear el agente de escucha de hello, **siguiente** dos veces y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="20aa8-126">No detenga el agente de escucha de Hola o recurso en línea en este momento.</span><span class="sxs-lookup"><span data-stu-id="20aa8-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="20aa8-127"><a name="congroup"></a>Configurar el recurso IP de Hola Hola grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="20aa8-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="20aa8-128">a.</span><span class="sxs-lookup"><span data-stu-id="20aa8-128">a.</span></span> <span data-ttu-id="20aa8-129">Haga clic en hello **recursos** ficha y, a continuación, expanda el punto de acceso de cliente de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="20aa8-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="20aa8-130">punto de acceso de cliente de Hello está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="20aa8-130">hello client access point is offline.</span></span>

   ![Punto de acceso cliente](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="20aa8-132">b.</span><span class="sxs-lookup"><span data-stu-id="20aa8-132">b.</span></span> <span data-ttu-id="20aa8-133">Haga clic en recurso IP de hello y, a continuación, haga clic en Propiedades.</span><span class="sxs-lookup"><span data-stu-id="20aa8-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="20aa8-134">Tenga en cuenta Hola nombre de dirección IP de Hola y usarla en hello `$IPResourceName` variable Hola script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20aa8-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="20aa8-135">c.</span><span class="sxs-lookup"><span data-stu-id="20aa8-135">c.</span></span> <span data-ttu-id="20aa8-136">En **Dirección IP**, haga clic en **Dirección IP estática**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="20aa8-137">Establecer la dirección IP de Hola que hello igual de direcciones que usa cuando se establece la dirección del equilibrador de carga de hello en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="20aa8-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="20aa8-139"><a name = "dependencyGroup"></a>Asegúrese de recurso de grupo de disponibilidad de SQL Server de hello depende del punto de acceso de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="20aa8-140">a.</span><span class="sxs-lookup"><span data-stu-id="20aa8-140">a.</span></span> <span data-ttu-id="20aa8-141">En el Administrador de clústeres de conmutación por error, haga clic en **Roles** y, después, en el grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="20aa8-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="20aa8-142">b.</span><span class="sxs-lookup"><span data-stu-id="20aa8-142">b.</span></span> <span data-ttu-id="20aa8-143">En hello **recursos** ficha **otros recursos**, haga clic en grupo de recursos de disponibilidad de hello y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="20aa8-144">c.</span><span class="sxs-lookup"><span data-stu-id="20aa8-144">c.</span></span> <span data-ttu-id="20aa8-145">En la ficha dependencias de hello, agregue el nombre de Hola Hola acceso punto (agente de escucha de hello) del recurso de cliente.</span><span class="sxs-lookup"><span data-stu-id="20aa8-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="20aa8-147">d.</span><span class="sxs-lookup"><span data-stu-id="20aa8-147">d.</span></span> <span data-ttu-id="20aa8-148">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-148">Click **OK**.</span></span>

5. <span data-ttu-id="20aa8-149"><a name="listname"></a>Hacer que el acceso de cliente de hello elija recursos depende de la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="20aa8-150">a.</span><span class="sxs-lookup"><span data-stu-id="20aa8-150">a.</span></span> <span data-ttu-id="20aa8-151">En el Administrador de clústeres de conmutación por error, haga clic en **Roles** y, después, en el grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="20aa8-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="20aa8-152">b.</span><span class="sxs-lookup"><span data-stu-id="20aa8-152">b.</span></span> <span data-ttu-id="20aa8-153">En hello **recursos** pestaña, haga clic en recurso de punto de acceso de cliente de hello en **nombre del servidor**y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="20aa8-155">c.</span><span class="sxs-lookup"><span data-stu-id="20aa8-155">c.</span></span> <span data-ttu-id="20aa8-156">Haga clic en hello **dependencias** ficha. Compruebe que la dirección IP de hello es una dependencia.</span><span class="sxs-lookup"><span data-stu-id="20aa8-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="20aa8-157">Si no es así, establecer una dependencia en la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="20aa8-158">Si hay varios recursos de la lista, compruebe que las direcciones IP Hola tienen o no AND, las dependencias.</span><span class="sxs-lookup"><span data-stu-id="20aa8-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="20aa8-159">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-159">Click **OK**.</span></span> 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="20aa8-161">d.</span><span class="sxs-lookup"><span data-stu-id="20aa8-161">d.</span></span> <span data-ttu-id="20aa8-162">Haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **poner en conexión**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="20aa8-163">Puede validar ese Hola dependencias están configuradas correctamente.</span><span class="sxs-lookup"><span data-stu-id="20aa8-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="20aa8-164">En el Administrador de clústeres de conmutación por error, vaya a tooRoles, haga clic en grupo de disponibilidad de hello, haga clic en **más acciones**y, a continuación, haga clic en **Mostrar informe de dependencias**.</span><span class="sxs-lookup"><span data-stu-id="20aa8-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="20aa8-165">Cuando las dependencias de hello estén configuradas correctamente, grupo de disponibilidad de hello es dependiente de nombre de red de Hola y nombre de red de hello es dependiente de la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="20aa8-166"><a name="setparam"></a>Establecer parámetros de clúster de hello en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20aa8-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="20aa8-167">a.</span><span class="sxs-lookup"><span data-stu-id="20aa8-167">a.</span></span> <span data-ttu-id="20aa8-168">Copie Hola después tooone de secuencia de comandos de PowerShell de las instancias de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="20aa8-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="20aa8-169">Actualice las variables de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="20aa8-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="20aa8-170">b.</span><span class="sxs-lookup"><span data-stu-id="20aa8-170">b.</span></span> <span data-ttu-id="20aa8-171">Establecer parámetros de clúster de hello ejecutando Hola script de PowerShell en uno de los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="20aa8-172">Si las instancias de SQL Server se encuentran en regiones independientes, debe script de PowerShell de hello toorun dos veces.</span><span class="sxs-lookup"><span data-stu-id="20aa8-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="20aa8-173">Hola la primera vez, utilice hello `$ILBIP` y `$ProbePort` desde la primera área de Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="20aa8-174">Hola segunda vez, utilice hello `$ILBIP` y `$ProbePort` de región del segundo Hola.</span><span class="sxs-lookup"><span data-stu-id="20aa8-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="20aa8-175">nombre de red del clúster de Hola y nombre de recurso IP de clúster de Hola se Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="20aa8-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
