---
title: "Creación de una máquina virtual Windows desde un VHD especializado en Azure | Microsoft Docs"
description: "Cree una nueva máquina virtual Windows asociando un disco administrado especializado como el disco del SO en el modelo de implementación de Resource Manager."
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
ms.openlocfilehash: fa952286a9ceca8b3b2c7efe2cc4867a2728c477
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="0f903-103">Creación de una máquina virtual Windows a partir de un disco especializado</span><span class="sxs-lookup"><span data-stu-id="0f903-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="0f903-104">Cree una máquina virtual mediante la asociación de un disco administrado especializado como el disco del SO mediante Powershell.</span><span class="sxs-lookup"><span data-stu-id="0f903-104">Create a new VM by attaching a specialized managed disk as the OS disk using Powershell.</span></span> <span data-ttu-id="0f903-105">Un disco especializado es una copia del disco duro virtual (VHD) de una máquina virtual existente que mantiene las cuentas de usuario, las aplicaciones y otros datos de estado de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="0f903-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains the user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="0f903-106">Cuando se usa un VHD especializado para crear una máquina virtual, la nueva máquina virtual conserva el nombre de equipo de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="0f903-106">When you use a specialized VHD to create a new VM, the new VM retains the computer name of the original VM.</span></span> <span data-ttu-id="0f903-107">También se conserva otra información específica del equipo y, en algunos casos, esta información duplicada podría ocasionar problemas.</span><span class="sxs-lookup"><span data-stu-id="0f903-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="0f903-108">Tenga en cuenta en qué tipo de información específica del equipo se basan las aplicaciones al copiar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f903-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="0f903-109">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="0f903-109">You have two options:</span></span>
* [<span data-ttu-id="0f903-110">Carga de un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="0f903-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="0f903-111">Copia de una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="0f903-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="0f903-112">En este tema se muestra cómo usar Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="0f903-112">This topic shows you how to use managed disks.</span></span> <span data-ttu-id="0f903-113">Si tiene una implementación heredada que requiere el uso de una cuenta de Storage, vea [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md) (Creación de una máquina virtual a partir de un VHD especializado en una cuenta de Storage).</span><span class="sxs-lookup"><span data-stu-id="0f903-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0f903-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0f903-114">Before you begin</span></span>
<span data-ttu-id="0f903-115">Si usa PowerShell, asegúrese de que tiene la versión más reciente del módulo de PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="0f903-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="0f903-116">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0f903-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="0f903-117">Opción 1: Cargar un VHD especializado</span><span class="sxs-lookup"><span data-stu-id="0f903-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="0f903-118">Puede cargar el VHD de una máquina virtual especializada creada con una herramienta de virtualización local, como Hyper-V, o de una máquina virtual exportada desde otra nube.</span><span class="sxs-lookup"><span data-stu-id="0f903-118">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="0f903-119">Preparación de la VM</span><span class="sxs-lookup"><span data-stu-id="0f903-119">Prepare the VM</span></span>
<span data-ttu-id="0f903-120">Si tiene previsto usar el VHD como está para crear una nueva VM, asegúrese de completar los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="0f903-120">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="0f903-121">[Preparar de un VHD de Windows para cargar en Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f903-121">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0f903-122">**No** generalice la VM mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="0f903-122">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="0f903-123">Quite todas las herramientas de virtualización de invitado y los agentes instalados en la VM (es decir, herramientas de VMware).</span><span class="sxs-lookup"><span data-stu-id="0f903-123">Remove any guest virtualization tools and agents that are installed on the VM (like VMware tools).</span></span>
  * <span data-ttu-id="0f903-124">Asegúrese de que la VM se configura para extraer su dirección IP y la configuración de DNS a través de DHCP.</span><span class="sxs-lookup"><span data-stu-id="0f903-124">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="0f903-125">Esto garantiza que el servidor obtiene una dirección IP dentro de la red virtual cuando se inicia.</span><span class="sxs-lookup"><span data-stu-id="0f903-125">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="0f903-126">Obtención de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="0f903-126">Get the storage account</span></span>
<span data-ttu-id="0f903-127">Necesita una cuenta de almacenamiento de Azure para almacenar el VHD cargado.</span><span class="sxs-lookup"><span data-stu-id="0f903-127">You need a storage account in Azure to store the uploaded VHD.</span></span> <span data-ttu-id="0f903-128">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="0f903-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="0f903-129">Para mostrar las cuentas de almacenamiento disponibles, escriba:</span><span class="sxs-lookup"><span data-stu-id="0f903-129">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="0f903-130">Si desea utilizar una cuenta de Storage existente, continúe con la sección [Carga del VHD](#upload-the-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0f903-130">If you want to use an existing storage account, proceed to the [Upload the VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="0f903-131">Si necesita crear una nueva cuenta de almacenamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0f903-131">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="0f903-132">Necesita el nombre del grupo de recursos donde se debe crear la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0f903-132">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="0f903-133">Para averiguar todos los grupos de recursos que están en la suscripción, escriba:</span><span class="sxs-lookup"><span data-stu-id="0f903-133">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="0f903-134">Para crear un grupo de recursos denominado *myResourceGroup* en la región *Oeste de EE. UU.*, escriba:</span><span class="sxs-lookup"><span data-stu-id="0f903-134">To create a resource group named *myResourceGroup* in the *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="0f903-135">Cree una cuenta de almacenamiento denominada *mystorageaccount* en este grupo de recursos con el cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount):</span><span class="sxs-lookup"><span data-stu-id="0f903-135">Create a storage account named *mystorageaccount* in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="0f903-136">Carga del VHD en la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="0f903-136">Upload the VHD to your storage account</span></span> 
<span data-ttu-id="0f903-137">Use el cmdlet [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) para cargar el VHD en un contenedor de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0f903-137">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="0f903-138">En este ejemplo se carga el archivo *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` para una cuenta de almacenamiento denominada *mystorageaccount* en el grupo de recursos *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0f903-138">This example uploads the file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="0f903-139">El archivo se almacena en el contenedor llamado *mycontainer* y el nuevo nombre de archivo será *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="0f903-139">The file is stored in the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="0f903-140">Si se realiza correctamente, obtendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0f903-140">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="0f903-141">Dependiendo de la conexión de red y del tamaño del archivo VHD, este comando tardará algún tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="0f903-141">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

### <a name="create-a-managed-disk-from-the-vhd"></a><span data-ttu-id="0f903-142">Creación de un disco administrado a partir del VHD</span><span class="sxs-lookup"><span data-stu-id="0f903-142">Create a managed disk from the VHD</span></span>

<span data-ttu-id="0f903-143">Cree un disco administrado a partir del VHD especializado en la cuenta de Storage mediante [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="0f903-143">Create a managed disk from the specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="0f903-144">En este ejemplo se usa **myOSDisk1** como nombre del disco, se coloca el disco en el almacenamiento *StandardLRS* y se usa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* como el URI para el VHD de origen.</span><span class="sxs-lookup"><span data-stu-id="0f903-144">This example uses **myOSDisk1** for the disk name, puts the disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as the URI for the source VHD.</span></span>

<span data-ttu-id="0f903-145">Cree un grupo de recursos para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f903-145">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="0f903-146">Cree el disco del SO a partir del VHD cargado.</span><span class="sxs-lookup"><span data-stu-id="0f903-146">Create the new OS disk from the uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="0f903-147">Opción 2: Copiar una máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="0f903-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="0f903-148">Puede crear una copia de una máquina virtual que usa Managed Disks mediante la realización de una instantánea de la máquina virtual, para usarla después para crear un disco administrado y una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f903-148">You can create a copy of a VM that uses managed disks by taking a snapshot of the VM, then using that snapshot to create a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-the-os-disk"></a><span data-ttu-id="0f903-149">Realización de la instantánea del disco del SO</span><span class="sxs-lookup"><span data-stu-id="0f903-149">Take a snapshot of the OS disk</span></span>

<span data-ttu-id="0f903-150">Puede realizar una instantánea de una máquina virtual completa (incluidos todos los discos) o solo de un disco.</span><span class="sxs-lookup"><span data-stu-id="0f903-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="0f903-151">En los pasos siguientes se describe cómo realizar una instantánea solo del disco del SO de la máquina virtual mediante el cmdlet [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot).</span><span class="sxs-lookup"><span data-stu-id="0f903-151">The following steps show you how to take a snapshot of just the OS disk of your VM using the [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="0f903-152">Configure algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="0f903-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="0f903-153">Obtenga el objeto de VM.</span><span class="sxs-lookup"><span data-stu-id="0f903-153">Get the VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="0f903-154">Obtenga el nombre del disco del SO.</span><span class="sxs-lookup"><span data-stu-id="0f903-154">Get the OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="0f903-155">Cree la configuración de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="0f903-155">Create the snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="0f903-156">Tome la instantánea.</span><span class="sxs-lookup"><span data-stu-id="0f903-156">Take the snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="0f903-157">Si tiene previsto utilizar la instantánea para crear una máquina virtual que precisa de un alto rendimiento, use el parámetro `-AccountType Premium_LRS` con el comando New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="0f903-157">If you plan to use the snapshot to create a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="0f903-158">El parámetro crea la instantánea para que se almacene como disco administrado Premium.</span><span class="sxs-lookup"><span data-stu-id="0f903-158">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="0f903-159">Managed Disks Premium son más costosos que los Estándar.</span><span class="sxs-lookup"><span data-stu-id="0f903-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="0f903-160">Por lo tanto, asegúrese de que realmente necesita discos Premium antes de usar el parámetro.</span><span class="sxs-lookup"><span data-stu-id="0f903-160">So be sure you really need Premium before using the parameter.</span></span>

### <a name="create-a-new-disk-from-the-snapshot"></a><span data-ttu-id="0f903-161">Creación de un disco a partir de la instantánea</span><span class="sxs-lookup"><span data-stu-id="0f903-161">Create a new disk from the snapshot</span></span>

<span data-ttu-id="0f903-162">Cree un disco administrado a partir de la instantánea mediante [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="0f903-162">Create a managed disk from the snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="0f903-163">Este ejemplo usa *myOSDisk* para el nombre del disco.</span><span class="sxs-lookup"><span data-stu-id="0f903-163">This example uses *myOSDisk* for the disk name.</span></span>

<span data-ttu-id="0f903-164">Cree un grupo de recursos para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f903-164">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="0f903-165">Defina el nombre del disco del SO.</span><span class="sxs-lookup"><span data-stu-id="0f903-165">Set the OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="0f903-166">Cree el disco administrado.</span><span class="sxs-lookup"><span data-stu-id="0f903-166">Create the managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-the-new-vm"></a><span data-ttu-id="0f903-167">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0f903-167">Create the new VM</span></span> 

<span data-ttu-id="0f903-168">Cree recursos de red y otros recursos de máquina virtual para que los use la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f903-168">Create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="0f903-169">Creación de la subred y la red virtual</span><span class="sxs-lookup"><span data-stu-id="0f903-169">Create the subNet and vNet</span></span>

<span data-ttu-id="0f903-170">Cree la red virtual y la subred de la [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f903-170">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="0f903-171">Cree la subred.</span><span class="sxs-lookup"><span data-stu-id="0f903-171">Create the subNet.</span></span> <span data-ttu-id="0f903-172">En este ejemplo se crea una subred llamada **mySubNet**, en el grupo de recursos **myDestinationResourceGroup** y se establece el prefijo de la dirección de subred en **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="0f903-172">This example creates a subnet named **mySubNet**, in the resource group **myDestinationResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="0f903-173">Cree la red virtual.</span><span class="sxs-lookup"><span data-stu-id="0f903-173">Create the vNet.</span></span> <span data-ttu-id="0f903-174">En este ejemplo se establece el nombre de la red virtual en **myVnetName**, la ubicación en **Oeste de EE. UU.** y el prefijo de dirección de la red virtual en **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="0f903-174">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="0f903-175">Creación del grupo de seguridad de red y las reglas de RDP</span><span class="sxs-lookup"><span data-stu-id="0f903-175">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="0f903-176">Para poder iniciar sesión en la máquina virtual mediante RDP, debe tener una regla de seguridad que permita el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="0f903-176">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="0f903-177">Como el disco duro virtual de la nueva máquina virtual se creó a partir de una máquina virtual especializada existente, puede usar una cuenta de la máquina virtual de origen para RDP.</span><span class="sxs-lookup"><span data-stu-id="0f903-177">Because the VHD for the new VM was created from an existing specialized VM, you can use an account from the source virtual machine for RDP.</span></span>

<span data-ttu-id="0f903-178">En este ejemplo se establece el nombre de NSG en **myNsg** y el nombre de la regla de RDP en **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="0f903-178">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="0f903-179">Para más información sobre puntos de conexión y reglas NSG, consulte [Apertura de puertos para una máquina virtual en Azure mediante PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f903-179">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="0f903-180">Creación de una dirección IP pública y una NIC</span><span class="sxs-lookup"><span data-stu-id="0f903-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="0f903-181">Para permitir la comunicación con la máquina virtual en la red virtual, necesitará una [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="0f903-181">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="0f903-182">Cree la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="0f903-182">Create the public IP.</span></span> <span data-ttu-id="0f903-183">En este ejemplo, el nombre de la dirección IP pública se establece en **myIP**.</span><span class="sxs-lookup"><span data-stu-id="0f903-183">In this example, the public IP address name is set to **myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="0f903-184">Cree la NIC.</span><span class="sxs-lookup"><span data-stu-id="0f903-184">Create the NIC.</span></span> <span data-ttu-id="0f903-185">En este ejemplo, el nombre de la NIC se establece en **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="0f903-185">In this example, the NIC name is set to **myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="0f903-186">Establecimiento del nombre de VM y el tamaño</span><span class="sxs-lookup"><span data-stu-id="0f903-186">Set the VM name and size</span></span>

<span data-ttu-id="0f903-187">En este ejemplo se establece el nombre de la máquina virtual como *myVM* y el tamaño de la máquina virtual en *Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="0f903-187">This example sets the VM name to *myVM* and the VM size to *Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="0f903-188">Incorporación de la NIC</span><span class="sxs-lookup"><span data-stu-id="0f903-188">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-the-os-disk"></a><span data-ttu-id="0f903-189">Adición del disco del SO</span><span class="sxs-lookup"><span data-stu-id="0f903-189">Add the OS disk</span></span> 

<span data-ttu-id="0f903-190">Agregue el disco del SO a la configuración mediante [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="0f903-190">Add the OS disk to the configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="0f903-191">Este ejemplo establece el tamaño del disco en *128 GB* y adjunta el disco administrado como un disco del SO *Windows*.</span><span class="sxs-lookup"><span data-stu-id="0f903-191">This example sets the size of the disk to *128 GB* and attaches the managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-the-vm"></a><span data-ttu-id="0f903-192">Finalización de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0f903-192">Complete the VM</span></span> 

<span data-ttu-id="0f903-193">Cree la máquina virtual mediante [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm), con las configuraciones que se acaban de crear.</span><span class="sxs-lookup"><span data-stu-id="0f903-193">Create the VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)the configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="0f903-194">Si este comando es correcto, verá un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="0f903-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="0f903-195">Comprobación de que se creó la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0f903-195">Verify that the VM was created</span></span>
<span data-ttu-id="0f903-196">Debería ver la máquina virtual recién creada en el [portal de Azure](https://portal.azure.com), en **Examinar** > **Máquinas virtuales** o mediante los comandos de PowerShell siguientes:</span><span class="sxs-lookup"><span data-stu-id="0f903-196">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="0f903-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f903-197">Next steps</span></span>
<span data-ttu-id="0f903-198">Para iniciar sesión en la nueva máquina virtual, examine la máquina virtual en el [Portal](https://portal.azure.com), haga clic en **Conectar**y abra el archivo RDP del Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="0f903-198">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="0f903-199">Utilice las credenciales de cuenta de la máquina virtual original para iniciar sesión en la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f903-199">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="0f903-200">Para más información, consulte [Conexión a una máquina virtual de Azure donde se ejecuta Windows Server e inicio de sesión en ella](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="0f903-200">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

