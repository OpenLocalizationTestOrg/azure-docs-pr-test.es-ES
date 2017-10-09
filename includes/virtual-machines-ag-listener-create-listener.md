<span data-ttu-id="bec74-101">En este paso, se crea manualmente el agente de escucha del grupo de disponibilidad de hello en el Administrador de clústeres de conmutación por error y SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="bec74-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="bec74-102">Abra el Administrador de clústeres de conmutación por error de nodo de Hola que hospeda la réplica principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="bec74-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="bec74-103">Seleccione hello **redes** nodo y, a continuación, el nombre de red de clúster de Hola de nota.</span><span class="sxs-lookup"><span data-stu-id="bec74-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="bec74-104">Este nombre se usa en la variable de hello $ClusterNetworkName Hola script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bec74-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="bec74-105">Expanda el nombre del clúster de hello y, a continuación, haga clic en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="bec74-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="bec74-106">Hola **Roles** panel, grupo de disponibilidad de hello contextual nombre y, a continuación, seleccione **Agregar recurso** > **punto de acceso de cliente**.</span><span class="sxs-lookup"><span data-stu-id="bec74-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Agregar un punto de acceso cliente para el grupo de disponibilidad](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="bec74-108">Hola **nombre** cuadro, cree un nombre para este nuevo agente de escucha, haga clic en **siguiente** dos veces y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="bec74-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="bec74-109">No detenga el agente de escucha de Hola o recurso en línea en este momento.</span><span class="sxs-lookup"><span data-stu-id="bec74-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="bec74-110">Haga clic en hello **recursos** ficha y, a continuación, expanda el punto de acceso de cliente de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="bec74-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="bec74-111">se muestra el recurso de dirección IP de Hola para cada red de clúster en el clúster.</span><span class="sxs-lookup"><span data-stu-id="bec74-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="bec74-112">Si se trata de una solución solo de Azure, se muestra un único recurso de dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bec74-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="bec74-113">Realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="bec74-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="bec74-114">tooconfigure una solución híbrida:</span><span class="sxs-lookup"><span data-stu-id="bec74-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="bec74-115">a.</span><span class="sxs-lookup"><span data-stu-id="bec74-115">a.</span></span> <span data-ttu-id="bec74-116">Haga clic en recurso de dirección IP de Hola que corresponde la subred local de tooyour y, a continuación, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="bec74-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="bec74-117">Observe el nombre de dirección IP de Hola y el nombre de red.</span><span class="sxs-lookup"><span data-stu-id="bec74-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="bec74-118">b.</span><span class="sxs-lookup"><span data-stu-id="bec74-118">b.</span></span> <span data-ttu-id="bec74-119">Seleccione **Dirección IP estática**, asigne una dirección IP no utilizada y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bec74-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="bec74-120">tooconfigure una solución solo de Azure:</span><span class="sxs-lookup"><span data-stu-id="bec74-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="bec74-121">a.</span><span class="sxs-lookup"><span data-stu-id="bec74-121">a.</span></span> <span data-ttu-id="bec74-122">Haga clic en recurso de dirección IP de hello correspondiente tooyour subred de Azure y, a continuación, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="bec74-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="bec74-123">Si el agente de escucha de hello más adelante se produce un error toocome en línea debido a una dirección IP en conflicto seleccionada por DHCP, puede configurar una dirección IP estática válida en esta ventana de propiedades.</span><span class="sxs-lookup"><span data-stu-id="bec74-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="bec74-124">b.</span><span class="sxs-lookup"><span data-stu-id="bec74-124">b.</span></span> <span data-ttu-id="bec74-125">En Hola mismo **dirección IP** ventana Propiedades, cambiar hello **nombre de dirección IP**.</span><span class="sxs-lookup"><span data-stu-id="bec74-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="bec74-126">Este nombre se usa en la variable de hello $IPResourceName de hello script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bec74-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="bec74-127">Si la solución abarca varias redes virtuales de Azure, repita este paso para cada recurso de dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bec74-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

