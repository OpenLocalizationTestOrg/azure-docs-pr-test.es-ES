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
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a>Adjuntar un tooa de disco de datos VM de Windows con PowerShell

Este artículo muestra cómo tooattach nueva y existente discos de máquina virtual de Windows de tooa mediante PowerShell. Si la VM utiliza discos administrados, puede conectar discos de datos administrados adicionales. También puede adjuntar discos de datos no administrados tooa VM que use un disco no administrado en una cuenta de almacenamiento.

Antes de hacerlo, revise estas sugerencias:
* tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar. Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* toouse almacenamiento Premium, necesitará un almacenamiento Premium habilitado tamaño de máquina virtual como Hola DS-series o GS-series máquina virtual. Puede utilizar discos de cuentas de almacenamiento premium y estándar con estas máquinas virtuales. Almacenamiento premium está disponible en determinadas regiones. Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="before-you-begin"></a>Antes de empezar
Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell. Ejecutar Hola siguientes tooinstall de comando.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a>Agregar una máquina virtual de datos vacíos disco tooa

Este ejemplo muestra cómo tooadd una datos vacíos disco de máquina virtual existente de tooan.

### <a name="using-managed-disks"></a>Uso de discos administrados

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a>Uso de discos no administrados en una cuenta de almacenamiento

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a>Inicializar disco Hola

Después de agregar un disco vacío, necesita tooinitialize lo. disco de hello tooinitialize, puede iniciar sesión en administración de discos de máquina virtual y el uso de tooa. Si habilita WinRM y un certificado en hello VM al crearlo, puede usar disco de hello tooinitialize de PowerShell remoto. También puede utilizar una extensión de script personalizada: 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
archivo de script de Hola puede contener algo parecido a los discos de Hola de tooinitialize de este código:

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a>Adjuntar un tooa de disco de datos VM existente

También puede adjuntar un disco duro virtual existente como una máquina virtual de datos administrados disco tooa. 

### <a name="using-managed-disks"></a>Uso de discos administrados

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

## <a name="next-steps"></a>Pasos siguientes

Crear una [instantánea](snapshot-copy-managed-disk.md).
