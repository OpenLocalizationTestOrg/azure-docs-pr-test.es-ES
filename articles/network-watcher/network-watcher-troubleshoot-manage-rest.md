---
title: 'aaaTroubleshoot la puerta de enlace de red Virtual y las conexiones con el Monitor de red de Azure: REST | Documentos de Microsoft'
description: "Esta página explica cómo se REST tootroubleshoot puertas de enlace de red Virtual y las conexiones con el Monitor de red de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a>Solución de problemas de las conexiones y la puerta de enlace de Virtual Network mediante Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API DE REST](network-watcher-troubleshoot-manage-rest.md)

Monitor de red proporciona muchas de las capacidades en lo referente a toounderstanding los recursos de red en Azure. Una de estas funcionalidades es la solución de problemas de recursos. Solución de problemas de recursos se puede llamar a través del portal de hello, PowerShell, CLI o API de REST. Cuando se llama, Monitor de red inspecciona el estado de saludo de una puerta de enlace de red Virtual o una conexión y devuelve sus conclusiones.

En este artículo le guiará por las tareas de administración diferente de Hola que están actualmente disponibles para solucionar problemas de recursos.

- [**Solución de problemas de una puerta de enlace de Virtual Network**](#troubleshoot-a-virtual-network-gateway)
- [**Solución de problemas de una conexión**](#troubleshoot-connections)

## <a name="before-you-begin"></a>Antes de empezar

ARMclient es la API de REST de hello toocall utilizados mediante PowerShell. ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Información general

Solución de problemas del Monitor de red proporciona la capacidad de hello solucionar los problemas que surgen con puertas de enlace de red Virtual y las conexiones. Cuando se realiza una solicitud de recursos de toohello solución de problemas, registros están consultando e inspeccionan. Una vez finalizada la inspección, se devuelven resultados de Hola. Hola solucionar API solicitudes son largos de solicitudes, que pueden durar varias tooreturn minutos un resultado en ejecución. Los registros se almacenan en un contenedor en una cuenta de almacenamiento.

## <a name="log-in-with-armclient"></a>Inicio de sesión con ARMClient

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a>Solución de problemas de una puerta de enlace de Virtual Network


### <a name="post-hello-troubleshoot-request"></a>Hola POST solucionar problemas de solicitud

Hola después de estado de Hola de las consultas de ejemplo de una puerta de enlace de red Virtual.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

Puesto que esta operación es larga ejecuta, Hola URI para consultar la operación de Hola y Hola URI para el resultado de hello se devuelve en el encabezado de respuesta de hello como se muestra en hello después de respuesta:

**Valores importantes**

* **Azure AsyncOperation** -esta propiedad contiene Hola URI tooquery Hola Async solucionar problemas de operación
* **Ubicación** -esta propiedad contiene Hola URI donde hello resultados no están cuando hello operación está completa

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>Operación asincrónica de hello para la finalización de la consulta

Utilice tooquery URI de las operaciones de hello para el progreso de operación de Hola Hola tal como se muestra en el siguiente ejemplo de Hola:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Mientras está en curso la operación de hello, Hola respuesta muestra **InProgress** tal como se muestra en el siguiente ejemplo de Hola:

```json
{
  "status": "InProgress"
}
```

Cuando operación hello es cambios de estado de hello completa demasiado**correcto**.

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a>Recuperar resultados de Hola

Una vez que el estado de hello devuelto es **correcto**, llamar a un método GET en tooretrieve URI de resultado de la operación de hello resultados Hola.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Hello respuestas siguientes son ejemplos de un degradado típico de respuesta devuelto al consultar los resultados de Hola de solución de problemas de una puerta de enlace. Vea [descripción de los resultados de hello](#understanding-the-results) tooget información más detallada sobre qué propiedades de hello en medio de respuesta de Hola.

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a>Solución de problemas de conexión

Hola después de estado de Hola de las consultas de ejemplo de una conexión.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> Hola solucionar problemas de operación no se puede ejecutar en paralelo en una conexión y sus puertas de enlace correspondientes. debe completar la operación de Hello toorunning anterior en el recurso de hello anterior.

Puesto que se trata de una transacción de larga duración, en el encabezado de respuesta Hola Hola URI para consultar la operación de Hola y Hola URI para el resultado de hello se devuelve como se muestra en hello después de respuesta:

**Valores importantes**

* **Azure AsyncOperation** -esta propiedad contiene Hola URI tooquery Hola Async solucionar problemas de operación
* **Ubicación** -esta propiedad contiene Hola URI donde hello resultados no están cuando hello operación está completa

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>Operación asincrónica de hello para la finalización de la consulta

Utilice tooquery URI de las operaciones de hello para el progreso de operación de Hola Hola tal como se muestra en el siguiente ejemplo de Hola:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Mientras está en curso la operación de hello, Hola respuesta muestra **InProgress** tal como se muestra en el siguiente ejemplo de Hola:

```json
{
  "status": "InProgress"
}
```

Cuando se completa la operación de hello, también cambia el estado de hello**correcto**.

```json
{
  "status": "Succeeded"
}
```

Hello respuestas siguientes son ejemplos de una respuesta típica que se devuelve al consultar los resultados de Hola de solución de problemas de una conexión.

### <a name="retrieve-hello-results"></a>Recuperar resultados de Hola

Una vez que el estado de hello devuelto es **correcto**, llamar a un método GET en tooretrieve URI de resultado de la operación de hello resultados Hola.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Hello respuestas siguientes son ejemplos de una respuesta típica que se devuelve al consultar los resultados de Hola de solución de problemas de una conexión.

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a>Descripción de los resultados de Hola

texto de acción de Hello ofrece instrucciones generales sobre cómo tooresolve Hola problema. Si el problema de Hola se pueda realizar una acción, se proporciona un vínculo con instrucciones adicionales. En caso de hello donde no haya ninguna orientación adicional, respuesta de hello proporciona Hola url tooopen un caso de soporte técnico.  Para obtener más información acerca de las propiedades de Hola de respuesta de Hola y qué se incluye, visite [información general de solución de problemas del Monitor de red](network-watcher-troubleshoot-overview.md)

Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Otra herramienta que se puede utilizar es el Explorador de Storage. Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)

## <a name="next-steps"></a>Pasos siguientes

Si se cambiaron las configuraciones que detenga la conectividad de VPN, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que pueden estar en cuestión.
