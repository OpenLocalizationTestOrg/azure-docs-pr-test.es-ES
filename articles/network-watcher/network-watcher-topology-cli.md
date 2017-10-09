---
title: "topología de Monitor de red de Azure aaaView - CLI de Azure | Documentos de Microsoft"
description: "En este artículo se describe cómo toouse CLI de Azure tooquery la topología de red."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a>Visualización de la topología de Network Watcher con la CLI de Azure

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [API DE REST](network-watcher-topology-rest.md)

característica de topología de Hola de Monitor de red proporciona una representación visual de los recursos de red de hello en una suscripción. En el portal de hello, esta visualización se presenta tooyou automáticamente. puede recuperar la información de Hello detrás de la vista de topología de hello en el portal de Hola a través de PowerShell.
Esta capacidad hace que la información de la topología de hello sea más versátil como datos de hello pueden utilizarse otro toobuild herramientas out visualización Hola.

En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux. Network Watcher usa actualmente Azure CLI 1.0 para la compatibilidad con CLI.

interconexión de Hola se modela en dos relaciones.

- **Contención**: por ejemplo, una red virtual contiene una subred que incluye una NIC.
- **Asociación**: por ejemplo, la NIC está asociada a una máquina virtual.

Hello lista siguiente es propiedades que se devuelven cuando se consultan Hola API de REST de topología.

* **nombre** : hello nombre de recurso de Hola
* **Id. de** -Hola uri del recurso de Hola.
* **ubicación** -Hola ubicación donde existe el recurso de Hola.
* **las asociaciones** -una lista de asociaciones toohello al que hace referencia el objeto.
    * **nombre de** -nombre de Hola de hello hace referencia a recursos.
    * **resourceId** -Hola resourceId es Hola uri del recurso de hello hace referencia en la asociación de Hola.
    * **associationType** -relación Hola entre Hola secundario y primario de hello hace referencia a este valor. Los valores válidos son **Contains** o **Associated**.

## <a name="before-you-begin"></a>Antes de empezar

En este escenario, utilice hello `network watcher topology` información de la topología de cmdlet tooretrieve Hola. También hay un artículo sobre cómo demasiado[recuperar la topología de red con la API de REST](network-watcher-topology-rest.md).

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo recupera la respuesta de la topología de Hola para un determinado grupo de recursos.

## <a name="retrieve-topology"></a>Recuperación de la topología

Hola `network watcher topology` cmdlet recupera la topología de Hola para un grupo de recursos determinado. Agregue el argumento de Hola "--json" tooview hello oput en formato json

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>Results

Hello resultados devueltos tienen una propiedad nombre "recursos", que contiene el cuerpo de respuesta json de Hola para hello `network watcher topology` cmdlet.  respuesta de Hello contiene recursos de hello en hello grupo de seguridad de red y sus asociaciones (es decir, Contains, asociados).

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>Pasos siguientes

Obtener más información sobre las reglas de seguridad de Hola que son los recursos de red aplicada tooyour visitando [información general de la vista de grupo de seguridad](network-watcher-security-group-view-overview.md)
