---
title: "Uso de PowerShell para cambiar el tamaño de una máquina virtual Windows en Azure | Microsoft Docs"
description: "Cambie el tamaño de una máquina virtual Windows creada con el modelo de implementación de Resource Manager utilizando Azure PowerShell."
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
ms.openlocfilehash: 742efd1496de9ce76b1e5636297ef30f546bd108
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="4b84a-103">Cambio de tamaño de una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="4b84a-103">Resize a Windows VM</span></span>
<span data-ttu-id="4b84a-104">En este artículo se muestra cómo cambiar de tamaño una máquina virtual Windows creada con el modelo de implementación de Resource Manager utilizando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b84a-104">This article shows you how to resize a Windows VM, created in the Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="4b84a-105">Después de crear una máquina virtual, puede escalarla o reducirla verticalmente cambiando su tamaño.</span><span class="sxs-lookup"><span data-stu-id="4b84a-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span></span> <span data-ttu-id="4b84a-106">En algunos casos, hay que desasignarla antes.</span><span class="sxs-lookup"><span data-stu-id="4b84a-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="4b84a-107">Esto puede suceder si el nuevo tamaño no está disponible en el clúster de hardware que hospeda la actualmente la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4b84a-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="4b84a-108">Cambio de tamaño de una máquina virtual Windows que no está en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="4b84a-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="4b84a-109">Muestre los tamaños de máquina virtual que están disponibles en el clúster de hardware donde se hospeda la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4b84a-109">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="4b84a-110">Si se muestra el tamaño deseado, ejecute el comando siguiente para cambiar el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4b84a-110">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="4b84a-111">Si el tamaño deseado no aparece, vaya al paso 3.</span><span class="sxs-lookup"><span data-stu-id="4b84a-111">If the desired size is not listed, go on to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="4b84a-112">Si, por el contrario, no aparece el tamaño deseado, ejecute los siguientes comandos para desasignar la máquina virtual, cambiar su tamaño y reiniciarla.</span><span class="sxs-lookup"><span data-stu-id="4b84a-112">If the desired size is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span></span>
   
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
> <span data-ttu-id="4b84a-113">Al desasignar la máquina virtual, se liberan todas las direcciones IP dinámicas asignadas a ella.</span><span class="sxs-lookup"><span data-stu-id="4b84a-113">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="4b84a-114">Esto no afecta a los discos del SO y de datos.</span><span class="sxs-lookup"><span data-stu-id="4b84a-114">The OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="4b84a-115">Cambio de tamaño de una máquina virtual Windows que está en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="4b84a-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="4b84a-116">Si el nuevo tamaño de una máquina virtual de un conjunto de disponibilidad no está disponible en el clúster de hardware que hospeda la máquina virtual, habrá que desasignar todas las máquinas virtuales del conjunto de disponibilidad para cambiar el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4b84a-116">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span></span> <span data-ttu-id="4b84a-117">También tendrá que actualizar el tamaño de otras máquinas virtuales del conjunto de disponibilidad después de cambiar el tamaño de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4b84a-117">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span></span> <span data-ttu-id="4b84a-118">Para cambiar el tamaño de una máquina virtual de un conjunto de disponibilidad, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="4b84a-118">To resize a VM in an availability set, perform the following steps.</span></span>

1. <span data-ttu-id="4b84a-119">Muestre los tamaños de máquina virtual que están disponibles en el clúster de hardware donde se hospeda la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4b84a-119">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="4b84a-120">Si se muestra el tamaño deseado, ejecute el comando siguiente para cambiar el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4b84a-120">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="4b84a-121">Si no aparece, vaya al paso 3.</span><span class="sxs-lookup"><span data-stu-id="4b84a-121">If it is not listed, go to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="4b84a-122">Si el tamaño deseado no aparece, continúe con los pasos siguientes para cancelar todas las máquinas virtuales dl conjunto de disponibilidad, cambiarles el tamaño y reiniciarlas.</span><span class="sxs-lookup"><span data-stu-id="4b84a-122">If the desired size is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="4b84a-123">Detenga todas las máquinas virtuales del conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="4b84a-123">Stop all VMs in the availability set.</span></span>
   
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
5. <span data-ttu-id="4b84a-124">Cambie el tamaño de todas las máquinas virtuales del conjunto de disponibilidad y reinícielas.</span><span class="sxs-lookup"><span data-stu-id="4b84a-124">Resize and restart the VMs in the availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="4b84a-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b84a-125">Next steps</span></span>
* <span data-ttu-id="4b84a-126">Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="4b84a-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="4b84a-127">Para obtener más información, consulte el artículo sobre [escalado automático de máquinas Linux en un conjunto de escalado de máquinas virtuales](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="4b84a-127">For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

