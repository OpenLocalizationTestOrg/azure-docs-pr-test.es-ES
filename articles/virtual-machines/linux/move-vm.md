---
title: aaaMove una VM de Linux en Azure | Documentos de Microsoft
description: "Mover una VM de Linux tooanother suscripción de Azure o un grupo de recursos en el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Mover un VM de Linux tooanother suscripción o grupo de recursos
En este artículo se explica cómo toomove una VM Linux entre grupos de recursos o suscripciones. Mover una máquina virtual entre suscripciones puede resultar útil si ha creado una máquina virtual en una suscripción personal y ahora desea toomove la suscripción de la empresa tooyour.

> [!IMPORTANT]
>No se puede mover discos administrados en este momento. 
>
>Identificadores de recursos nuevos se crean como parte del movimiento de Hola. Una vez hello máquina virtual se ha movido, deberá tooupdate los scripts y herramientas toouse Hola nuevos identificadores de recursos. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Usar hello Azure CLI toomove una máquina virtual
toosuccessfully mover una máquina virtual, deberá toomove Hola VM y todos sus recursos de soporte. Hola de uso **mostrar grupo azure** comando toolist todos los recursos de hello en un grupo de recursos y sus identificadores. Salida de hello toopipe de este archivo de comandos tooa es útil para que pueda copiar y pegar Hola identificadores en los comandos posteriores.

    azure group show <resourceGroupName>

toomove una máquina virtual y su grupo de recursos tooanother de recursos, utilice hello **mover recursos de azure** comando de CLI. Hola de ejemplo siguiente muestra cómo toomove una máquina virtual y los recursos más comunes de hello requiere. Usamos hello **-i** parámetro y pase una-lista separados por comas (sin espacios) de identificadores para hello recursos toomove.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Si desea que toomove Hola VM y su suscripción de recursos de tooa diferente, agregue hello **--destino subscriptionId &#60; destinationSubscriptionID &#62;** suscripción de destino de parámetro toospecify Hola.

Si está trabajando desde Hola símbolo del sistema en un equipo Windows, deberá tooadd un  **$**  delante de los nombres de variable de saludo al declararlas. Esto no es necesario en Linux.

Se le pide tooconfirm que desea toomove Hola el recurso especificado. Tipo de **Y** tooconfirm que desea que los recursos de hello toomove.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>Pasos siguientes
Puede mover muchos tipos diferentes de recursos entre suscripciones y grupos de recursos. Para obtener más información, consulte [Mover grupo de recursos de toonew de recursos o suscripción](../../resource-group-move-resources.md).    

