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
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="e6eaf-103">Solución de problemas de las conexiones y la puerta de enlace de Virtual Network mediante Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="e6eaf-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e6eaf-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e6eaf-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="e6eaf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6eaf-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="e6eaf-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e6eaf-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="e6eaf-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e6eaf-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="e6eaf-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="e6eaf-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="e6eaf-109">Monitor de red proporciona muchas de las capacidades en lo referente a toounderstanding los recursos de red en Azure.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="e6eaf-110">Una de estas funcionalidades es la solución de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="e6eaf-111">Solución de problemas de recursos se puede llamar a través del portal de hello, PowerShell, CLI o API de REST.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="e6eaf-112">Cuando se llama, Monitor de red inspecciona el estado de saludo de una puerta de enlace de red Virtual o una conexión y devuelve sus conclusiones.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="e6eaf-113">En este artículo le guiará por las tareas de administración diferente de Hola que están actualmente disponibles para solucionar problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="e6eaf-114">**Solución de problemas de una puerta de enlace de Virtual Network**</span><span class="sxs-lookup"><span data-stu-id="e6eaf-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="e6eaf-115">**Solución de problemas de una conexión**</span><span class="sxs-lookup"><span data-stu-id="e6eaf-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="e6eaf-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e6eaf-116">Before you begin</span></span>

<span data-ttu-id="e6eaf-117">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="e6eaf-118">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="e6eaf-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="e6eaf-119">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="e6eaf-120">Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="e6eaf-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="e6eaf-121">Información general</span><span class="sxs-lookup"><span data-stu-id="e6eaf-121">Overview</span></span>

<span data-ttu-id="e6eaf-122">Solución de problemas del Monitor de red proporciona la capacidad de hello solucionar los problemas que surgen con puertas de enlace de red Virtual y las conexiones.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="e6eaf-123">Cuando se realiza una solicitud de recursos de toohello solución de problemas, registros están consultando e inspeccionan.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="e6eaf-124">Una vez finalizada la inspección, se devuelven resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="e6eaf-125">Hola solucionar API solicitudes son largos de solicitudes, que pueden durar varias tooreturn minutos un resultado en ejecución.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="e6eaf-126">Los registros se almacenan en un contenedor en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="e6eaf-127">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="e6eaf-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="e6eaf-128">Solución de problemas de una puerta de enlace de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="e6eaf-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="e6eaf-129">Hola POST solucionar problemas de solicitud</span><span class="sxs-lookup"><span data-stu-id="e6eaf-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="e6eaf-130">Hola después de estado de Hola de las consultas de ejemplo de una puerta de enlace de red Virtual.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="e6eaf-131">Puesto que esta operación es larga ejecuta, Hola URI para consultar la operación de Hola y Hola URI para el resultado de hello se devuelve en el encabezado de respuesta de hello como se muestra en hello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="e6eaf-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="e6eaf-132">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="e6eaf-132">**Important Values**</span></span>

* <span data-ttu-id="e6eaf-133">**Azure AsyncOperation** -esta propiedad contiene Hola URI tooquery Hola Async solucionar problemas de operación</span><span class="sxs-lookup"><span data-stu-id="e6eaf-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="e6eaf-134">**Ubicación** -esta propiedad contiene Hola URI donde hello resultados no están cuando hello operación está completa</span><span class="sxs-lookup"><span data-stu-id="e6eaf-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="e6eaf-135">Operación asincrónica de hello para la finalización de la consulta</span><span class="sxs-lookup"><span data-stu-id="e6eaf-135">Query hello async operation for completion</span></span>

<span data-ttu-id="e6eaf-136">Utilice tooquery URI de las operaciones de hello para el progreso de operación de Hola Hola tal como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="e6eaf-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="e6eaf-137">Mientras está en curso la operación de hello, Hola respuesta muestra **InProgress** tal como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="e6eaf-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="e6eaf-138">Cuando operación hello es cambios de estado de hello completa demasiado**correcto**.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="e6eaf-139">Recuperar resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="e6eaf-139">Retrieve hello results</span></span>

<span data-ttu-id="e6eaf-140">Una vez que el estado de hello devuelto es **correcto**, llamar a un método GET en tooretrieve URI de resultado de la operación de hello resultados Hola.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="e6eaf-141">Hello respuestas siguientes son ejemplos de un degradado típico de respuesta devuelto al consultar los resultados de Hola de solución de problemas de una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="e6eaf-142">Vea [descripción de los resultados de hello](#understanding-the-results) tooget información más detallada sobre qué propiedades de hello en medio de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

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


## <a name="troubleshoot-connections"></a><span data-ttu-id="e6eaf-143">Solución de problemas de conexión</span><span class="sxs-lookup"><span data-stu-id="e6eaf-143">Troubleshoot Connections</span></span>

<span data-ttu-id="e6eaf-144">Hola después de estado de Hola de las consultas de ejemplo de una conexión.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-144">hello following example queries hello status of a Connection.</span></span>

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
> <span data-ttu-id="e6eaf-145">Hola solucionar problemas de operación no se puede ejecutar en paralelo en una conexión y sus puertas de enlace correspondientes.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="e6eaf-146">debe completar la operación de Hello toorunning anterior en el recurso de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="e6eaf-147">Puesto que se trata de una transacción de larga duración, en el encabezado de respuesta Hola Hola URI para consultar la operación de Hola y Hola URI para el resultado de hello se devuelve como se muestra en hello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="e6eaf-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="e6eaf-148">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="e6eaf-148">**Important Values**</span></span>

* <span data-ttu-id="e6eaf-149">**Azure AsyncOperation** -esta propiedad contiene Hola URI tooquery Hola Async solucionar problemas de operación</span><span class="sxs-lookup"><span data-stu-id="e6eaf-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="e6eaf-150">**Ubicación** -esta propiedad contiene Hola URI donde hello resultados no están cuando hello operación está completa</span><span class="sxs-lookup"><span data-stu-id="e6eaf-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="e6eaf-151">Operación asincrónica de hello para la finalización de la consulta</span><span class="sxs-lookup"><span data-stu-id="e6eaf-151">Query hello async operation for completion</span></span>

<span data-ttu-id="e6eaf-152">Utilice tooquery URI de las operaciones de hello para el progreso de operación de Hola Hola tal como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="e6eaf-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="e6eaf-153">Mientras está en curso la operación de hello, Hola respuesta muestra **InProgress** tal como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="e6eaf-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="e6eaf-154">Cuando se completa la operación de hello, también cambia el estado de hello**correcto**.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="e6eaf-155">Hello respuestas siguientes son ejemplos de una respuesta típica que se devuelve al consultar los resultados de Hola de solución de problemas de una conexión.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="e6eaf-156">Recuperar resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="e6eaf-156">Retrieve hello results</span></span>

<span data-ttu-id="e6eaf-157">Una vez que el estado de hello devuelto es **correcto**, llamar a un método GET en tooretrieve URI de resultado de la operación de hello resultados Hola.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="e6eaf-158">Hello respuestas siguientes son ejemplos de una respuesta típica que se devuelve al consultar los resultados de Hola de solución de problemas de una conexión.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="e6eaf-159">Descripción de los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="e6eaf-159">Understanding hello results</span></span>

<span data-ttu-id="e6eaf-160">texto de acción de Hello ofrece instrucciones generales sobre cómo tooresolve Hola problema.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="e6eaf-161">Si el problema de Hola se pueda realizar una acción, se proporciona un vínculo con instrucciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="e6eaf-162">En caso de hello donde no haya ninguna orientación adicional, respuesta de hello proporciona Hola url tooopen un caso de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="e6eaf-163">Para obtener más información acerca de las propiedades de Hola de respuesta de Hola y qué se incluye, visite [información general de solución de problemas del Monitor de red](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e6eaf-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="e6eaf-164">Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="e6eaf-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="e6eaf-165">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="e6eaf-166">Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="e6eaf-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6eaf-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6eaf-167">Next steps</span></span>

<span data-ttu-id="e6eaf-168">Si se cambiaron las configuraciones que detenga la conectividad de VPN, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que pueden estar en cuestión.</span><span class="sxs-lookup"><span data-stu-id="e6eaf-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
