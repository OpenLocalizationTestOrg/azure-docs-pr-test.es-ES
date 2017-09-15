<span data-ttu-id="7ee3c-101">Ahora se ofrece en Azure compatibilidad con dos características de depuración, Salida de la consola y Captura de pantalla, para el modelo de implementación de Resource Manager en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="7ee3c-102">Cuando lleva su propia imagen a Azure o incluso cuando arranca una de las imágenes de la plataforma, hay muchas razones por las que una máquina virtual puede entrar en un estado que no permita el arranque.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-102">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="7ee3c-103">Estas características le permiten diagnosticar y recuperar fácilmente las máquinas virtuales de los errores de arranque.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-103">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="7ee3c-104">Para las máquinas virtuales Linux, puede ver fácilmente la salida de su registro de consola desde el portal:</span><span class="sxs-lookup"><span data-stu-id="7ee3c-104">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="7ee3c-106">Sin embargo, para las máquinas virtuales Windows y Linux, Azure también le permite ver una captura de pantalla de la máquina virtual desde el hipervisor:</span><span class="sxs-lookup"><span data-stu-id="7ee3c-106">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Error](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="7ee3c-108">Ambas características son compatibles para las máquinas virtuales de Azure en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="7ee3c-109">Tenga en cuenta que las capturas de pantalla y la salida pueden tardar hasta 10 minutos en aparecer en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-109">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="7ee3c-110">Errores comunes de arranque</span><span class="sxs-lookup"><span data-stu-id="7ee3c-110">Common boot errors</span></span>

- [<span data-ttu-id="7ee3c-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="7ee3c-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="7ee3c-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="7ee3c-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="7ee3c-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="7ee3c-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="7ee3c-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="7ee3c-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="7ee3c-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="7ee3c-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="7ee3c-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="7ee3c-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="7ee3c-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="7ee3c-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="7ee3c-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="7ee3c-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="7ee3c-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="7ee3c-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="7ee3c-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="7ee3c-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="7ee3c-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="7ee3c-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="7ee3c-122">No se encontró un sistema operativo</span><span class="sxs-lookup"><span data-stu-id="7ee3c-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="7ee3c-123">Error de arranque o INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="7ee3c-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="7ee3c-124">Habilitación del diagnóstico en una nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7ee3c-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="7ee3c-125">Cuando cree una máquina virtual desde la versión preliminar del portal, seleccione **Azure Resource Manager** en la lista desplegable de modelo de implementación:</span><span class="sxs-lookup"><span data-stu-id="7ee3c-125">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="7ee3c-127">Configure la opción Supervisión para seleccionar la cuenta de almacenamiento donde desee colocar estos archivos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-127">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![Creación de una máquina virtual](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="7ee3c-129">Si va a realizar la implementación con una plantilla de Azure Resource Manager, vaya al recurso de máquina virtual y anexe la sección de perfil de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-129">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="7ee3c-130">Recuerde usar el encabezado de versión de API "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="7ee3c-130">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="7ee3c-131">El perfil de diagnóstico le permite seleccionar la cuenta de almacenamiento donde desea colocar estos registros.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-131">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

<span data-ttu-id="7ee3c-132">Para implementar una máquina virtual de ejemplo con el diagnóstico de arranque habilitado, visite nuestro repositorio aquí.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-132">To deploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="7ee3c-133">Actualización de una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="7ee3c-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="7ee3c-134">Para habilitar el diagnóstico de arranque a través del portal, también puede actualizar una máquina virtual existente en el portal.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-134">To enable boot diagnostics through the Portal, you can also update an existing Virtual Machine through the Portal.</span></span> <span data-ttu-id="7ee3c-135">Seleccione la opción Diagnósticos de arranque y guarde.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-135">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="7ee3c-136">Reinicie la máquina virtual para que surta efecto.</span><span class="sxs-lookup"><span data-stu-id="7ee3c-136">Restart the VM to take effect.</span></span>

![Actualización de una máquina virtual existente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

