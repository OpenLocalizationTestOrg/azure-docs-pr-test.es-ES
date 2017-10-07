---
title: aaaAttach un tooa de disco de datos VM de Windows en Azure mediante PowerShell | Documentos de Microsoft
description: "Cómo los datos nuevo o existente de tooattach disco tooa máquina virtual de Windows con PowerShell con el modelo de implementación del Administrador de recursos de Hola."
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
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="22c99-103">Adjuntar un tooa de disco de datos VM de Windows con PowerShell</span><span class="sxs-lookup"><span data-stu-id="22c99-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="22c99-104">Este artículo muestra cómo tooattach nueva y existente discos de máquina virtual de Windows de tooa mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22c99-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="22c99-105">Si la VM utiliza discos administrados, puede conectar discos de datos administrados adicionales.</span><span class="sxs-lookup"><span data-stu-id="22c99-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="22c99-106">También puede adjuntar discos de datos no administrados tooa VM que use un disco no administrado en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="22c99-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="22c99-107">Antes de hacerlo, revise estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="22c99-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="22c99-108">tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar.</span><span class="sxs-lookup"><span data-stu-id="22c99-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="22c99-109">Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22c99-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="22c99-110">toouse almacenamiento Premium, necesitará un almacenamiento Premium habilitado tamaño de máquina virtual como Hola DS-series o GS-series máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22c99-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="22c99-111">Puede utilizar discos de cuentas de almacenamiento premium y estándar con estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="22c99-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="22c99-112">Almacenamiento premium está disponible en determinadas regiones.</span><span class="sxs-lookup"><span data-stu-id="22c99-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="22c99-113">Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="22c99-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="22c99-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="22c99-114">Before you begin</span></span>
<span data-ttu-id="22c99-115">Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22c99-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="22c99-116">Ejecutar Hola siguientes tooinstall de comando.</span><span class="sxs-lookup"><span data-stu-id="22c99-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="22c99-117">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="22c99-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="22c99-118">Agregar una máquina virtual de datos vacíos disco tooa</span><span class="sxs-lookup"><span data-stu-id="22c99-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="22c99-119">Este ejemplo muestra cómo tooadd una datos vacíos disco de máquina virtual existente de tooan.</span><span class="sxs-lookup"><span data-stu-id="22c99-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="22c99-120">Uso de discos administrados</span><span class="sxs-lookup"><span data-stu-id="22c99-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="22c99-121">Uso de discos no administrados en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="22c99-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="22c99-122">Inicializar disco Hola</span><span class="sxs-lookup"><span data-stu-id="22c99-122">Initialize hello disk</span></span>

<span data-ttu-id="22c99-123">Después de agregar un disco vacío, necesita tooinitialize lo.</span><span class="sxs-lookup"><span data-stu-id="22c99-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="22c99-124">disco de hello tooinitialize, puede iniciar sesión en administración de discos de máquina virtual y el uso de tooa.</span><span class="sxs-lookup"><span data-stu-id="22c99-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="22c99-125">Si habilita WinRM y un certificado en hello VM al crearlo, puede usar disco de hello tooinitialize de PowerShell remoto.</span><span class="sxs-lookup"><span data-stu-id="22c99-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="22c99-126">También puede utilizar una extensión de script personalizada:</span><span class="sxs-lookup"><span data-stu-id="22c99-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="22c99-127">archivo de script de Hola puede contener algo parecido a los discos de Hola de tooinitialize de este código:</span><span class="sxs-lookup"><span data-stu-id="22c99-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="22c99-128">Adjuntar un tooa de disco de datos VM existente</span><span class="sxs-lookup"><span data-stu-id="22c99-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="22c99-129">También puede adjuntar un disco duro virtual existente como una máquina virtual de datos administrados disco tooa.</span><span class="sxs-lookup"><span data-stu-id="22c99-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="22c99-130">Uso de discos administrados</span><span class="sxs-lookup"><span data-stu-id="22c99-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="22c99-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22c99-131">Next steps</span></span>

<span data-ttu-id="22c99-132">Crear una [instantánea](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="22c99-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
