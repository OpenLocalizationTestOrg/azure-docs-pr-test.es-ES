---
title: "topología de Monitor de red de Azure aaaView: API de REST | Documentos de Microsoft"
description: "En este artículo se describe cómo toouse REST API tooquery la topología de red."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>Visualización de la topología de Network Watcher con la API de REST

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [API DE REST](network-watcher-topology-rest.md)

característica de topología de Hola de Monitor de red proporciona una representación visual de los recursos de red de hello en una suscripción. En el portal de hello, esta visualización se presenta tooyou automáticamente. puede recuperar la información de Hello detrás de la vista de topología de hello en el portal de Hola a través de PowerShell.
Esta capacidad hace que la información de la topología de hello sea más versátil como datos de hello pueden utilizarse otro toobuild herramientas out visualización Hola.

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

En este escenario, recupera la información de topología de Hola. ARMclient es la API de REST de hello toocall utilizados mediante PowerShell. ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo recupera la respuesta de la topología de Hola para un determinado grupo de recursos.

## <a name="log-in-with-armclient"></a>Inicio de sesión con ARMClient

Inicie sesión en tooarmclient con sus credenciales de Azure.

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>Recuperación de la topología

Hola siguiendo el ejemplo de topología de hello las solicitudes de hello API de REST.  ejemplo de Hola es tooallow con parámetros para flexibilidad en la creación de un ejemplo.  Reemplace todos los valores dentro de \< \>.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

Hola después de la respuesta es un ejemplo de una respuesta reducida que se devuelve cuando recuperar topología para un grupo de recursos:

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

