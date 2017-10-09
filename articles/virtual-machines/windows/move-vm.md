---
title: "aaaMove un recurso de máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Mover una máquina virtual de Windows tooanother suscripción de Azure o el grupo de recursos en el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="d593a-103">Mover una máquina virtual de Windows tooanother suscripción de Azure o un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d593a-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="d593a-104">En este artículo se explica cómo toomove una VM de Windows entre grupos de recursos o suscripciones.</span><span class="sxs-lookup"><span data-stu-id="d593a-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="d593a-105">Mover entre suscripciones puede resultar útil si originalmente se crea una máquina virtual en una suscripción personal y ahora desea toomove se toocontinue de suscripción de la compañía de tooyour su trabajo.</span><span class="sxs-lookup"><span data-stu-id="d593a-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="d593a-106">No se puede mover discos administrados en este momento.</span><span class="sxs-lookup"><span data-stu-id="d593a-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="d593a-107">Identificadores de recursos nuevos se crean como parte del movimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d593a-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="d593a-108">Una vez hello máquina virtual se ha movido, deberá tooupdate los scripts y herramientas toouse Hola nuevos identificadores de recursos.</span><span class="sxs-lookup"><span data-stu-id="d593a-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="d593a-109">Usar Powershell toomove una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d593a-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="d593a-110">toomove un grupo de recursos de máquina virtual tooanother, deberá toomake seguro de que mueva todos los recursos dependientes Hola.</span><span class="sxs-lookup"><span data-stu-id="d593a-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="d593a-111">toouse Hola Move-AzureRMResource cmdlet, necesita el nombre del recurso de Hola y Hola tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d593a-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="d593a-112">Puede obtener ambas cosas de cmdlet Find-AzureRMResource Hola.</span><span class="sxs-lookup"><span data-stu-id="d593a-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="d593a-113">toomove una máquina virtual que necesitamos toomove varios recursos.</span><span class="sxs-lookup"><span data-stu-id="d593a-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="d593a-114">Podemos crear variables independientes para cada recurso y, luego, enumerarlos.</span><span class="sxs-lookup"><span data-stu-id="d593a-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="d593a-115">Este ejemplo incluye la mayoría de los recursos básicos de Hola para una máquina virtual, pero puede agregar más según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d593a-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="d593a-116">toomove Hola suscripción de recursos de toodifferent, incluya hello **DestinationSubscriptionId -** parámetro.</span><span class="sxs-lookup"><span data-stu-id="d593a-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="d593a-117">Se le pedirá tooconfirm que desea toomove Hola de los recursos especificados.</span><span class="sxs-lookup"><span data-stu-id="d593a-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="d593a-118">Tipo de **Y** tooconfirm que desea que los recursos de hello toomove.</span><span class="sxs-lookup"><span data-stu-id="d593a-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d593a-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d593a-119">Next steps</span></span>
<span data-ttu-id="d593a-120">Puede mover muchos tipos diferentes de recursos entre suscripciones y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="d593a-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="d593a-121">Para obtener más información, consulte [Mover grupo de recursos de toonew de recursos o suscripción](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d593a-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

