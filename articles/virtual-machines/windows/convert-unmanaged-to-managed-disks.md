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
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="b1c5b-103">Convertir una máquina virtual Windows de discos de toomanaged de discos no administrado</span><span class="sxs-lookup"><span data-stu-id="b1c5b-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="b1c5b-104">Si tienes existentes máquinas virtuales (VM) de Windows que usan discos no administrados, puede convertir discos de toouse administrado de máquinas virtuales de Hola a través de hello [discos de Azure administrados](managed-disks-overview.md) servicio.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="b1c5b-105">Este proceso convierte disco Hola OS y los discos de datos adjunto.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="b1c5b-106">Este artículo muestra cómo tooconvert máquinas virtuales mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="b1c5b-107">Si necesita tooinstall o actualizarlo, consulte [instalar y configurar Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b1c5b-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b1c5b-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="b1c5b-108">Before you begin</span></span>


* <span data-ttu-id="b1c5b-109">Revisión [planear la migración de Hola de discos tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="b1c5b-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="b1c5b-110">Conversión de máquinas virtuales de instancia única</span><span class="sxs-lookup"><span data-stu-id="b1c5b-110">Convert single-instance VMs</span></span>
<span data-ttu-id="b1c5b-111">Esta sección tratan cómo tooconvert instancia única máquinas virtuales de Azure de código no discos toomanaged discos.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="b1c5b-112">(Si las máquinas virtuales están en un conjunto de disponibilidad, consulte la sección siguiente de Hola.)</span><span class="sxs-lookup"><span data-stu-id="b1c5b-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="b1c5b-113">Desasignar Hola VM utilizando hello [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="b1c5b-114">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b1c5b-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="b1c5b-115">Convertir discos de máquinas virtuales hello toomanaged mediante hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="b1c5b-116">Hola siguiendo el proceso convierte Hola VM anterior, incluidos discos de hello OS y los discos de datos:</span><span class="sxs-lookup"><span data-stu-id="b1c5b-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="b1c5b-117">Iniciar Hola VM después de discos de toomanaged de conversión de hello mediante [AzureRmVM inicio](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="b1c5b-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="b1c5b-118">Después de reinicios del ejemplo de Hola Hola VM anterior:</span><span class="sxs-lookup"><span data-stu-id="b1c5b-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="b1c5b-119">Conversión de VM de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="b1c5b-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="b1c5b-120">Si máquinas virtuales de Hola que quieres tooconvert toomanaged discos están en un conjunto de disponibilidad, primero debe tooconvert Hola disponibilidad conjunto tooa administrado conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="b1c5b-121">Convertir la disponibilidad de hello establecer mediante hello [AzureRmAvailabilitySet actualización](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="b1c5b-122">Hola actualizaciones Hola conjunto con nombre de disponibilidad de ejemplo siguiente `myAvailabilitySet` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b1c5b-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="b1c5b-123">Si región Hola donde se encuentra el conjunto de disponibilidad tiene solo 2 dominios de error administrado pero número Hola de dominios de error no administrado es 3, este comando muestra un error similar demasiado "hello especifica número de dominios de error 3 debe estar en hello intervalo 1 too2."</span><span class="sxs-lookup"><span data-stu-id="b1c5b-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="b1c5b-124">tooresolve Hola error, too2 de dominio de error de actualización hello y update `Sku` demasiado`Aligned` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b1c5b-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="b1c5b-125">Cancelar la asignación y convertir máquinas virtuales de hello en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="b1c5b-126">Hello secuencia de comandos siguiente cancela la asignación de cada máquina virtual mediante el uso de hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, se convierte mediante [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)y se reinicia en [AzureRmVM de inicio ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="b1c5b-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="b1c5b-127">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="b1c5b-127">Troubleshooting</span></span>

<span data-ttu-id="b1c5b-128">Si se produce un error durante la conversión, o si una máquina virtual está en un estado de error debido a problemas en una conversión anterior, ejecute hello `ConvertTo-AzureRmVMManagedDisk` cmdlet nuevo.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="b1c5b-129">Un simple reintento normalmente desbloquea la situación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c5b-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b1c5b-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1c5b-130">Next steps</span></span>

[<span data-ttu-id="b1c5b-131">Convertir discos administrados estándar toopremium</span><span class="sxs-lookup"><span data-stu-id="b1c5b-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="b1c5b-132">Realice una copia de solo lectura de una máquina virtual mediante [instantáneas](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="b1c5b-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

