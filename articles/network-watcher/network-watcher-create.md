---
title: "Creación de una instancia de Azure Network Watcher | Microsoft Docs"
description: "En esta página se proporcionan los pasos necesarios para crear una instancia de Network Watcher mediante el portal y la API de REST de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2aeaffdd5ab552e18677cbd1a24a748dd14bf172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Creación de una instancia de Azure Network Watcher

Network Watcher es un servicio regional que permite supervisar y diagnosticar problemas en un nivel de escenario de red mediante Azure. La supervisión del nivel de escenario permite diagnosticar problemas en una vista de nivel de red de un extremo a otro. Las herramientas de visualización y diagnóstico de red que incluye Network Watcher le ayudan a conocer, diagnosticar y obtener información acerca de cualquier red de Azure.

> [!NOTE]
> Debido a que, por el momento, Network Watcher solo es compatible con CLI 1.0, las instrucciones para crear una nueva instancia de Network Watcher son las mismas que para CLI 1.0.

## <a name="create-a-network-watcher-in-the-portal"></a>Creación de una instancia de Network Watcher en el portal

Navegue a **Más servicios** > **Redes** > **Network Watcher**. Puede seleccionar todas las suscripciones para las que desee habilitar Network Watcher. Esta acción crea una instancia de Network Watcher en todas las regiones que estén disponibles.

![crear una instancia de network watcher][1]

Cuando habilita Network Watcher mediante el Portal, el nombre de la instancia de Network Watcher se establecerá automáticamente en Network_region_name, donde region_name corresponde a la región de Azure donde se habilitó la instancia.  Por ejemplo, una instancia de Network Watcher habilitada en la región Centro occidental de EE. UU. se denominará NetworkWatcher_westcentralus

Además, la instancia de Network Watcher se agregará automáticamente a un grupo de recursos llamado NetworkWatcherRG.  Se creará este grupo de recursos si todavía no existe.

Si desea personalizar el nombre de una instancia de Network Watcher y el grupo de recursos en que se encuentra, puede usar PowerShell, la API de REST o los métodos de ARMClient que se describen a continuación.  En cada opción, el grupo de recursos debe existir antes de que ubique Network Watcher ahí.  

## <a name="create-a-network-watcher-with-powershell"></a>Creación de una instancia de Network Watcher con PowerShell

Para crear una instancia de Network Watcher, ejecute el siguiente ejemplo:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a>Creación de una instancia de Network Watcher con la API de REST

ARMclient se usa para llamar a la API de REST con PowerShell. ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)

### <a name="log-in-with-armclient"></a>Inicio de sesión con ARMClient

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a>Creación de Network Watcher

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene una instancia de Network Watcher, obtenga información acerca de las características disponibles:

* [Topología](network-watcher-topology-overview.md)
* [Captura de paquetes](network-watcher-packet-capture-overview.md)
* [Comprobación de flujo de IP](network-watcher-ip-flow-verify-overview.md)
* [Próximo salto](network-watcher-next-hop-overview.md)
* [Vista de grupo de seguridad](network-watcher-security-group-view-overview.md)
* [Registro de flujo de NSG](network-watcher-nsg-flow-logging-overview.md)
* [Solución de problemas de una puerta de enlace de Virtual Network](network-watcher-troubleshoot-overview.md)

Una vez creada una instancia de Network Watcher, para configurar la captura de paquetes vea el artículo [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md) (Crear una captura de paquetes desencadenada por alertas).

[1]: ./media/network-watcher-create/figure1.png











