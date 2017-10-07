---
title: aaaUse PowerShell tooresize una VM de Windows en Azure | Documentos de Microsoft
description: "Cambiar el tamaño de una máquina virtual de Windows creada en el modelo de implementación de administrador de recursos de hello, uso de Powershell de Azure."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a>Cambio de tamaño de una máquina virtual Windows
Este artículo muestra cómo se tooresize una VM de Windows, creado en el modelo de implementación del Administrador de recursos Hola con Azure Powershell.

Después de crear una máquina virtual (VM), puede escalar Hola VM hacia arriba o hacia abajo al cambiar el tamaño de la máquina virtual de Hola. En algunos casos, debe desasignar Hola VM en primer lugar. Esto puede ocurrir si no está disponible en clúster de hardware de Hola que hospeda actualmente Hola VM nuevo tamaño de Hola.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Cambio de tamaño de una máquina virtual Windows que no está en un conjunto de disponibilidad
1. Lista de tamaños de máquinas virtuales de Hola que están disponibles en el clúster de hardware de Hola donde se hospeda Hola máquina virtual. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. Si Hola deseado se muestra el tamaño, ejecute hello después comandos tooresize Hola VM. Si Hola deseado tamaño no aparece, vaya toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Si Hola deseado no se especifica tamaño, ejecute hello siga los comandos toodeallocate Hola VM, cambiar su tamaño y reiniciar Hola VM.
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> Hola desasignar VM libera todas las direcciones IP dinámicas asignadas toohello máquina virtual. Hola OS y discos de datos no se ven afectados. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Cambio de tamaño de una máquina virtual Windows que está en un conjunto de disponibilidad
Si hello nuevo tamaño de una máquina virtual en un conjunto de disponibilidad no está disponible en el clúster de hardware de hello hospedando Hola VM y, a continuación, todas las máquinas virtuales en el conjunto de disponibilidad de Hola será necesario toobe desasignado tooresize Hola máquina virtual. También podrían necesitar tooupdate tamaño de Hola de otras máquinas virtuales en la disponibilidad de hello establecer después de que se ha cambiado el tamaño de una máquina virtual. tooresize una máquina virtual en un conjunto de disponibilidad, realizar Hola pasos.

1. Lista de tamaños de máquinas virtuales de Hola que están disponibles en el clúster de hardware de Hola donde se hospeda Hola máquina virtual.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. Si Hola deseado se muestra el tamaño, ejecute hello después comandos tooresize Hola VM. Si no aparece, vaya toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Si Hola deseado no se especifica tamaño, continuar con hello siguiendo los pasos toodeallocate todas las máquinas virtuales en el conjunto de disponibilidad de hello, cambiar el tamaño de las máquinas virtuales y reiniciarlas una vez.
4. Detener todas las máquinas virtuales en el conjunto de disponibilidad de Hola.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. Cambiar el tamaño y reinicie hello las máquinas virtuales en el conjunto de disponibilidad de Hola.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente. Para obtener más información, consulte el artículo sobre [escalado automático de máquinas Linux en un conjunto de escalado de máquinas virtuales](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

