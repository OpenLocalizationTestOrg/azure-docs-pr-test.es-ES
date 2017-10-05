---
title: "Conexión de un disco de datos a una VM con Windows en Azure mediante PowerShell | Microsoft Docs"
description: "Cómo conectar un disco de datos nuevo o existente a una VM con Windows mediante PowerShell con el modelo de implementación de Resource Manager."
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
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 486e6a27fa28ec63001d824fe9f59c03a7aea5a7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-vm-using-powershell"></a><span data-ttu-id="4c07c-103">Conexión de un disco a una VM con Windows mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c07c-103">Attach a data disk to a Windows VM using PowerShell</span></span>

<span data-ttu-id="4c07c-104">En este artículo se explica cómo conectar discos nuevos y existentes a una máquina virtual con Windows mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4c07c-104">This article shows you how to attach both new and existing disks to a Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="4c07c-105">Si la VM utiliza discos administrados, puede conectar discos de datos administrados adicionales.</span><span class="sxs-lookup"><span data-stu-id="4c07c-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="4c07c-106">También puede conectar discos de datos no administrados a una VM que usa discos no administrados en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4c07c-106">You can also attach unmanaged data disks to a VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="4c07c-107">Antes de hacerlo, revise estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="4c07c-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="4c07c-108">El tamaño de la máquina virtual controla cuántos discos de datos puede conectar.</span><span class="sxs-lookup"><span data-stu-id="4c07c-108">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="4c07c-109">Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c07c-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="4c07c-110">Para usar Premium Storage, necesitará una VM con Premium Storage habilitado con un tamaño como el de las VM de las series DS o GS.</span><span class="sxs-lookup"><span data-stu-id="4c07c-110">To use Premium storage, you'll need a Premium Storage enabled VM size like the DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="4c07c-111">Puede utilizar discos de cuentas de almacenamiento premium y estándar con estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4c07c-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="4c07c-112">Almacenamiento premium está disponible en determinadas regiones.</span><span class="sxs-lookup"><span data-stu-id="4c07c-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="4c07c-113">Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4c07c-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4c07c-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4c07c-114">Before you begin</span></span>
<span data-ttu-id="4c07c-115">Si usa PowerShell, asegúrese de que tiene la versión más reciente del módulo de PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="4c07c-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="4c07c-116">Ejecute el siguiente comando para instalarla.</span><span class="sxs-lookup"><span data-stu-id="4c07c-116">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="4c07c-117">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="4c07c-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-to-a-virtual-machine"></a><span data-ttu-id="4c07c-118">Incorporación de un disco de datos vacío a una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4c07c-118">Add an empty data disk to a virtual machine</span></span>

<span data-ttu-id="4c07c-119">En este ejemplo se muestra cómo agregar un disco de datos vacío a una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="4c07c-119">This example shows how to add an empty data disk to an existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="4c07c-120">Uso de discos administrados</span><span class="sxs-lookup"><span data-stu-id="4c07c-120">Using managed disks</span></span>

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="4c07c-121">Uso de discos no administrados en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4c07c-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-the-disk"></a><span data-ttu-id="4c07c-122">Initialize the disk</span><span class="sxs-lookup"><span data-stu-id="4c07c-122">Initialize the disk</span></span>

<span data-ttu-id="4c07c-123">Después de agregar un disco vacío, debe inicializarlo.</span><span class="sxs-lookup"><span data-stu-id="4c07c-123">After you add an empty disk, you need to initialize it.</span></span> <span data-ttu-id="4c07c-124">Para hacerlo, puede iniciar sesión en una VM y usar la administración de discos.</span><span class="sxs-lookup"><span data-stu-id="4c07c-124">To initialize the disk, you can log in to a VM and use disk management.</span></span> <span data-ttu-id="4c07c-125">Si habilitó WinRM y un certificado en la VM cuando la creó, puede usar PowerShell remoto para inicializar el disco.</span><span class="sxs-lookup"><span data-stu-id="4c07c-125">If you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="4c07c-126">También puede utilizar una extensión de script personalizada:</span><span class="sxs-lookup"><span data-stu-id="4c07c-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="4c07c-127">El archivo de script puede tener un contenido parecido a este código para inicializar los discos:</span><span class="sxs-lookup"><span data-stu-id="4c07c-127">The script file can contain something like this code to initialize the disks:</span></span>

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-to-a-vm"></a><span data-ttu-id="4c07c-128">Incorporación de un disco de datos existente a una VM</span><span class="sxs-lookup"><span data-stu-id="4c07c-128">Attach an existing data disk to a VM</span></span>

<span data-ttu-id="4c07c-129">También puede conectar un VHD existente como un disco de datos administrado a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4c07c-129">You can also attach an existing VHD as a managed data disk to a virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="4c07c-130">Uso de discos administrados</span><span class="sxs-lookup"><span data-stu-id="4c07c-130">Using managed disks</span></span>

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a><span data-ttu-id="4c07c-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c07c-131">Next steps</span></span>

<span data-ttu-id="4c07c-132">Crear una [instantánea](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="4c07c-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
