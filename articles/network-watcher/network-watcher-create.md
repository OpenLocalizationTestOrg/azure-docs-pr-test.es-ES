---
title: aaaCreate una instancia del Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona Hola pasos toocreate una instancia del Monitor de red mediante el portal de Hola y la API de REST de Azure"
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
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Creación de una instancia de Azure Network Watcher

Monitor de red es un servicio regional que permite toomonitor y diagnosticar condiciones en un nivel de escenario de red, hacia y desde Azure. Supervisión del nivel de escenario permite toodiagnose problemas en una vista de nivel de red de tooend final. Diagnóstico de red y herramientas de visualización disponibles con Monitor de red ayudan a comprender, diagnosticar y obtener red tooyour de visión en Azure.

> [!NOTE]
> Monitor de red actualmente solo admite CLI 1.0, Hola instrucciones toocreate una nueva instancia de Monitor de red se proporciona para CLI 1.0.

## <a name="create-a-network-watcher-in-hello-portal"></a>Crear un monitor de red en el portal de Hola

Navegue demasiado**más servicios** > **red** > **Monitor de red**. Puede seleccionar todas las suscripciones de hello desea tooenable Monitor de red para. Esta acción crea una instancia de Network Watcher en todas las regiones que estén disponibles.

![crear una instancia de network watcher][1]

Cuando se habilita el Monitor de red mediante el Portal de Hola, nombre de Hola de instancia de Monitor de red de hello establecerá automáticamente tooNetworkWatcher_region_name donde region_name corresponde toohello región de Azure donde se habilitó la instancia de Hola.  Por ejemplo, una instancia de Network Watcher habilitada en la región Centro occidental de EE. UU. se denominará NetworkWatcher_westcentralus

Además, la instancia de Monitor de red de Hola se agregará automáticamente en un grupo de recursos denominado NetworkWatcherRG.  Se creará este grupo de recursos si todavía no existe.

Si desea que el nombre de hello toocustomize de una instancia del Monitor de red y Hola grupo de recursos se ha colocado en, puede usar métodos de Powershell, API de REST de Hola o ARMClient que se describe a continuación.  En cada opción, Hola grupo de recursos debe existir antes de colocar Hola Monitor de red en él.  

## <a name="create-a-network-watcher-with-powershell"></a>Creación de una instancia de Network Watcher con PowerShell

una instancia del Monitor de red, ejecute el siguiente ejemplo de Hola toocreate:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>Crear un monitor de red con hello API de REST

ARMclient es la API de REST de hello toocall utilizados mediante PowerShell. ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)

### <a name="log-in-with-armclient"></a>Inicio de sesión con ARMClient

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>Crear Monitor de red de Hola

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

Ahora que tiene una instancia del Monitor de red, obtener información acerca de las características de hello disponibles:

* [Topología](network-watcher-topology-overview.md)
* [Captura de paquetes](network-watcher-packet-capture-overview.md)
* [Comprobación de flujo de IP](network-watcher-ip-flow-verify-overview.md)
* [Próximo salto](network-watcher-next-hop-overview.md)
* [Vista de grupo de seguridad](network-watcher-security-group-view-overview.md)
* [Registro de flujo de NSG](network-watcher-nsg-flow-logging-overview.md)
* [Solución de problemas de una puerta de enlace de Virtual Network](network-watcher-troubleshoot-overview.md)

Una vez creada una instancia del Monitor de red, captura de paquete puede configurarse mediante el siguiente artículo de hello: [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











