1. <span data-ttu-id="02218-101">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02218-101">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="02218-102">A partir de la parte superior izquierda de hello, haga clic en **nuevo > proceso > Centro de datos de Windows Server 2016**.</span><span class="sxs-lookup"><span data-stu-id="02218-102">Starting in hello upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Navegue toohello imágenes de máquina virtual de Azure en el portal de Hola](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="02218-104">En Windows Server 2016 Datacenter hello, seleccione el modelo de implementación de clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-104">On hello Windows Server 2016 Datacenter, select hello Classic deployment model.</span></span> <span data-ttu-id="02218-105">Haga clic en Crear.</span><span class="sxs-lookup"><span data-stu-id="02218-105">Click Create.</span></span>

    ![Captura de pantalla que muestra las imágenes de máquina virtual de Azure de hello disponibles en el portal de Hola](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="02218-107">1. Hoja Básico</span><span class="sxs-lookup"><span data-stu-id="02218-107">1. Basics blade</span></span>

<span data-ttu-id="02218-108">hoja de conceptos básicos de Hello solicita la información administrativa para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-108">hello Basics blade requests administrative information for hello virtual machine.</span></span>

1. <span data-ttu-id="02218-109">Escriba un **nombre** para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-109">Enter a **Name** for hello virtual machine.</span></span> <span data-ttu-id="02218-110">En el ejemplo de Hola, _HeroVM_ es Hola nombre de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-110">In hello example, _HeroVM_ is hello name of hello virtual machine.</span></span> <span data-ttu-id="02218-111">nombre de Hello debe ser 1 y 15 caracteres y no puede contener caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="02218-111">hello name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="02218-112">Escriba un **nombre de usuario** y una gran **contraseña** que están toocreate usa una cuenta local en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="02218-112">Enter a **User name** and a strong **Password** that are used toocreate a local account on hello VM.</span></span> <span data-ttu-id="02218-113">Hello cuenta local se usa toosign en tooand administrar Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="02218-113">hello local account is used toosign in tooand manage hello VM.</span></span> <span data-ttu-id="02218-114">En el ejemplo de Hola, _azureuser_ es el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-114">In hello example, _azureuser_ is hello user name.</span></span>

 <span data-ttu-id="02218-115">Hello contraseña debe tener 8-123 caracteres de longitud y satisfacer tres de hello cuatro requisitos de complejidad: caracteres de una minúscula, una letra mayúscula, un número y un carácter especial.</span><span class="sxs-lookup"><span data-stu-id="02218-115">hello password must be 8-123 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="02218-116">Obtenga más información acerca de los [requisitos de usuario y la contraseña](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="02218-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="02218-117">Hola **suscripción** es opcional.</span><span class="sxs-lookup"><span data-stu-id="02218-117">hello **Subscription** is optional.</span></span> <span data-ttu-id="02218-118">Una configuración común es "Pago por uso".</span><span class="sxs-lookup"><span data-stu-id="02218-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="02218-119">Seleccione una existente **grupo de recursos** o nombre de tipo hello para uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="02218-119">Select an existing **Resource group** or type hello name for a new one.</span></span> <span data-ttu-id="02218-120">En el ejemplo de Hola, _HeroVMRG_ es nombre Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="02218-120">In hello example, _HeroVMRG_ is hello name of hello resource group.</span></span>

5. <span data-ttu-id="02218-121">Seleccione un centro de datos Azure **ubicación** donde desea Hola VM toorun.</span><span class="sxs-lookup"><span data-stu-id="02218-121">Select an Azure datacenter **Location** where you want hello VM toorun.</span></span> <span data-ttu-id="02218-122">En el ejemplo de Hola, **UU** es Hola ubicación.</span><span class="sxs-lookup"><span data-stu-id="02218-122">In hello example, **East US** is hello location.</span></span>

6. <span data-ttu-id="02218-123">Cuando haya terminado, haga clic en **siguiente** toocontinue toohello siguiente hoja.</span><span class="sxs-lookup"><span data-stu-id="02218-123">When you are done, click **Next** toocontinue toohello next blade.</span></span>

    ![Captura de pantalla que muestra la configuración de hello en la hoja de hello conceptos básicos para configurar una máquina virtual de Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="02218-125">2. Hoja Tamaño</span><span class="sxs-lookup"><span data-stu-id="02218-125">2. Size blade</span></span>

<span data-ttu-id="02218-126">hoja de tamaño de Hola identifica los detalles de configuración de Hola de hello VM y enumera las distintas opciones que incluyen el sistema operativo, número de procesadores, el tipo de almacenamiento en disco y costos de uso mensual estimado.</span><span class="sxs-lookup"><span data-stu-id="02218-126">hello Size blade identifies hello configuration details of hello VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="02218-127">Elija un tamaño de máquina virtual y, a continuación, haga clic en **seleccione** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="02218-127">Choose a VM size, and then click **Select** toocontinue.</span></span> <span data-ttu-id="02218-128">En este ejemplo, _DS1_\__V2 estándar_ es el tamaño de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-128">In this example, _DS1_\__V2 Standard_ is hello VM size.</span></span>

  ![Captura de pantalla de hoja de tamaño de Hola que muestra hello tamaños de máquina virtual de Azure que se pueden seleccionar](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="02218-130">3. Hoja Configuración</span><span class="sxs-lookup"><span data-stu-id="02218-130">3. Settings blade</span></span>

<span data-ttu-id="02218-131">hoja de configuración de Hello solicita opciones de almacenamiento y red.</span><span class="sxs-lookup"><span data-stu-id="02218-131">hello Settings blade requests storage and network options.</span></span> <span data-ttu-id="02218-132">Puede aceptar la configuración predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-132">You can accept hello default settings.</span></span> <span data-ttu-id="02218-133">Azure crea las entradas correspondientes en caso de ser necesario.</span><span class="sxs-lookup"><span data-stu-id="02218-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="02218-134">Si seleccionó un tamaño de máquina virtual que lo admita, puede probar Azure Premium Storage, para lo que debe seleccionar Premium (SSD) en Tipo de disco.</span><span class="sxs-lookup"><span data-stu-id="02218-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="02218-135">Cuando haya terminado de realizar los cambios, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="02218-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="02218-136">4. Hoja Resumen</span><span class="sxs-lookup"><span data-stu-id="02218-136">4. Summary blade</span></span>

<span data-ttu-id="02218-137">hoja de resumen de Hola enumera los valores de hello especificados en hojas de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="02218-137">hello Summary blade lists hello settings specified in hello previous blades.</span></span> <span data-ttu-id="02218-138">Haga clic en **Aceptar** cuando esté listo toomake imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-138">Click **OK** when you're ready toomake hello image.</span></span>

 ![Informe de resumen de hoja que proporciona los valores especificados de la máquina virtual de Hola](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="02218-140">Después de crear la máquina virtual de hello, Hola portal mostrará las Hola nueva máquina virtual en **todos los recursos**y muestra un icono de la máquina virtual de hello en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="02218-140">After hello virtual machine is created, hello portal lists hello new virtual machine under **All resources**, and displays a tile of hello virtual machine on hello dashboard.</span></span> <span data-ttu-id="02218-141">cuenta de Hello correspondiente en la nube almacenamiento y el servicio también se crean y muestran.</span><span class="sxs-lookup"><span data-stu-id="02218-141">hello corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="02218-142">Máquina virtual de Hola y servicio de nube se inician automáticamente y su estado aparece como **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="02218-142">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Configurar puntos de conexión de máquina virtual de Hola de hello y agente de máquina virtual](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
