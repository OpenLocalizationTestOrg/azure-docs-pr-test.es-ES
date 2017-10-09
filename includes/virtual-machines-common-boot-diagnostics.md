<span data-ttu-id="e9ea9-101">Ahora se ofrece en Azure compatibilidad con dos características de depuración, Salida de la consola y Captura de pantalla, para el modelo de implementación de Resource Manager en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="e9ea9-102">Al volver a poner su propia imagen tooAzure o incluso arranque uno de imágenes de la plataforma de hello, puede haber muchas razones, ¿por qué se obtiene una máquina Virtual en un estado no sean de arranque.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="e9ea9-103">Estos permiten características tooeasily, diagnosticar y recuperarse de las máquinas virtuales de los errores de arranque.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="e9ea9-104">Para máquinas de virtuales de Linux, puede ver fácilmente salida de hello de su registro de la consola de hello Portal:</span><span class="sxs-lookup"><span data-stu-id="e9ea9-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="e9ea9-106">Sin embargo, Windows y máquinas virtuales de Linux, Azure también permite toosee una captura de pantalla de hello VM desde el hipervisor de hello:</span><span class="sxs-lookup"><span data-stu-id="e9ea9-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Error](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="e9ea9-108">Ambas características son compatibles para las máquinas virtuales de Azure en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="e9ea9-109">Tenga en cuenta, capturas de pantalla y salida pueden tardar hasta too10 minutos tooappear en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="e9ea9-110">Errores comunes de arranque</span><span class="sxs-lookup"><span data-stu-id="e9ea9-110">Common boot errors</span></span>

- [<span data-ttu-id="e9ea9-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="e9ea9-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="e9ea9-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="e9ea9-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="e9ea9-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="e9ea9-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="e9ea9-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="e9ea9-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="e9ea9-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="e9ea9-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="e9ea9-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="e9ea9-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="e9ea9-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="e9ea9-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="e9ea9-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="e9ea9-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="e9ea9-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="e9ea9-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="e9ea9-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="e9ea9-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="e9ea9-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="e9ea9-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="e9ea9-122">No se encontró un sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e9ea9-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="e9ea9-123">Error de arranque o INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="e9ea9-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="e9ea9-124">Habilitación del diagnóstico en una nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e9ea9-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="e9ea9-125">Al crear una nueva máquina Virtual desde el Portal de vista previa de hello, seleccione hello **Azure Resource Manager** de lista desplegable de modelo de implementación de hello:</span><span class="sxs-lookup"><span data-stu-id="e9ea9-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="e9ea9-127">Configurar Hola cuenta de almacenamiento de hello en tooselect de supervisión opción que desee que tooplace estos archivos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Creación de una máquina virtual](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="e9ea9-129">Si va a implementar desde una plantilla de Azure Resource Manager, navegue tooyour recurso de máquina Virtual y anexar la sección de perfil de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="e9ea9-130">Recuerde que el encabezado de la versión de API de "2015-06-15" toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="e9ea9-131">perfil de diagnóstico de Hello permite cuenta de almacenamiento de hello tooselect donde desea tooput estos registros.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="e9ea9-132">toodeploy una muestra de la máquina Virtual con diagnósticos de arranque habilitada, consulte nuestro repositorio aquí.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="e9ea9-133">Actualización de una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="e9ea9-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="e9ea9-134">tooenable el diagnóstico de arranque a través de hello Portal, también puede actualizar una máquina Virtual existente a través de hello Portal.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="e9ea9-135">Diagnóstico de arranque de hello seleccione opción y guardar.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="e9ea9-136">Reinicie el efecto de hello VM tootake.</span><span class="sxs-lookup"><span data-stu-id="e9ea9-136">Restart hello VM tootake effect.</span></span>

![Actualización de una máquina virtual existente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

