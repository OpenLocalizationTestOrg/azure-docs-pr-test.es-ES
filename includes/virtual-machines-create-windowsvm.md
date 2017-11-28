1. <span data-ttu-id="a507c-101">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a507c-101">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a507c-102">Desde la esquina superior izquierda, haga clic en **Nuevo > Proceso > Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="a507c-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Vaya a las imágenes de máquinas virtuales de Azure en el portal](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="a507c-104">En Windows Server 2016 Datacenter, seleccione el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="a507c-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span></span> <span data-ttu-id="a507c-105">Haga clic en Crear.</span><span class="sxs-lookup"><span data-stu-id="a507c-105">Click Create.</span></span>

    ![Captura de pantalla que muestra las imágenes de las máquinas virtuales de Azure disponibles en el portal](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="a507c-107">1. Hoja Básico</span><span class="sxs-lookup"><span data-stu-id="a507c-107">1. Basics blade</span></span>

<span data-ttu-id="a507c-108">La hoja Básico solicita información administrativa para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a507c-108">The Basics blade requests administrative information for the virtual machine.</span></span>

1. <span data-ttu-id="a507c-109">Escriba un **nombre** para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a507c-109">Enter a **Name** for the virtual machine.</span></span> <span data-ttu-id="a507c-110">En este ejemplo, _HeroVM_ es el nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a507c-110">In the example, _HeroVM_ is the name of the virtual machine.</span></span> <span data-ttu-id="a507c-111">El nombre debe tener de 1 a 15 caracteres de longitud, sin caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="a507c-111">The name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="a507c-112">Escriba un **nombre de usuario** y una **contraseña** segura que se usarán para crear una cuenta local en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a507c-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span></span> <span data-ttu-id="a507c-113">La cuenta local sirve para iniciar sesión en la máquina virtual y administrarla.</span><span class="sxs-lookup"><span data-stu-id="a507c-113">The local account is used to sign in to and manage the VM.</span></span> <span data-ttu-id="a507c-114">En el ejemplo, _azureuser_ es el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="a507c-114">In the example, _azureuser_ is the user name.</span></span>

 <span data-ttu-id="a507c-115">La contraseña debe tener entre 8 y 123 caracteres y reunir, al menos, tres de los cuatro requisitos de complejidad siguientes: contener al menos una minúscula, una mayúscula, un número y un carácter especial.</span><span class="sxs-lookup"><span data-stu-id="a507c-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="a507c-116">Obtenga más información acerca de los [requisitos de usuario y la contraseña](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="a507c-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="a507c-117">La **suscripción** es opcional.</span><span class="sxs-lookup"><span data-stu-id="a507c-117">The **Subscription** is optional.</span></span> <span data-ttu-id="a507c-118">Una configuración común es "Pago por uso".</span><span class="sxs-lookup"><span data-stu-id="a507c-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="a507c-119">Seleccione un valor de **Grupo de recursos** existente o escriba el nombre para crear uno.</span><span class="sxs-lookup"><span data-stu-id="a507c-119">Select an existing **Resource group** or type the name for a new one.</span></span> <span data-ttu-id="a507c-120">En el ejemplo, _HeroVMRG_ es el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a507c-120">In the example, _HeroVMRG_ is the name of the resource group.</span></span>

5. <span data-ttu-id="a507c-121">Seleccione una **ubicación** del centro de datos de Azure donde desea que se ejecute la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a507c-121">Select an Azure datacenter **Location** where you want the VM to run.</span></span> <span data-ttu-id="a507c-122">En el ejemplo, la ubicación es **Este de EE. UU**.</span><span class="sxs-lookup"><span data-stu-id="a507c-122">In the example, **East US** is the location.</span></span>

6. <span data-ttu-id="a507c-123">Cuando termine, haga clic en **Siguiente** para continuar a la hoja siguiente.</span><span class="sxs-lookup"><span data-stu-id="a507c-123">When you are done, click **Next** to continue to the next blade.</span></span>

    ![Captura de pantalla que muestra la configuración en la hoja Básico para configurar una máquina virtual de Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="a507c-125">2. Hoja Tamaño</span><span class="sxs-lookup"><span data-stu-id="a507c-125">2. Size blade</span></span>

<span data-ttu-id="a507c-126">La hoja Tamaño identifica los detalles de configuración de la máquina virtual y enumera diversas opciones que incluyen SO, el número de procesadores, el tipo de almacenamiento en disco y costos de uso mensuales estimados.</span><span class="sxs-lookup"><span data-stu-id="a507c-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="a507c-127">Elija un tamaño de máquina virtual y, luego, **Seleccionar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="a507c-127">Choose a VM size, and then click **Select** to continue.</span></span> <span data-ttu-id="a507c-128">En este ejemplo, _DS1_\__V2 estándar_ es el tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a507c-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span></span>

  ![Captura de pantalla que muestra la hoja Tamaño con los tamaños de máquina virtual de Azure que puede seleccionar](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="a507c-130">3. Hoja Configuración</span><span class="sxs-lookup"><span data-stu-id="a507c-130">3. Settings blade</span></span>

<span data-ttu-id="a507c-131">La hoja Configuración solicita las opciones de almacenamiento y red.</span><span class="sxs-lookup"><span data-stu-id="a507c-131">The Settings blade requests storage and network options.</span></span> <span data-ttu-id="a507c-132">Puede aceptar la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a507c-132">You can accept the default settings.</span></span> <span data-ttu-id="a507c-133">Azure crea las entradas correspondientes en caso de ser necesario.</span><span class="sxs-lookup"><span data-stu-id="a507c-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="a507c-134">Si seleccionó un tamaño de máquina virtual que lo admita, puede probar Azure Premium Storage, para lo que debe seleccionar Premium (SSD) en Tipo de disco.</span><span class="sxs-lookup"><span data-stu-id="a507c-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="a507c-135">Cuando haya terminado de realizar los cambios, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a507c-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="a507c-136">4. Hoja Resumen</span><span class="sxs-lookup"><span data-stu-id="a507c-136">4. Summary blade</span></span>

<span data-ttu-id="a507c-137">La hoja Resumen enumera la configuración que se especificó en las hojas anteriores.</span><span class="sxs-lookup"><span data-stu-id="a507c-137">The Summary blade lists the settings specified in the previous blades.</span></span> <span data-ttu-id="a507c-138">Haga clic en **Aceptar** cuando esté listo para crear la imagen.</span><span class="sxs-lookup"><span data-stu-id="a507c-138">Click **OK** when you're ready to make the image.</span></span>

 ![Informe de la hoja Resumen que proporciona la configuración especificada de la máquina virtual](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="a507c-140">Una vez creada la máquina virtual, en el portal se muestra la máquina virtual nueva en **Todos los recursos** y muestra un icono de la máquina virtual en el panel.</span><span class="sxs-lookup"><span data-stu-id="a507c-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span></span> <span data-ttu-id="a507c-141">También se crean y muestran el servicio en la nube y la cuenta de almacenamiento correspondientes.</span><span class="sxs-lookup"><span data-stu-id="a507c-141">The corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="a507c-142">La máquina virtual y el servicio en la nube se inician automáticamente, y su estado aparece como **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="a507c-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Configure el agente de máquina virtual y los puntos de conexión de la máquina virtual](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
