---
title: aaaCreate una VM de Windows desde un disco duro virtual especializado en Azure | Documentos de Microsoft
description: "Crear una nueva máquina virtual de Windows si se adjunta un disco especializado administrado como disco del sistema operativo hello en el modelo de implementación del Administrador de recursos de Hola."
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
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="702ec-103">Creación de una máquina virtual Windows a partir de un disco especializado</span><span class="sxs-lookup"><span data-stu-id="702ec-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="702ec-104">Crear una nueva máquina virtual si se adjunta un disco especializado administrado como disco del sistema operativo hello mediante Powershell.</span><span class="sxs-lookup"><span data-stu-id="702ec-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="702ec-105">Un disco especializado es una copia del disco duro virtual (VHD) de una máquina virtual existente que mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="702ec-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="702ec-106">Cuando se usa un toocreate VHD especializada una nueva máquina virtual, Hola nueva máquina virtual conserva el nombre de equipo de Hola Hola VM original.</span><span class="sxs-lookup"><span data-stu-id="702ec-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="702ec-107">También se conserva otra información específica del equipo y, en algunos casos, esta información duplicada podría ocasionar problemas.</span><span class="sxs-lookup"><span data-stu-id="702ec-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="702ec-108">Tenga en cuenta en qué tipo de información específica del equipo se basan las aplicaciones al copiar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="702ec-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="702ec-109">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="702ec-109">You have two options:</span></span>
* [<span data-ttu-id="702ec-110">Carga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="702ec-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="702ec-111">Copia de una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="702ec-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="702ec-112">Este tema muestra cómo toouse administra los discos.</span><span class="sxs-lookup"><span data-stu-id="702ec-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="702ec-113">Si tiene una implementación heredada que requiere el uso de una cuenta de Storage, vea [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md) (Creación de una máquina virtual a partir de un VHD especializado en una cuenta de Storage).</span><span class="sxs-lookup"><span data-stu-id="702ec-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="702ec-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="702ec-114">Before you begin</span></span>
<span data-ttu-id="702ec-115">Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="702ec-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="702ec-116">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="702ec-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="702ec-117">Opción 1: Cargar un VHD especializado</span><span class="sxs-lookup"><span data-stu-id="702ec-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="702ec-118">Puede cargar Hola que VHD de una máquina virtual especializada creado con una herramienta de virtualización local, como Hyper-V o una máquina virtual exportado desde otra nube.</span><span class="sxs-lookup"><span data-stu-id="702ec-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="702ec-119">Preparar Hola VM</span><span class="sxs-lookup"><span data-stu-id="702ec-119">Prepare hello VM</span></span>
<span data-ttu-id="702ec-120">Si piensa toouse Hola VHD como-es toocreate una nueva máquina virtual, asegúrese de que se completa Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="702ec-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="702ec-121">[Preparar una tooAzure de tooupload de disco duro virtual de Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="702ec-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="702ec-122">**No** generalizar Hola VM con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="702ec-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="702ec-123">Quite todas las herramientas de virtualización de invitado y los agentes instalados en hello VM (por ejemplo, las herramientas de VMware).</span><span class="sxs-lookup"><span data-stu-id="702ec-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="702ec-124">Asegúrese de hello VM es toopull configurado su dirección IP y la configuración de DNS a través de DHCP.</span><span class="sxs-lookup"><span data-stu-id="702ec-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="702ec-125">Esto garantiza que el servidor hello Obtiene una dirección IP dentro de la red virtual de hello cuando se inicia.</span><span class="sxs-lookup"><span data-stu-id="702ec-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="702ec-126">Obtener la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="702ec-126">Get hello storage account</span></span>
<span data-ttu-id="702ec-127">Se necesita un almacenamiento cuenta en Azure toostore Hola carga VHD.</span><span class="sxs-lookup"><span data-stu-id="702ec-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="702ec-128">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="702ec-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="702ec-129">cuentas de almacenamiento disponibles de hello tooshow, escriba:</span><span class="sxs-lookup"><span data-stu-id="702ec-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="702ec-130">Si desea que toouse una cuenta de almacenamiento existente, continúe toohello [carga Hola VHD](#upload-the-vhd-to-your-storage-account) sección.</span><span class="sxs-lookup"><span data-stu-id="702ec-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="702ec-131">Si necesita toocreate una cuenta de almacenamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="702ec-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="702ec-132">Se necesita el nombre de Hola Hola del grupo de recursos donde se debe crear la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="702ec-133">toofind todos los grupos de recursos de Hola que se encuentran en su suscripción, tipo:</span><span class="sxs-lookup"><span data-stu-id="702ec-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="702ec-134">toocreate un grupo de recursos denominado *myResourceGroup* Hola *West US* región, escriba:</span><span class="sxs-lookup"><span data-stu-id="702ec-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="702ec-135">Crear una cuenta de almacenamiento denominada *mystorageaccount* en este grupo de recursos mediante el uso de hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="702ec-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="702ec-136">Cargar la cuenta de almacenamiento de hello VHD tooyour</span><span class="sxs-lookup"><span data-stu-id="702ec-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="702ec-137">Hola de uso [AzureRmVhd agregar](/powershell/module/azurerm.compute/add-azurermvhd) contenedor cmdlet tooupload Hola VHD tooa en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="702ec-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="702ec-138">En este ejemplo Hola a cargas de archivo *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa cuenta de almacenamiento denominada *mystorageaccount* en hello *myResourceGroup* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="702ec-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="702ec-139">archivo de Hola se almacena en el contenedor de hello denominado *mycontainer* y nombre de archivo nuevo de hello será *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="702ec-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="702ec-140">Si se realiza correctamente, obtendrá una respuesta que busca toothis similar:</span><span class="sxs-lookup"><span data-stu-id="702ec-140">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="702ec-141">Dependiendo de la conexión de red y el tamaño de hello del archivo VHD, este comando puede tardar un rato toocomplete</span><span class="sxs-lookup"><span data-stu-id="702ec-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="702ec-142">Crear un disco administrado desde Hola VHD</span><span class="sxs-lookup"><span data-stu-id="702ec-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="702ec-143">Crear un disco administrado desde Hola especializado de disco duro virtual en su cuenta de almacenamiento mediante [AzureRMDisk nuevo](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="702ec-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="702ec-144">Este ejemplo se utiliza **myOSDisk1** para el nombre del disco hello, coloca Hola disco en *StandardLRS* almacenamiento y usa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* como Hola URI para el origen de hello VHD.</span><span class="sxs-lookup"><span data-stu-id="702ec-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="702ec-145">Crear un nuevo grupo de recursos para hello nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="702ec-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="702ec-146">Crear nuevo disco de SO Hola de hello carga VHD.</span><span class="sxs-lookup"><span data-stu-id="702ec-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="702ec-147">Opción 2: Copiar una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="702ec-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="702ec-148">Puede crear una copia de una máquina virtual que utiliza discos administrados tomando una instantánea de máquina virtual de hello, a continuación, mediante ese toocreate instantánea un nuevo administrado disco y una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="702ec-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="702ec-149">Tomar una instantánea del disco del sistema operativo Hola</span><span class="sxs-lookup"><span data-stu-id="702ec-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="702ec-150">Puede realizar una instantánea de una máquina virtual completa (incluidos todos los discos) o solo de un disco.</span><span class="sxs-lookup"><span data-stu-id="702ec-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="702ec-151">Hello pasos siguientes muestran cómo Hola tootake una instantánea de solo Hola SO disco de la VM con [AzureRmSnapshot New](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="702ec-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="702ec-152">Configure algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="702ec-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="702ec-153">Obtenga el objeto de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="702ec-154">Obtener nombre de disco de SO Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="702ec-155">Crear configuración de instantáneas de Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="702ec-156">Tomar instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="702ec-157">Si tiene previsto toouse Hola instantánea toocreate una máquina virtual que necesita toobe alto rendimiento, use el parámetro hello `-AccountType Premium_LRS` con el comando hello AzureRmSnapshot de nuevo.</span><span class="sxs-lookup"><span data-stu-id="702ec-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="702ec-158">parámetro Hello crea instantáneas de Hola para que se almacena como un disco de Premium administrados.</span><span class="sxs-lookup"><span data-stu-id="702ec-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="702ec-159">Managed Disks Premium son más costosos que los Estándar.</span><span class="sxs-lookup"><span data-stu-id="702ec-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="702ec-160">Por tanto, asegúrese de que realmente necesita Premium antes de usar el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="702ec-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="702ec-161">Crear un nuevo disco de instantánea de Hola</span><span class="sxs-lookup"><span data-stu-id="702ec-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="702ec-162">Crear un disco administrado desde Hola instantánea mediante [AzureRMDisk nuevo](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="702ec-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="702ec-163">Este ejemplo se utiliza *myOSDisk* para el nombre del disco Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="702ec-164">Crear un nuevo grupo de recursos para hello nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="702ec-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="702ec-165">Establecer el nombre de disco de SO Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="702ec-166">Crear disco administrado Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="702ec-167">Crear nueva máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="702ec-167">Create hello new VM</span></span> 

<span data-ttu-id="702ec-168">Crear funciones de red y otro toobe de recursos de máquina virtual usa Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="702ec-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="702ec-169">Crear red virtual y subred de Hola</span><span class="sxs-lookup"><span data-stu-id="702ec-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="702ec-170">Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="702ec-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="702ec-171">Crear una subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-171">Create hello subNet.</span></span> <span data-ttu-id="702ec-172">Este ejemplo crea una subred denominada **mySubNet**, en el grupo de recursos de hello **myDestinationResourceGroup**, y conjuntos de Hola prefijo de dirección de subred demasiado**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="702ec-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="702ec-173">Crear red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-173">Create hello vNet.</span></span> <span data-ttu-id="702ec-174">Este ejemplo establece Hola toobe de nombre de red virtual **myVnetName**, Hola ubicación demasiado**oeste de Estados Unidos**, y Hola prefijo de dirección de red virtual de hello demasiado**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="702ec-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="702ec-175">Crear grupo de seguridad de red de hello y una regla de RDP</span><span class="sxs-lookup"><span data-stu-id="702ec-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="702ec-176">toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad que permite el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="702ec-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="702ec-177">Dado que Hola VHD para hello nueva máquina virtual creada a partir de una máquina virtual especializada existente, puede usar una cuenta de máquina virtual de origen de Hola para RDP.</span><span class="sxs-lookup"><span data-stu-id="702ec-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="702ec-178">Este ejemplo establece Hola nombre NSG demasiado**myNsg** y nombre de regla Hola RDP demasiado**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="702ec-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="702ec-179">Para obtener más información acerca de los puntos de conexión y las reglas NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="702ec-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="702ec-180">Creación de una dirección IP pública y una NIC</span><span class="sxs-lookup"><span data-stu-id="702ec-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="702ec-181">tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="702ec-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="702ec-182">Crear dirección IP pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-182">Create hello public IP.</span></span> <span data-ttu-id="702ec-183">En este ejemplo, nombre de dirección IP pública de Hola se establece demasiado**myIP**.</span><span class="sxs-lookup"><span data-stu-id="702ec-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="702ec-184">Crear NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="702ec-184">Create hello NIC.</span></span> <span data-ttu-id="702ec-185">En este ejemplo, nombre de la NIC de Hola se establece demasiado**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="702ec-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="702ec-186">Establecer nombre de máquina virtual de Hola y el tamaño</span><span class="sxs-lookup"><span data-stu-id="702ec-186">Set hello VM name and size</span></span>

<span data-ttu-id="702ec-187">Este ejemplo establece Hola nombre de máquina virtual demasiado*myVM* y Hola VM tamaño demasiado*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="702ec-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="702ec-188">Agregar Hola NIC</span><span class="sxs-lookup"><span data-stu-id="702ec-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="702ec-189">Agregar disco Hola SO</span><span class="sxs-lookup"><span data-stu-id="702ec-189">Add hello OS disk</span></span> 

<span data-ttu-id="702ec-190">Agregar using de hello SO disco toohello configuración [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="702ec-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="702ec-191">Este ejemplo establece el tamaño de hello del disco de Hola de demasiado*128 GB* y adjuntará Hola disco administrado como un *Windows* disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="702ec-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="702ec-192">Completar Hola VM</span><span class="sxs-lookup"><span data-stu-id="702ec-192">Complete hello VM</span></span> 

<span data-ttu-id="702ec-193">Crear Hola VM con [AzureRMVM New](/powershell/module/azurerm.compute/new-azurermvm)Hola configuraciones que se acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="702ec-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="702ec-194">Si este comando es correcto, verá un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="702ec-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="702ec-195">Compruebe que se creó la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="702ec-195">Verify that hello VM was created</span></span>
<span data-ttu-id="702ec-196">Debería ver Hola recién creado máquina virtual en hello [portal de Azure](https://portal.azure.com), en **examinar** > **máquinas virtuales**, o mediante el uso de hello después de PowerShell comandos:</span><span class="sxs-lookup"><span data-stu-id="702ec-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="702ec-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="702ec-197">Next steps</span></span>
<span data-ttu-id="702ec-198">toosign en tooyour nueva máquina virtual, examinar toohello VM en hello [portal](https://portal.azure.com), haga clic en **conectar**y el archivo de escritorio remoto RDP Hola abierto.</span><span class="sxs-lookup"><span data-stu-id="702ec-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="702ec-199">Usar credenciales de cuenta de hello de su toosign de máquina virtual original en la nueva máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="702ec-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="702ec-200">Para obtener más información, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="702ec-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

