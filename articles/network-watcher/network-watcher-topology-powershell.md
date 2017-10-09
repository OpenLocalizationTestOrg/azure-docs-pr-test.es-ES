---
title: "topología de Monitor de red de Azure aaaView - PowerShell | Documentos de Microsoft"
description: "En este artículo se describe cómo toouse PowerShell tooquery la topología de red."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a>Visualización de la topología de Network Watcher con PowerShell

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

En este escenario, utilice hello `Get-AzureRmNetworkWatcherTopology` información de la topología de cmdlet tooretrieve Hola. También hay un artículo sobre cómo demasiado[recuperar la topología de red con la API de REST](network-watcher-topology-rest.md).

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo recupera la respuesta de la topología de Hola para un determinado grupo de recursos.

## <a name="retrieve-network-watcher"></a>Recuperación de Network Watcher

Hola primer paso es instancia de Monitor de red de tooretrieve Hola. Hola `$networkWatcher` pasa una variable toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a>Recuperación de la topología

Hola `Get-AzureRmNetworkWatcherTopology` cmdlet recupera la topología de Hola para un grupo de recursos determinado.

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a>Results

Hello resultados devueltos tienen una propiedad nombre "recursos", que contiene el cuerpo de respuesta json de Hola para hello `Get-AzureRmNetworkWatcherTopology` cmdlet.  respuesta de Hello contiene recursos de hello en hello grupo de seguridad de red y sus asociaciones (es decir, Contains, asociados).

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


