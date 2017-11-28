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
# <a name="resize-a-windows-vm"></a><span data-ttu-id="05ad4-103">Cambio de tamaño de una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="05ad4-103">Resize a Windows VM</span></span>
<span data-ttu-id="05ad4-104">Este artículo muestra cómo se tooresize una VM de Windows, creado en el modelo de implementación del Administrador de recursos Hola con Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="05ad4-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="05ad4-105">Después de crear una máquina virtual (VM), puede escalar Hola VM hacia arriba o hacia abajo al cambiar el tamaño de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="05ad4-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="05ad4-106">En algunos casos, debe desasignar Hola VM en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="05ad4-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="05ad4-107">Esto puede ocurrir si no está disponible en clúster de hardware de Hola que hospeda actualmente Hola VM nuevo tamaño de Hola.</span><span class="sxs-lookup"><span data-stu-id="05ad4-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="05ad4-108">Cambio de tamaño de una máquina virtual Windows que no está en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="05ad4-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="05ad4-109">Lista de tamaños de máquinas virtuales de Hola que están disponibles en el clúster de hardware de Hola donde se hospeda Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05ad4-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="05ad4-110">Si Hola deseado se muestra el tamaño, ejecute hello después comandos tooresize Hola VM.</span><span class="sxs-lookup"><span data-stu-id="05ad4-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="05ad4-111">Si Hola deseado tamaño no aparece, vaya toostep 3.</span><span class="sxs-lookup"><span data-stu-id="05ad4-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="05ad4-112">Si Hola deseado no se especifica tamaño, ejecute hello siga los comandos toodeallocate Hola VM, cambiar su tamaño y reiniciar Hola VM.</span><span class="sxs-lookup"><span data-stu-id="05ad4-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
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
> <span data-ttu-id="05ad4-113">Hola desasignar VM libera todas las direcciones IP dinámicas asignadas toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05ad4-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="05ad4-114">Hola OS y discos de datos no se ven afectados.</span><span class="sxs-lookup"><span data-stu-id="05ad4-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="05ad4-115">Cambio de tamaño de una máquina virtual Windows que está en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="05ad4-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="05ad4-116">Si hello nuevo tamaño de una máquina virtual en un conjunto de disponibilidad no está disponible en el clúster de hardware de hello hospedando Hola VM y, a continuación, todas las máquinas virtuales en el conjunto de disponibilidad de Hola será necesario toobe desasignado tooresize Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05ad4-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="05ad4-117">También podrían necesitar tooupdate tamaño de Hola de otras máquinas virtuales en la disponibilidad de hello establecer después de que se ha cambiado el tamaño de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05ad4-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="05ad4-118">tooresize una máquina virtual en un conjunto de disponibilidad, realizar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="05ad4-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="05ad4-119">Lista de tamaños de máquinas virtuales de Hola que están disponibles en el clúster de hardware de Hola donde se hospeda Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05ad4-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="05ad4-120">Si Hola deseado se muestra el tamaño, ejecute hello después comandos tooresize Hola VM.</span><span class="sxs-lookup"><span data-stu-id="05ad4-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="05ad4-121">Si no aparece, vaya toostep 3.</span><span class="sxs-lookup"><span data-stu-id="05ad4-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="05ad4-122">Si Hola deseado no se especifica tamaño, continuar con hello siguiendo los pasos toodeallocate todas las máquinas virtuales en el conjunto de disponibilidad de hello, cambiar el tamaño de las máquinas virtuales y reiniciarlas una vez.</span><span class="sxs-lookup"><span data-stu-id="05ad4-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="05ad4-123">Detener todas las máquinas virtuales en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="05ad4-123">Stop all VMs in hello availability set.</span></span>
   
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
5. <span data-ttu-id="05ad4-124">Cambiar el tamaño y reinicie hello las máquinas virtuales en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="05ad4-124">Resize and restart hello VMs in hello availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="05ad4-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05ad4-125">Next steps</span></span>
* <span data-ttu-id="05ad4-126">Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente. Para obtener más información, consulte el artículo sobre [escalado automático de máquinas Linux en un conjunto de escalado de máquinas virtuales](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="05ad4-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

