---
title: "aaaConvert una máquina virtual de Windows de código no discos toomanaged discos - Azure administrados | Documentos de Microsoft"
description: "¿Cómo tooconvert una VM de Windows de discos no administrado toomanaged discos mediante PowerShell en el modelo de implementación del Administrador de recursos de Hola"
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
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Convertir una máquina virtual Windows de discos de toomanaged de discos no administrado

Si tienes existentes máquinas virtuales (VM) de Windows que usan discos no administrados, puede convertir discos de toouse administrado de máquinas virtuales de Hola a través de hello [discos de Azure administrados](managed-disks-overview.md) servicio. Este proceso convierte disco Hola OS y los discos de datos adjunto.

Este artículo muestra cómo tooconvert máquinas virtuales mediante el uso de PowerShell de Azure. Si necesita tooinstall o actualizarlo, consulte [instalar y configurar Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Antes de empezar


* Revisión [planear la migración de Hola de discos tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Conversión de máquinas virtuales de instancia única
Esta sección tratan cómo tooconvert instancia única máquinas virtuales de Azure de código no discos toomanaged discos. (Si las máquinas virtuales están en un conjunto de disponibilidad, consulte la sección siguiente de Hola.) 

1. Desasignar Hola VM utilizando hello [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet. Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Convertir discos de máquinas virtuales hello toomanaged mediante hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet. Hola siguiendo el proceso convierte Hola VM anterior, incluidos discos de hello OS y los discos de datos:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Iniciar Hola VM después de discos de toomanaged de conversión de hello mediante [AzureRmVM inicio](/powershell/module/azurerm.compute/start-azurermvm). Después de reinicios del ejemplo de Hola Hola VM anterior:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Conversión de VM de un conjunto de disponibilidad

Si máquinas virtuales de Hola que quieres tooconvert toomanaged discos están en un conjunto de disponibilidad, primero debe tooconvert Hola disponibilidad conjunto tooa administrado conjunto de disponibilidad.

1. Convertir la disponibilidad de hello establecer mediante hello [AzureRmAvailabilitySet actualización](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet. Hola actualizaciones Hola conjunto con nombre de disponibilidad de ejemplo siguiente `myAvailabilitySet` en grupo de recursos de hello llamado `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Si región Hola donde se encuentra el conjunto de disponibilidad tiene solo 2 dominios de error administrado pero número Hola de dominios de error no administrado es 3, este comando muestra un error similar demasiado "hello especifica número de dominios de error 3 debe estar en hello intervalo 1 too2." tooresolve Hola error, too2 de dominio de error de actualización hello y update `Sku` demasiado`Aligned` como se indica a continuación:

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Cancelar la asignación y convertir máquinas virtuales de hello en el conjunto de disponibilidad de Hola. Hello secuencia de comandos siguiente cancela la asignación de cada máquina virtual mediante el uso de hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, se convierte mediante [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)y se reinicia en [AzureRmVM de inicio ](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>Solución de problemas

Si se produce un error durante la conversión, o si una máquina virtual está en un estado de error debido a problemas en una conversión anterior, ejecute hello `ConvertTo-AzureRmVMManagedDisk` cmdlet nuevo. Un simple reintento normalmente desbloquea la situación de Hola.


## <a name="next-steps"></a>Pasos siguientes

[Convertir discos administrados estándar toopremium](convert-disk-storage.md)

Realice una copia de solo lectura de una máquina virtual mediante [instantáneas](snapshot-copy-managed-disk.md).

