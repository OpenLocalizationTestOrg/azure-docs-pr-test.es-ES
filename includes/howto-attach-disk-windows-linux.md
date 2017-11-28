


## <a name="attach-an-empty-disk"></a><span data-ttu-id="2424d-101">Conectar un disco vacío</span><span class="sxs-lookup"><span data-stu-id="2424d-101">Attach an empty disk</span></span>
<span data-ttu-id="2424d-102">El acoplamiento de un disco vacío supone un método sencillo de agregar un disco de datos, porque Azure crea el archivo .vhd y lo guarda en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2424d-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span></span>

1. <span data-ttu-id="2424d-103">Haga clic en **Virtual Machines (clásico)** y luego seleccione la máquina virtual adecuada.</span><span class="sxs-lookup"><span data-stu-id="2424d-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span></span>

2. <span data-ttu-id="2424d-104">En el menú Configuración, haga clic en **Discos**.</span><span class="sxs-lookup"><span data-stu-id="2424d-104">In the Settings menu, click **Disks**.</span></span>

   ![Conectar un nuevo disco vacío](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="2424d-106">En la barra de comandos, haga clic en **Asociar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="2424d-106">On the command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="2424d-107">Aparece el cuadro de diálogo **Asociar nuevo disco**.</span><span class="sxs-lookup"><span data-stu-id="2424d-107">The **Attach new disk** dialog box appears.</span></span>

    ![Conexión de un disco nuevo](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="2424d-109">Rellene la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="2424d-109">Fill in the following information:</span></span>
    - <span data-ttu-id="2424d-110">En **Nombre de archivo**, acepte el nombre predeterminado o escriba otro para el archivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="2424d-110">In **File Name**, accept the default name or type another one for the .vhd file.</span></span> <span data-ttu-id="2424d-111">El disco de datos usa un nombre generado automáticamente, incluso si escribe otro nombre para el archivo .vhd</span><span class="sxs-lookup"><span data-stu-id="2424d-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span></span>
    - <span data-ttu-id="2424d-112">Seleccione el **tipo** del disco de datos.</span><span class="sxs-lookup"><span data-stu-id="2424d-112">Select the **Type** of the data disk.</span></span> <span data-ttu-id="2424d-113">Todas las máquinas virtuales admiten discos estándares.</span><span class="sxs-lookup"><span data-stu-id="2424d-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="2424d-114">Muchas máquinas virtuales también admiten discos premium.</span><span class="sxs-lookup"><span data-stu-id="2424d-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="2424d-115">Seleccione el **tamaño (GB)** del disco de datos.</span><span class="sxs-lookup"><span data-stu-id="2424d-115">Select the **Size (GB)** of the data disk.</span></span>
    - <span data-ttu-id="2424d-116">Para **Almacenamiento en caché de host**, elija Ninguno o Solo lectura.</span><span class="sxs-lookup"><span data-stu-id="2424d-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="2424d-117">Haga clic en Aceptar para finalizar.</span><span class="sxs-lookup"><span data-stu-id="2424d-117">Click OK to finish.</span></span>

4. <span data-ttu-id="2424d-118">Una vez creado y conectado el disco de datos, este aparece en la sección de discos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2424d-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span></span>

   ![Disco de datos nuevo y vacío conectado correctamente](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="2424d-120">Después de agregar un disco de datos, es preciso iniciar sesión en la máquina virtual e inicializar el disco para que se pueda usar.</span><span class="sxs-lookup"><span data-stu-id="2424d-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="2424d-121">Acoplamiento de un disco existente</span><span class="sxs-lookup"><span data-stu-id="2424d-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="2424d-122">El acoplamiento de un disco existente requiere que disponga de un .vhd disponible en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2424d-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="2424d-123">Use el cmdlet [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) para cargar el archivo .vhd a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2424d-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span></span> <span data-ttu-id="2424d-124">Una vez que se haya creado y cargado el archivo .vhd, puede acoplarlo a una VM.</span><span class="sxs-lookup"><span data-stu-id="2424d-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span></span>

1. <span data-ttu-id="2424d-125">Haga clic en **Virtual Machines (clásico)** y luego seleccione la máquina virtual correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2424d-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span></span>

2. <span data-ttu-id="2424d-126">En el menú Configuración, haga clic en **Discos**.</span><span class="sxs-lookup"><span data-stu-id="2424d-126">In the Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="2424d-127">En la barra de comandos, haga clic en **Asociar existente**.</span><span class="sxs-lookup"><span data-stu-id="2424d-127">On the command bar, click **Attach existing**.</span></span>

    ![Acoplar disco de datos](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="2424d-129">Haga clic en **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="2424d-129">Click **Location**.</span></span> <span data-ttu-id="2424d-130">Se muestran las cuentas de almacenamiento disponibles.</span><span class="sxs-lookup"><span data-stu-id="2424d-130">The available storage accounts display.</span></span> <span data-ttu-id="2424d-131">A continuación, seleccione una cuenta de almacenamiento adecuada de las que aparecen.</span><span class="sxs-lookup"><span data-stu-id="2424d-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Proporcionar la cuenta de almacenamiento de disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="2424d-133">Una **cuenta de almacenamiento** contiene uno o varios contenedores que contienen unidades de disco (discos duros virtuales).</span><span class="sxs-lookup"><span data-stu-id="2424d-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="2424d-134">Seleccione el contenedor adecuado de los que aparecen.</span><span class="sxs-lookup"><span data-stu-id="2424d-134">Select the appropriate container from those listed.</span></span>

    ![Proporcionar el contenedor de máquinas virtuales Windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="2424d-136">En el panel de **discos duros virtuales** se muestran las unidades de disco que contiene el contenedor.</span><span class="sxs-lookup"><span data-stu-id="2424d-136">The **vhds** panel lists the disk drives held in the container.</span></span> <span data-ttu-id="2424d-137">Haga clic en uno de los discos y luego en Seleccionar.</span><span class="sxs-lookup"><span data-stu-id="2424d-137">Click one of the disks, and then click Select.</span></span>

    ![Proporcionar la imagen de disco para máquinas virtuales de Windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="2424d-139">Se muestra de nuevo el panel **Asociar disco existente**, con la ubicación que contiene la cuenta de almacenamiento, el contenedor y la unidad de disco duro virtual seleccionada que se agregará a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2424d-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span></span>

  <span data-ttu-id="2424d-140">Establezca **Almacenamiento en caché de host** en Ninguno o Solo lectura y luego haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="2424d-140">Set **Host caching** to none or Read only, then click OK.</span></span>

    ![Disco de datos conectado correctamente](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
