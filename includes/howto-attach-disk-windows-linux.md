


## <a name="attach-an-empty-disk"></a><span data-ttu-id="d799b-101">Conectar un disco vacío</span><span class="sxs-lookup"><span data-stu-id="d799b-101">Attach an empty disk</span></span>
<span data-ttu-id="d799b-102">Conectar un disco vacío es un tooadd de manera sencilla disco de datos, ya que Azure crea el archivo .vhd de hello automáticamente y lo almacena en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d799b-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="d799b-103">Haga clic en **máquinas virtuales (clásicas)**, y, a continuación, seleccione Hola VM adecuado.</span><span class="sxs-lookup"><span data-stu-id="d799b-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="d799b-104">En el menú de configuración de hello, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="d799b-104">In hello Settings menu, click **Disks**.</span></span>

   ![Conectar un nuevo disco vacío](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="d799b-106">En la barra de comandos de hello, haga clic en **adjuntar nuevas**.</span><span class="sxs-lookup"><span data-stu-id="d799b-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="d799b-107">Hola **adjuntar nuevo disco** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d799b-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Conexión de un disco nuevo](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="d799b-109">Rellene Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d799b-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="d799b-110">En **nombre de archivo**, acepte el nombre predeterminado de Hola o escriba otro archivo .vhd de Hola.</span><span class="sxs-lookup"><span data-stu-id="d799b-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="d799b-111">disco de datos de Hello usa un nombre generado automáticamente, incluso si escribe otro nombre para el archivo .vhd de Hola.</span><span class="sxs-lookup"><span data-stu-id="d799b-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="d799b-112">Seleccione hello **tipo** Hola disco de datos.</span><span class="sxs-lookup"><span data-stu-id="d799b-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="d799b-113">Todas las máquinas virtuales admiten discos estándares.</span><span class="sxs-lookup"><span data-stu-id="d799b-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="d799b-114">Muchas máquinas virtuales también admiten discos premium.</span><span class="sxs-lookup"><span data-stu-id="d799b-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="d799b-115">Seleccione hello **tamaño (GB)** Hola disco de datos.</span><span class="sxs-lookup"><span data-stu-id="d799b-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="d799b-116">Para **Almacenamiento en caché de host**, elija Ninguno o Solo lectura.</span><span class="sxs-lookup"><span data-stu-id="d799b-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="d799b-117">Haga clic en Aceptar toofinish.</span><span class="sxs-lookup"><span data-stu-id="d799b-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="d799b-118">Después de crear disco de datos de Hola y conectado, se muestra en la sección de discos de Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d799b-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Disco de datos nuevo y vacío conectado correctamente](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="d799b-120">Después de agregar un disco de datos, es necesario toolog en toohello VM e inicializar disco Hola para que se puede utilizar.</span><span class="sxs-lookup"><span data-stu-id="d799b-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="d799b-121">Acoplamiento de un disco existente</span><span class="sxs-lookup"><span data-stu-id="d799b-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="d799b-122">El acoplamiento de un disco existente requiere que disponga de un .vhd disponible en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d799b-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="d799b-123">Hola de uso [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cuenta de almacenamiento toohello de archivo .vhd de hello tooupload de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d799b-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="d799b-124">Una vez que haya creado y cargado el archivo .vhd de hello, puede adjuntarla tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d799b-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="d799b-125">Haga clic en **máquinas virtuales (clásicas)**, y, a continuación, seleccione Hola máquina virtual adecuada.</span><span class="sxs-lookup"><span data-stu-id="d799b-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="d799b-126">En el menú de configuración de hello, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="d799b-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="d799b-127">En la barra de comandos de hello, haga clic en **adjuntar existente**.</span><span class="sxs-lookup"><span data-stu-id="d799b-127">On hello command bar, click **Attach existing**.</span></span>

    ![Acoplar disco de datos](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="d799b-129">Haga clic en **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="d799b-129">Click **Location**.</span></span> <span data-ttu-id="d799b-130">mostrar las cuentas de almacenamiento disponible de Hola.</span><span class="sxs-lookup"><span data-stu-id="d799b-130">hello available storage accounts display.</span></span> <span data-ttu-id="d799b-131">A continuación, seleccione una cuenta de almacenamiento adecuada de las que aparecen.</span><span class="sxs-lookup"><span data-stu-id="d799b-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Proporcionar la cuenta de almacenamiento de disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="d799b-133">Una **cuenta de almacenamiento** contiene uno o varios contenedores que contienen unidades de disco (discos duros virtuales).</span><span class="sxs-lookup"><span data-stu-id="d799b-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="d799b-134">Seleccione el contenedor adecuado de Hola de los que aparecen.</span><span class="sxs-lookup"><span data-stu-id="d799b-134">Select hello appropriate container from those listed.</span></span>

    ![Proporcionar el contenedor de máquinas virtuales Windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="d799b-136">Hola **discos duros virtuales** panel muestra las unidades de disco de hello mantenidas en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="d799b-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="d799b-137">Haga clic en uno de los discos de hello y, a continuación, haga clic en seleccionar.</span><span class="sxs-lookup"><span data-stu-id="d799b-137">Click one of hello disks, and then click Select.</span></span>

    ![Proporcionar la imagen de disco para máquinas virtuales de Windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="d799b-139">Hola **adjuntar el disco existente** panel se mostrará de nuevo con la ubicación de Hola que contiene la cuenta de almacenamiento de hello, contenedor y máquina virtual de disco duro seleccionado (vhd) tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="d799b-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="d799b-140">Establecer **hospedar el almacenamiento en caché** toonone o lectura únicamente, a continuación, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="d799b-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Disco de datos conectado correctamente](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
