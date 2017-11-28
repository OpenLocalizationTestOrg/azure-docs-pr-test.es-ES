---
title: aaaCreate una imagen administrada en Azure | Documentos de Microsoft
description: "Cree una imagen administrada de un VHD o de una VM generalizada en Azure. Las imágenes puede ser utilizado toocreate varias máquinas virtuales que usan discos administrados."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="33097-104">Captura de una imagen administrada de una máquina virtual generalizada en Azure</span><span class="sxs-lookup"><span data-stu-id="33097-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="33097-105">Se puede crear un recurso de imagen administrado a partir de una máquina virtual generalizada que se almacena como un disco administrado o como un disco no administrado en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="33097-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="33097-106">a continuación, Hola imagen puede ser toocreate usa varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="33097-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="33097-107">Generalizar Hola VM de Windows con Sysprep</span><span class="sxs-lookup"><span data-stu-id="33097-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="33097-108">Sysprep quita toda la información de cuenta personal, entre otras cosas y prepara Hola máquina toobe utilizado como una imagen.</span><span class="sxs-lookup"><span data-stu-id="33097-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="33097-109">Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="33097-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="33097-110">Asegúrese de que los roles de servidor hello ejecutando en el equipo de hello son compatibles con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="33097-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="33097-111">Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="33097-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33097-112">Si está ejecutando Sysprep antes de cargar su tooAzure de disco duro virtual para hello primera vez, asegúrese de que tiene [preparado la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep.</span><span class="sxs-lookup"><span data-stu-id="33097-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="33097-113">Inicie sesión en toohello máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="33097-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="33097-114">Abra la ventana de símbolo del sistema de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="33097-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="33097-115">Cambie el directorio de hello demasiado**%windir%\system32\sysprep**y, a continuación, ejecute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="33097-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="33097-116">Hola **herramienta de preparación del sistema** cuadro de diálogo, seleccione **sistema Out-of-Box experiencia inmediata (OOBE)**y asegúrese de que ese hello **generalizar** casilla está activada.</span><span class="sxs-lookup"><span data-stu-id="33097-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="33097-117">En **Opciones de apagado**, seleccione **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="33097-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="33097-118">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="33097-118">Click **OK**.</span></span>
   
    ![Iniciar Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="33097-120">Cuando Sysprep finalice, se apaga máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="33097-121">No se reinician Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33097-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="33097-122">Crear una imagen administrada en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="33097-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="33097-123">Abra hello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="33097-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="33097-124">Haga clic en Hola signo toocreate un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="33097-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="33097-125">En la búsqueda del filtro de hello, escriba **imagen**.</span><span class="sxs-lookup"><span data-stu-id="33097-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="33097-126">Seleccione **imagen** de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="33097-127">Hola **imagen** hoja, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="33097-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="33097-128">En **nombre**, escriba un nombre para la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="33097-129">Si tiene más de una suscripción, seleccione Hola uno correcto de hello **suscripción** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="33097-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="33097-130">En **grupo de recursos** seleccione **crear nuevo** y escriba un nombre o seleccione **de existentes** y seleccione un toouse de grupo de recursos de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="33097-131">En **ubicación**, Elegir ubicación de Hola de su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="33097-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="33097-132">En **tipo de SO** Seleccionar tipo de Hola de sistema operativo Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="33097-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="33097-133">En **blob de almacenamiento**, haga clic en **examinar** toolook para hello VHD en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="33097-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="33097-134">En **Tipo de cuenta**, elija Standard_LRS o Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="33097-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="33097-135">Standard utiliza unidades de disco duro y Premium utiliza unidades de estado sólido.</span><span class="sxs-lookup"><span data-stu-id="33097-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="33097-136">Ambas opciones emplean almacenamiento con redundancia local.</span><span class="sxs-lookup"><span data-stu-id="33097-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="33097-137">En **almacenamiento en caché de disco** seleccione Hola opción de caché de disco adecuado.</span><span class="sxs-lookup"><span data-stu-id="33097-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="33097-138">Opciones de Hello son **ninguno**, **de sólo lectura** y **lectura/escritura**.</span><span class="sxs-lookup"><span data-stu-id="33097-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="33097-139">Opcional: También puede agregar una imagen de toohello de disco de datos existente, haga clic en **+ Agregar disco de datos**.</span><span class="sxs-lookup"><span data-stu-id="33097-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="33097-140">Cuando haya terminado de realizar todas las selecciones, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="33097-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="33097-141">Después de crea la imagen de hello, verá como un **imagen** recurso en la lista de Hola de recursos de grupo de recursos de Hola que eligió.</span><span class="sxs-lookup"><span data-stu-id="33097-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="33097-142">Creación de una imagen administrada de una VM mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="33097-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="33097-143">Crear una imagen directamente a partir de hello que VM garantiza esa imagen Hola incluye todos los discos de hello asociados Hola máquina virtual, incluyendo hello disco del sistema operativo y los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="33097-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="33097-144">Antes de comenzar, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33097-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="33097-145">Ejecutar Hola siguientes tooinstall de comando.</span><span class="sxs-lookup"><span data-stu-id="33097-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="33097-146">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="33097-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="33097-147">Cree algunas variables.</span><span class="sxs-lookup"><span data-stu-id="33097-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="33097-148">Asegúrese de hello seguro que se ha desasignado la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33097-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="33097-149">Establecer el estado de saludo de la máquina virtual de hello demasiado**generalizado**.</span><span class="sxs-lookup"><span data-stu-id="33097-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="33097-150">Obtenga la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="33097-151">Crear configuración de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="33097-152">Crear imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="33097-153">Creación de una imagen administrada de un VHD en PowerShell</span><span class="sxs-lookup"><span data-stu-id="33097-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="33097-154">Cree una imagen administrada con el VHD del SO generalizado.</span><span class="sxs-lookup"><span data-stu-id="33097-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="33097-155">En primer lugar, establezca los parámetros comunes de hello:</span><span class="sxs-lookup"><span data-stu-id="33097-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="33097-156">Hola Step\deallocate máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33097-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="33097-157">Marcar Hola VM tal y como se ha generalizado.</span><span class="sxs-lookup"><span data-stu-id="33097-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="33097-158">Crear imagen de hello con el disco duro virtual generalizado de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="33097-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="33097-159">Creación de una imagen administrada a partir de una instantánea mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="33097-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="33097-160">También puede crear una imagen administrada de una instantánea de hello VHD de una máquina virtual generalizada.</span><span class="sxs-lookup"><span data-stu-id="33097-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="33097-161">Cree algunas variables.</span><span class="sxs-lookup"><span data-stu-id="33097-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="33097-162">Obtener instantáneas de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="33097-163">Crear configuración de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="33097-164">Crear imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="33097-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="33097-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33097-165">Next steps</span></span>
- <span data-ttu-id="33097-166">Ahora podrá [crear una máquina virtual de imagen administrada Hola generalizado](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="33097-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

