---
title: aaaExpand un disco de datos adjunta tooa VM de Windows en Azure | Documentos de Microsoft
description: "Expanda Hola tamaño de un disco de datos que está adjunto tooa de la máquina de virtual de Windows con PowerShell."
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="674fe-103">Aumente el tamaño de Hola de un disco de datos adjunta tooa VM de Windows</span><span class="sxs-lookup"><span data-stu-id="674fe-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="674fe-104">Si necesita tooincrease tamaño de Hola de máquina virtual de hello datos disco conectado tooyour, puede aumentar tamaño de hello mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="674fe-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="674fe-105">Después de aumentar el tamaño de Hola Hola del disco de datos en la configuración de máquina virtual de Azure de hello, también necesita tooallocate Hola nuevo espacio en disco en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="674fe-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="674fe-106">Usar Powershell tooincrease Hola tamaño de un disco de datos administrados</span><span class="sxs-lookup"><span data-stu-id="674fe-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="674fe-107">tamaño de hello tooincrease de un disco de datos administrados, Hola de uso después de cmdlets de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="674fe-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="674fe-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="674fe-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="674fe-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="674fe-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="674fe-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="674fe-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="674fe-111">Update-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="674fe-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="674fe-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="674fe-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="674fe-113">Hello secuencia de comandos siguiente le guiará a través de obtener información de la máquina virtual de hello, selección de disco de datos de Hola y especificar el nuevo tamaño de Hola.</span><span class="sxs-lookup"><span data-stu-id="674fe-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="674fe-114">Usar PowerShell tooincrease Hola tamaño de un disco de datos no administrados</span><span class="sxs-lookup"><span data-stu-id="674fe-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="674fe-115">tamaño de hello tooincrease de discos de datos no administrados en una cuenta de almacenamiento, Hola de uso después de cmdlets de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="674fe-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="674fe-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="674fe-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="674fe-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="674fe-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="674fe-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="674fe-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="674fe-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="674fe-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="674fe-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="674fe-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="674fe-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="674fe-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="674fe-122">Hello secuencia de comandos siguiente le guiará a través de obtener información de cuenta de máquina virtual y almacenamiento hello, selección de disco de datos de Hola y especificar el nuevo tamaño de Hola.</span><span class="sxs-lookup"><span data-stu-id="674fe-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="674fe-123">Asignar espacio en disco sin asignar de Hola</span><span class="sxs-lookup"><span data-stu-id="674fe-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="674fe-124">Una vez haya realizado una unidad de hello más grande, debe tooallocate Hola nuevo espacio sin asignar desde dentro de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="674fe-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="674fe-125">espacio de hello tooallocate, puede conectar uso de máquina virtual de toohello administración de discos (diskmgmt.msc).</span><span class="sxs-lookup"><span data-stu-id="674fe-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="674fe-126">O bien, si habilita WinRM y un certificado en hello VM al crearlo, puede usar discos de hello tooinitialize de PowerShell remota.</span><span class="sxs-lookup"><span data-stu-id="674fe-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="674fe-127">También puede utilizar una extensión de script personalizada:</span><span class="sxs-lookup"><span data-stu-id="674fe-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="674fe-128">archivo de script de Hola puede contener algo parecido a este código tooincrease Hola unidad asignación toohello tamaño máximo Hola discos:</span><span class="sxs-lookup"><span data-stu-id="674fe-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="674fe-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="674fe-129">Next Steps</span></span>
- [<span data-ttu-id="674fe-130">Más información sobre los discos y VHD</span><span class="sxs-lookup"><span data-stu-id="674fe-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
