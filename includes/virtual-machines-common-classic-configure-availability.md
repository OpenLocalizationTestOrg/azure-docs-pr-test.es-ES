


<span data-ttu-id="28331-101">Un conjunto de disponibilidad ayuda a mantener las máquinas virtuales disponibles durante períodos de inactividad, como por ejemplo mientras se realiza mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="28331-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="28331-102">Colocar dos o más máquinas virtuales configuradas de manera similar en un conjunto de disponibilidad crea Hola redundancia necesitado toomaintain disponibilidad de aplicaciones de Hola o servicios que se ejecuta la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="28331-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="28331-103">Para obtener más información acerca de cómo funciona esto, consulte [administrar Hola disponibilidad de máquinas virtuales][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="28331-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="28331-104">Es una mejor toouse práctica conjuntos de disponibilidad y equilibrio de carga extremos toohelp aseguran de que la aplicación está siempre disponible y se ejecuta eficazmente.</span><span class="sxs-lookup"><span data-stu-id="28331-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="28331-105">Para obtener información detallada acerca de los puntos de conexión de carga equilibrada, consulte [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services] (Equilibrio de carga en los servicios de infraestructura de Azure).</span><span class="sxs-lookup"><span data-stu-id="28331-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="28331-106">Puede agregar máquinas virtuales clásicas en un conjunto de disponibilidad mediante una de estas dos opciones:</span><span class="sxs-lookup"><span data-stu-id="28331-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="28331-107">[Opción 1: Crear una máquina virtual y un conjunto de disponibilidad en hello mismo tiempo][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="28331-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="28331-108">A continuación, agregue nuevas toohello de máquinas virtuales configurada al crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="28331-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="28331-109">[Opción 2: Agregar un conjunto de disponibilidad de tooan de máquina virtual existente][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="28331-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="28331-110">En el modelo clásico de hello, máquinas virtuales que desea tooput en Hola mismo conjunto de disponibilidad debe pertenecer toohello mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="28331-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="28331-111"><a id="createset"></a>Opción 1: crear una máquina virtual y un conjunto de disponibilidad en hello mismo tiempo</span><span class="sxs-lookup"><span data-stu-id="28331-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="28331-112">Puede usar cualquier Hola portal de Azure o Azure PowerShell comandos toodo esto.</span><span class="sxs-lookup"><span data-stu-id="28331-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="28331-113">Hola toouse portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="28331-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="28331-114">Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="28331-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="28331-115">En el menú del concentrador hello, haga clic en **+ nuevo**y, a continuación, haga clic en **Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="28331-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="28331-117">Seleccione la imagen de máquina virtual de Marketplace de hello desea toouse.</span><span class="sxs-lookup"><span data-stu-id="28331-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="28331-118">Puede elegir toocreate una máquina virtual Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="28331-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="28331-119">Para hello selecciona máquina virtual, compruebe que ese modelo de implementación de Hola se establece demasiado**clásico** y, a continuación, haga clic en **crear**</span><span class="sxs-lookup"><span data-stu-id="28331-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="28331-121">Escriba un nombre de máquina virtual, un nombre de usuario y una contraseña (para máquinas con Windows) o la clave pública SSH (para equipos con Linux).</span><span class="sxs-lookup"><span data-stu-id="28331-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="28331-122">Elija el tamaño de la máquina virtual de hello y, a continuación, haga clic en **seleccione** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="28331-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="28331-123">Elija **configuración opcional > conjunto de disponibilidad**y seleccione el conjunto de disponibilidad de hello desea tooadd Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="28331-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="28331-125">Revise las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="28331-125">Review your configuration settings.</span></span> <span data-ttu-id="28331-126">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="28331-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="28331-127">Mientras Azure crea la máquina virtual, puede seguir el progreso de hello en **máquinas virtuales** en el menú del concentrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="28331-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="28331-128">toouse Azure PowerShell comandos toocreate una máquina virtual de Azure y Agregar conjunto de disponibilidad nuevo o existente de tooa, consulte [toocreate usar Azure PowerShell y preconfigurar máquinas virtuales basadas en Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28331-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="28331-129"><a id="addmachine"></a>Opción 2: agregar un conjunto de disponibilidad de tooan de máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="28331-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="28331-130">Hola portal de Azure, puede agregar existente tooan de máquinas virtuales clásicas existente conjunto de disponibilidad o cree uno nuevo para ellos.</span><span class="sxs-lookup"><span data-stu-id="28331-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="28331-131">(Tenga en cuenta que las máquinas virtuales de hello en Hola mismo conjunto de disponibilidad debe pertenecer toohello mismo servicio en la nube.) pasos de Hello son casi Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="28331-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="28331-132">Con Azure PowerShell, puede agregar conjunto de disponibilidad existente de tooan de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="28331-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="28331-133">Si no lo ha hecho ya, inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="28331-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="28331-134">En el menú del concentrador hello, haga clic en **máquinas virtuales (clásicas)**.</span><span class="sxs-lookup"><span data-stu-id="28331-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="28331-136">En lista de Hola de máquinas virtuales, seleccione el nombre de Hola de máquina virtual de Hola que desee tooadd toohello establecer.</span><span class="sxs-lookup"><span data-stu-id="28331-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="28331-137">Elija **conjunto de disponibilidad** de la máquina virtual de hello **configuración**.</span><span class="sxs-lookup"><span data-stu-id="28331-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="28331-139">Seleccione conjunto de disponibilidad de hello que desea tooadd Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="28331-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="28331-140">máquina virtual de Hello debe pertenecer toohello mismo servicio en la nube como conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="28331-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="28331-142">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="28331-142">Click **Save**.</span></span>

<span data-ttu-id="28331-143">comandos de PowerShell de Azure toouse, abra una sesión de PowerShell de Azure de nivel de administrador y ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="28331-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="28331-144">Para los marcadores de posición de hello (como &lt;VmCloudServiceName&gt;), reemplace todo el contenido de las comillas de hello, incluidos los caracteres de Hola < y >, con hello corregir nombres.</span><span class="sxs-lookup"><span data-stu-id="28331-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="28331-145">máquina virtual de Hello podría tener toofinish toobe reinicia Agregar conjunto de disponibilidad toohello.</span><span class="sxs-lookup"><span data-stu-id="28331-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

