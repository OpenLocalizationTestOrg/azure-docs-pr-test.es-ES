---
title: "aaaConvert Azure administra el almacenamiento de discos de toopremium estándar y viceversa. | Documentos de Microsoft"
description: "Cómo tooconvert Azure administra los discos de toopremium estándar y viceversa, mediante el uso de PowerShell de Azure."
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Convertir Azure administra el almacenamiento de discos de toopremium estándar y viceversa.

Managed Disks ofrece dos opciones de almacenamiento: [Premium](../../storage/storage-premium-storage.md) (basado en SSD) y [Estándar](../../storage/storage-standard-storage.md) (basado en HDD). Permite cambiar de tooeasily entre las opciones de hello dos con el tiempo de inactividad mínimo según sus necesidades de rendimiento. Esta funcionalidad no está disponible con discos no administrados. Pero puede fácilmente [convertir discos toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily conmutador entre las opciones de hello dos.

Este artículo muestra cómo tooconvert administra los discos de toopremium estándar y viceversa mediante Azure PowerShell. Si necesita tooinstall o actualizarlo, consulte [instalar y configurar Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Antes de empezar

* conversión de Hello requiere un reinicio de hello VM, por lo que programar la migración de Hola de discos del almacenamiento de datos durante un período de mantenimiento existente. 
* Si usas discos no administrados, en primer lugar [convertir discos toomanaged](convert-unmanaged-to-managed-disks.md) toouse esta tooswitch artículo entre las opciones de almacenamiento de hello dos. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Convert Hola a todos los discos de una máquina virtual administrados por de toopremium estándar y viceversa.

En el siguiente ejemplo de Hola, mostramos cómo tooswitch todos los discos de una máquina virtual desde el almacenamiento de toopremium estándar de Hola. discos administrados por toouse premium, la máquina virtual debe usar un [tamaño de máquina virtual](sizes.md) que admite el almacenamiento premium. En este ejemplo también cambia de tamaño de tooa que admite el almacenamiento premium.

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Convertir un disco administrado de toopremium estándar y viceversa.

Para la carga de trabajo de desarrollo y pruebas, puede que desee toohave mezcla de discos estándar y premium tooreduce su costo. Que puede realizar mediante la actualización de almacenamiento de toopremium, solo los discos de Hola que requieren un mejor rendimiento. En el siguiente ejemplo de Hola, mostramos cómo tooswitch un único disco de una máquina virtual desde el almacenamiento de toopremium estándar y viceversa. discos administrados por toouse premium, la máquina virtual debe usar un [tamaño de máquina virtual](sizes.md) que admite el almacenamiento premium. En este ejemplo también cambia de tamaño de tooa que admite el almacenamiento premium.

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a>Pasos siguientes

Realice una copia de solo lectura de una máquina virtual mediante [instantáneas](snapshot-copy-managed-disk.md).

