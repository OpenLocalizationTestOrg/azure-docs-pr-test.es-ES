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
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Mover una máquina virtual de Windows tooanother suscripción de Azure o un grupo de recursos
En este artículo se explica cómo toomove una VM de Windows entre grupos de recursos o suscripciones. Mover entre suscripciones puede resultar útil si originalmente se crea una máquina virtual en una suscripción personal y ahora desea toomove se toocontinue de suscripción de la compañía de tooyour su trabajo.

> [!IMPORTANT]
>No se puede mover discos administrados en este momento. 
>
>Identificadores de recursos nuevos se crean como parte del movimiento de Hola. Una vez hello máquina virtual se ha movido, deberá tooupdate los scripts y herramientas toouse Hola nuevos identificadores de recursos. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>Usar Powershell toomove una máquina virtual
toomove un grupo de recursos de máquina virtual tooanother, deberá toomake seguro de que mueva todos los recursos dependientes Hola. toouse Hola Move-AzureRMResource cmdlet, necesita el nombre del recurso de Hola y Hola tipo de recurso. Puede obtener ambas cosas de cmdlet Find-AzureRMResource Hola.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


toomove una máquina virtual que necesitamos toomove varios recursos. Podemos crear variables independientes para cada recurso y, luego, enumerarlos. Este ejemplo incluye la mayoría de los recursos básicos de Hola para una máquina virtual, pero puede agregar más según sea necesario.

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

toomove Hola suscripción de recursos de toodifferent, incluya hello **DestinationSubscriptionId -** parámetro. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



Se le pedirá tooconfirm que desea toomove Hola de los recursos especificados. Tipo de **Y** tooconfirm que desea que los recursos de hello toomove.

## <a name="next-steps"></a>Pasos siguientes
Puede mover muchos tipos diferentes de recursos entre suscripciones y grupos de recursos. Para obtener más información, consulte [Mover grupo de recursos de toonew de recursos o suscripción](../../resource-group-move-resources.md).    

