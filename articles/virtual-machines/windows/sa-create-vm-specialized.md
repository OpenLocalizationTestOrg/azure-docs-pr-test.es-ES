---
title: "aaaCreate máquina virtual desde un disco especializado en Azure | Documentos de Microsoft"
description: "Crear una nueva máquina virtual si se adjunta un disco especializado no administrado, en el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="5a532-103">Crear una máquina virtual a partir de un VHD especializado en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5a532-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="5a532-104">Crear una nueva máquina virtual si se adjunta un disco especializado no administrado como disco del sistema operativo hello mediante Powershell.</span><span class="sxs-lookup"><span data-stu-id="5a532-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="5a532-105">Un disco especializado es una copia de disco duro virtual de una máquina virtual existente que mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="5a532-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="5a532-106">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="5a532-106">You have two options:</span></span>
* [<span data-ttu-id="5a532-107">Carga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="5a532-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="5a532-108">Copiar Hola VHD de una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="5a532-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="5a532-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="5a532-109">Before you begin</span></span>
<span data-ttu-id="5a532-110">Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a532-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5a532-111">Ejecutar Hola siguientes tooinstall de comando.</span><span class="sxs-lookup"><span data-stu-id="5a532-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="5a532-112">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5a532-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="5a532-113">Opción 1: Cargar un VHD especializado</span><span class="sxs-lookup"><span data-stu-id="5a532-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="5a532-114">Puede cargar Hola que VHD de una máquina virtual especializada creado con una herramienta de virtualización local, como Hyper-V o una máquina virtual exportado desde otra nube.</span><span class="sxs-lookup"><span data-stu-id="5a532-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="5a532-115">Preparar Hola VM</span><span class="sxs-lookup"><span data-stu-id="5a532-115">Prepare hello VM</span></span>
<span data-ttu-id="5a532-116">Puede cargar un VHD especializado que se haya creado con una máquina virtual local o un VHD exportado desde otra nube.</span><span class="sxs-lookup"><span data-stu-id="5a532-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="5a532-117">Un disco duro virtual especializado mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="5a532-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="5a532-118">Si piensa toouse Hola VHD como-es toocreate una nueva máquina virtual, asegúrese de que se completa Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="5a532-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="5a532-119">[Preparar una tooAzure de tooupload de disco duro virtual de Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a532-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5a532-120">**No** generalizar Hola VM con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="5a532-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="5a532-121">Quite todas las herramientas de virtualización de invitado y los agentes instalados en hello VM (es decir, herramientas de VMware).</span><span class="sxs-lookup"><span data-stu-id="5a532-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="5a532-122">Asegúrese de hello VM es toopull configurado su dirección IP y la configuración de DNS a través de DHCP.</span><span class="sxs-lookup"><span data-stu-id="5a532-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="5a532-123">Esto garantiza que el servidor hello Obtiene una dirección IP dentro de la red virtual de hello cuando se inicia.</span><span class="sxs-lookup"><span data-stu-id="5a532-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="5a532-124">Obtener la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="5a532-124">Get hello storage account</span></span>
<span data-ttu-id="5a532-125">Necesita una cuenta de almacenamiento en la imagen de máquina virtual de Azure toostore Hola cargado.</span><span class="sxs-lookup"><span data-stu-id="5a532-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="5a532-126">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="5a532-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="5a532-127">cuentas de almacenamiento disponibles de hello tooshow, escriba:</span><span class="sxs-lookup"><span data-stu-id="5a532-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="5a532-128">Si desea que toouse una cuenta de almacenamiento existente, continúe toohello [imagen de máquina virtual de carga hello](#upload-the-vm-vhd-to-your-storage-account) sección.</span><span class="sxs-lookup"><span data-stu-id="5a532-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="5a532-129">Si necesita toocreate una cuenta de almacenamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5a532-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="5a532-130">Se necesita el nombre de Hola Hola del grupo de recursos donde se debe crear la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="5a532-131">toofind todos los grupos de recursos de Hola que se encuentran en su suscripción, tipo:</span><span class="sxs-lookup"><span data-stu-id="5a532-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="5a532-132">toocreate un grupo de recursos denominado **myResourceGroup** Hola **West US** región, escriba:</span><span class="sxs-lookup"><span data-stu-id="5a532-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="5a532-133">Crear una cuenta de almacenamiento denominada **mystorageaccount** en este grupo de recursos mediante el uso de hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5a532-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="5a532-134">Cargar la cuenta de almacenamiento de hello VHD tooyour</span><span class="sxs-lookup"><span data-stu-id="5a532-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="5a532-135">Hola de uso [AzureRmVhd agregar](/powershell/module/azurerm.compute/add-azurermvhd) contenedor cmdlet tooupload Hola imagen tooa en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5a532-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="5a532-136">En este ejemplo Hola a cargas de archivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa cuenta de almacenamiento denominada **mystorageaccount** en hello **myResourceGroup** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5a532-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="5a532-137">archivo Hello se colocarán en el contenedor de hello denominado **mycontainer** y nombre de archivo nuevo de hello será **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="5a532-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="5a532-138">Si se realiza correctamente, obtendrá una respuesta que busca toothis similar:</span><span class="sxs-lookup"><span data-stu-id="5a532-138">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="5a532-139">Dependiendo de la conexión de red y el tamaño de hello del archivo VHD, este comando puede tardar un rato toocomplete.</span><span class="sxs-lookup"><span data-stu-id="5a532-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="5a532-140">Opción 2: Copiar Hola VHD de una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="5a532-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="5a532-141">Puede copiar un toouse de cuenta de almacenamiento de disco duro virtual tooanother al crear una máquina virtual nueva y duplicada.</span><span class="sxs-lookup"><span data-stu-id="5a532-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="5a532-142">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="5a532-142">Before you begin</span></span>
<span data-ttu-id="5a532-143">Asegúrese de todo esto:</span><span class="sxs-lookup"><span data-stu-id="5a532-143">Make sure that you:</span></span>

* <span data-ttu-id="5a532-144">Tener información sobre hello **cuentas de almacenamiento de origen y destino**.</span><span class="sxs-lookup"><span data-stu-id="5a532-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="5a532-145">Para hello una VM de origen, deberá toohave Hola cuenta nombres almacenamiento y contenedor.</span><span class="sxs-lookup"><span data-stu-id="5a532-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="5a532-146">Normalmente, será el nombre del contenedor de hello **discos duros virtuales**.</span><span class="sxs-lookup"><span data-stu-id="5a532-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="5a532-147">También debe toohave una cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="5a532-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="5a532-148">Si aún no tiene uno, puede crear uno mediante cualquier portal hello (**más servicios** > cuentas de almacenamiento > Agregar) o mediante hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5a532-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="5a532-149">Ha descargado e instalado hello [herramienta AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5a532-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="5a532-150">Cancela la asignación de hello VM</span><span class="sxs-lookup"><span data-stu-id="5a532-150">Deallocate hello VM</span></span>
<span data-ttu-id="5a532-151">Cancela la asignación de hello VM, lo que libera hello toobe de disco duro virtual copiado.</span><span class="sxs-lookup"><span data-stu-id="5a532-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="5a532-152">**Portal**: haga clic en **Máquinas virtuales** > **myVM** &gt; Detener</span><span class="sxs-lookup"><span data-stu-id="5a532-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="5a532-153">**PowerShell**: Use [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (desasignarlos) Hola máquina virtual denominada **myVM** en grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5a532-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="5a532-154">Hola **estado** para hello VM en hello Azure portal cambia de **detenido** demasiado**detenido (desasignado)**.</span><span class="sxs-lookup"><span data-stu-id="5a532-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="5a532-155">Obtener direcciones URL de cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="5a532-155">Get hello storage account URLs</span></span>
<span data-ttu-id="5a532-156">Necesita hello las direcciones URL de cuentas de almacenamiento de origen y destino Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="5a532-157">Hello direcciones URL aspecto: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="5a532-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="5a532-158">Si ya sabe el nombre de cuenta y el contenedor de almacenamiento de hello, simplemente puede reemplazar la dirección URL de información de hello entre Hola corchetes toocreate.</span><span class="sxs-lookup"><span data-stu-id="5a532-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="5a532-159">Puede usar Hola portal de Azure o Azure Powershell tooget Hola URL:</span><span class="sxs-lookup"><span data-stu-id="5a532-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="5a532-160">**Portal de**: haga clic en hello  **>**  para **más servicios** > **cuentas de almacenamiento**  >   *cuenta de almacenamiento* > **Blobs** y el archivo de disco duro virtual de origen es probablemente Hola **discos duros virtuales** contenedor.</span><span class="sxs-lookup"><span data-stu-id="5a532-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="5a532-161">Haga clic en **propiedades** de contenedor de Hola y con la etiqueta de texto de copia hello **URL**.</span><span class="sxs-lookup"><span data-stu-id="5a532-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="5a532-162">Necesitará hello las direcciones URL de los contenedores de origen y destino Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="5a532-163">**PowerShell**: Use [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget información de hello para la máquina virtual denominada **myVM** en grupo de recursos de hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5a532-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="5a532-164">En los resultados de hello, buscar en hello **perfil de almacenamiento** sección para hello **Uri de Vhd**.</span><span class="sxs-lookup"><span data-stu-id="5a532-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="5a532-165">Hola primera parte del Uri de hello es contenedor de toohello de dirección URL de Hola y Hola última parte es Hola nombre de disco duro virtual del sistema operativo para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a532-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="5a532-166">Obtener claves de acceso de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="5a532-166">Get hello storage access keys</span></span>
<span data-ttu-id="5a532-167">Buscar claves de acceso de Hola de hello las cuentas de almacenamiento de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="5a532-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="5a532-168">Para más información acerca de las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5a532-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="5a532-169">**Portal**: haga clic en **Más servicios** > **Cuentas de almacenamiento** > *cuenta de almacenamiento* > **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="5a532-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="5a532-170">Clave de copia Hola etiquetada como **key1**.</span><span class="sxs-lookup"><span data-stu-id="5a532-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="5a532-171">**PowerShell**: Use [Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget Hola almacenamiento clave Hola cuenta de almacenamiento **mystorageaccount** en grupo de recursos de hello  **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5a532-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="5a532-172">Clave de hello copia con la etiqueta **key1**.</span><span class="sxs-lookup"><span data-stu-id="5a532-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="5a532-173">Copiar Hola VHD</span><span class="sxs-lookup"><span data-stu-id="5a532-173">Copy hello VHD</span></span>
<span data-ttu-id="5a532-174">Puede copiar archivos entre cuentas de almacenamiento con AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5a532-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="5a532-175">Para el contenedor de destino de hello, si no existe el contenedor especificado de hello, se creará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5a532-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="5a532-176">toouse AzCopy, abra un símbolo del sistema en el equipo local y desplazarse por las carpetas de toohello donde está instalado AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5a532-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="5a532-177">Será similar demasiado*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="5a532-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="5a532-178">toocopy todos Hola archivos dentro de un contenedor, utiliza hello **/S** cambiar.</span><span class="sxs-lookup"><span data-stu-id="5a532-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="5a532-179">Esto puede ser usado toocopy Hola VHD de sistema operativo y todos los discos de datos de hello si están en Hola mismo contenedor.</span><span class="sxs-lookup"><span data-stu-id="5a532-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="5a532-180">Este ejemplo se muestra cómo toocopy todos los de hello archivos de contenedor de hello **mysourcecontainer** en la cuenta de almacenamiento **mysourcestorageaccount** toohello contenedor **mydestinationcontainer**  en hello **mydestinationstorageaccount** cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5a532-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="5a532-181">Reemplazar nombres de Hola de cuentas de almacenamiento de Hola y de contenedores por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="5a532-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="5a532-182">Reemplace `<sourceStorageAccountKey1>` y `<destinationStorageAccountKey1>` por sus propias claves.</span><span class="sxs-lookup"><span data-stu-id="5a532-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="5a532-183">Si solo desea toocopy un VHD específico en un contenedor con varios archivos, también puede especificar el nombre de archivo de hello mediante el modificador de /Pattern Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="5a532-184">En este ejemplo, solo Hola archivo denominado **myFileName.vhd** se va a copiar.</span><span class="sxs-lookup"><span data-stu-id="5a532-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="5a532-185">Cuando haya finalizado, obtendrá un mensaje parecido a este:</span><span class="sxs-lookup"><span data-stu-id="5a532-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="5a532-186">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5a532-186">Troubleshooting</span></span>
* <span data-ttu-id="5a532-187">Cuando usas AZCopy, si ve el error de Hola "Servidor no pudo solicitud de hello tooauthenticate", asegúrese de que valor Hola de encabezado de autorización de hello está formado correctamente incluye firma de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="5a532-188">Si usas 2 de clave o la clave de almacenamiento secundaria hello, pruebe a usar la clave de almacenamiento principal o el 1 de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="5a532-189">Crear nueva máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="5a532-189">Create hello new VM</span></span> 

<span data-ttu-id="5a532-190">Necesita toocreate redes y otro toobe de recursos de máquina virtual usa Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a532-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="5a532-191">Crear red virtual y subred de Hola</span><span class="sxs-lookup"><span data-stu-id="5a532-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="5a532-192">Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a532-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="5a532-193">Crear una subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-193">Create hello subNet.</span></span> <span data-ttu-id="5a532-194">Este ejemplo crea una subred denominada **mySubNet**, en el grupo de recursos de hello **myResourceGroup**, y conjuntos de Hola prefijo de dirección de subred demasiado**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="5a532-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="5a532-195">Crear red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-195">Create hello vNet.</span></span> <span data-ttu-id="5a532-196">Este ejemplo establece Hola toobe de nombre de red virtual **myVnetName**, Hola ubicación demasiado**oeste de Estados Unidos**, y Hola prefijo de dirección de red virtual de hello demasiado**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="5a532-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="5a532-197">Creación de una dirección IP pública y una NIC</span><span class="sxs-lookup"><span data-stu-id="5a532-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="5a532-198">tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="5a532-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="5a532-199">Crear dirección IP pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-199">Create hello public IP.</span></span> <span data-ttu-id="5a532-200">En este ejemplo, nombre de dirección IP pública de Hola se establece demasiado**myIP**.</span><span class="sxs-lookup"><span data-stu-id="5a532-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="5a532-201">Crear NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-201">Create hello NIC.</span></span> <span data-ttu-id="5a532-202">En este ejemplo, nombre de la NIC de Hola se establece demasiado**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="5a532-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="5a532-203">Crear grupo de seguridad de red de hello y una regla de RDP</span><span class="sxs-lookup"><span data-stu-id="5a532-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="5a532-204">toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad que concede acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="5a532-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="5a532-205">Porque especializados hello VHD para hello que nueva máquina virtual creada a partir de una existente máquina virtual, una vez creado Hola VM puede usar una cuenta existente de la máquina virtual de hello origen que tenía permiso toolog sobre el uso de RDP.</span><span class="sxs-lookup"><span data-stu-id="5a532-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="5a532-206">Este ejemplo establece Hola nombre NSG demasiado**myNsg** y nombre de regla Hola RDP demasiado**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="5a532-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="5a532-207">Para obtener más información acerca de los puntos de conexión y las reglas NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a532-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="5a532-208">Establecer nombre de máquina virtual de Hola y el tamaño</span><span class="sxs-lookup"><span data-stu-id="5a532-208">Set hello VM name and size</span></span>

<span data-ttu-id="5a532-209">En este ejemplo Hola de conjuntos de nombre de máquina virtual demasiado hello VM y "myVM" tamaño demasiado "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="5a532-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="5a532-210">Agregar Hola NIC</span><span class="sxs-lookup"><span data-stu-id="5a532-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="5a532-211">Configurar el disco de SO Hola</span><span class="sxs-lookup"><span data-stu-id="5a532-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="5a532-212">URI del conjunto hello para hello VHD que cargado o copiado.</span><span class="sxs-lookup"><span data-stu-id="5a532-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="5a532-213">En este ejemplo, Hola archivo de disco duro virtual denominado **myOsDisk.vhd** se mantiene en una cuenta de almacenamiento denominada **myStorageAccount** en un contenedor denominado **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="5a532-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="5a532-214">Agregar disco de SO Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-214">Add hello OS disk.</span></span> <span data-ttu-id="5a532-215">En este ejemplo, cuando se crea el disco del sistema operativo de hello, Hola término "osDisk" es appened toohello VM nombre toocreate Hola SO nombre del disco.</span><span class="sxs-lookup"><span data-stu-id="5a532-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="5a532-216">En este ejemplo también se especifica que este disco duro virtual basado en Windows debe ser adjunto toohello máquina virtual como disco de SO Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="5a532-217">Opcional: Si tiene discos de datos que toobe necesidad adjunta toohello VM, agregue más discos de datos de hello mediante direcciones URL de Hola de VHD de datos y Hola número de unidad lógica (Lun) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="5a532-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="5a532-218">Cuando se usa una cuenta de almacenamiento, datos de Hola y direcciones URL de disco del sistema operativo este aspecto: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="5a532-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="5a532-219">Puede encontrar en el portal de hello examinando el contenedor de almacenamiento de destino de toohello, haga clic en el sistema operativo de Hola o datos del disco duro virtual que se ha copiado, y, a continuación, copiar contenido de hello de la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a532-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="5a532-220">Completar Hola VM</span><span class="sxs-lookup"><span data-stu-id="5a532-220">Complete hello VM</span></span> 

<span data-ttu-id="5a532-221">Crear Hola VM usando configuraciones de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="5a532-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="5a532-222">Si este comando es correcto, verá un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="5a532-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="5a532-223">Compruebe que se creó la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="5a532-223">Verify that hello VM was created</span></span>
<span data-ttu-id="5a532-224">Debería ver Hola recién creado máquina virtual en hello [portal de Azure](https://portal.azure.com), en **examinar** > **máquinas virtuales**, o mediante el uso de hello después de PowerShell comandos:</span><span class="sxs-lookup"><span data-stu-id="5a532-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="5a532-225">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a532-225">Next steps</span></span>
<span data-ttu-id="5a532-226">toosign en tooyour nueva máquina virtual, examinar toohello VM en hello [portal](https://portal.azure.com), haga clic en **conectar**y el archivo de escritorio remoto RDP Hola abierto.</span><span class="sxs-lookup"><span data-stu-id="5a532-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="5a532-227">Usar credenciales de cuenta de hello de su toosign de máquina virtual original en la nueva máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="5a532-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="5a532-228">Para obtener más información, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="5a532-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

