---
title: "aaaFind próximo salto con Monitor Azure red próximo salto - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "En este artículo se describe cómo puede encontrar qué Hola siguiente tipo de salto es y uso de dirección ip del próximo salto de mediante la CLI de Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a>Averiguar qué tipo de hello próximo salto es con capacidad de próximo salto de hello en Monitor de red de Azure mediante Azure CLI 2.0

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API de REST de Azure](network-watcher-check-next-hop-rest.md)

Próximo salto es una característica del Monitor de red que proporciona la capacidad de hello obtener tipo hello de próximo salto y la dirección IP basándose en una máquina virtual especificada. Esta característica es útil para determinar si el tráfico que sale de una máquina virtual recorre una puerta de enlace, internet o redes virtuales tooget tooits destino.

En este artículo usa la CLI de próxima generación para el modelo de implementación de administración de recursos hello, CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.

Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Antes de empezar

En este escenario, utilizará Hola tipo de próximo salto de CLI de Azure toofind hello y la dirección IP.

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red. escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo usa próximo salto, una característica de Monitor de red que se determina el tipo de próximo salto hello y dirección IP para un recurso. toolearn más información acerca de próximo salto, visite [información general sobre salto siguiente](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Obtención del próximo salto

llamamos a Hola de próximo salto tooget hello `az network watcher show-next-hop` cmdlet. Pasamos grupo de recursos de Monitor de red de hello cmdlet hello, hello NetworkWatcher, máquina virtual de Id., dirección IP de origen y dirección IP de destino. En este ejemplo, la dirección IP de destino de Hola es tooa máquina virtual en otra red virtual. Hay una puerta de enlace de red virtual entre las dos redes virtuales de Hola.

Si aún no lo ha aún, instalar y configurar hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login). A continuación, ejecute hello siguiente comando:

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
Si Hola máquina virtual tiene varios NIC y reenvío IP está habilitado en ninguno de hello NIC, a continuación, Hola parámetro NIC (-Id. de nic) debe especificarse. De lo contrario, es opcional.

## <a name="review-results"></a>Revisión de los resultados

Cuando haya finalizado, se proporcionan los resultados de Hola. se devuelve la dirección IP del próximo salto Hello, así como de tipo hello del recurso es.

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

Hello lista siguiente muestra valores de hello disponibles actualmente NextHopType:

**Tipo de próximo salto**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooreview la configuración del grupo de seguridad de red mediante programación si visita [NSG auditoría con Monitor de red](network-watcher-nsg-auditing-powershell.md)
