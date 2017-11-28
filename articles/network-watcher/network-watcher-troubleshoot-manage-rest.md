---
title: "Solución de problemas de las conexiones y la puerta de enlace de Virtual Network mediante Azure Network Watcher: REST | Microsoft Docs"
description: "Esta página explica cómo solucionar problemas de las conexiones y las puertas de enlace de Virtual Network con Azure Network Watcher usando REST"
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
ms.openlocfilehash: bc61be74d85a309c158716460b918baaf4fa94dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="5f8d0-103">Solución de problemas de las conexiones y la puerta de enlace de Virtual Network mediante Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="5f8d0-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5f8d0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5f8d0-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="5f8d0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f8d0-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="5f8d0-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5f8d0-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="5f8d0-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5f8d0-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="5f8d0-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="5f8d0-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="5f8d0-109">Network Watcher proporciona numerosas funcionalidades con relación a los recursos de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="5f8d0-110">Una de estas funcionalidades es la solución de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="5f8d0-111">Se puede llamar a la solución de problemas de recursos mediante el portal, PowerShell, la CLI o la API de REST.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="5f8d0-112">Cuando se llama a Network Watcher, este inspecciona el estado de una puerta de enlace de Virtual Network o de una conexión y devuelve sus conclusiones.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="5f8d0-113">Este artículo le guiará por las diferentes tareas de administración que están actualmente disponibles para la solución de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-113">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="5f8d0-114">**Solución de problemas de una puerta de enlace de Virtual Network**</span><span class="sxs-lookup"><span data-stu-id="5f8d0-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="5f8d0-115">**Solución de problemas de una conexión**</span><span class="sxs-lookup"><span data-stu-id="5f8d0-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="5f8d0-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="5f8d0-116">Before you begin</span></span>

<span data-ttu-id="5f8d0-117">ARMclient se usa para llamar a la API de REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-117">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="5f8d0-118">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="5f8d0-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="5f8d0-119">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-119">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="5f8d0-120">Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="5f8d0-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="5f8d0-121">Información general</span><span class="sxs-lookup"><span data-stu-id="5f8d0-121">Overview</span></span>

<span data-ttu-id="5f8d0-122">La solución de problemas de Network Watcher permite solucionar los problemas que surgen con las puertas de enlace de Virtual Network y las conexiones.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-122">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="5f8d0-123">Cuando se envía una solicitud para solucionar problemas de recursos, se consultan y se inspeccionan los registros.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-123">When a request is made to the resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="5f8d0-124">Una vez finalizada la inspección, se devuelven los resultados.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-124">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="5f8d0-125">Las solicitudes de la API para solucionar problemas son de larga ejecución, y podrían tardar varios minutos en devolver un resultado.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-125">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="5f8d0-126">Los registros se almacenan en un contenedor en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="5f8d0-127">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="5f8d0-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="5f8d0-128">Solución de problemas de una puerta de enlace de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="5f8d0-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-the-troubleshoot-request"></a><span data-ttu-id="5f8d0-129">REGISTRO de la solicitud de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5f8d0-129">POST the troubleshoot request</span></span>

<span data-ttu-id="5f8d0-130">En el ejemplo siguiente se consulta el estado de una puerta de enlace de Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-130">The following example queries the status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="5f8d0-131">Puesto que esta operación es de larga ejecución, el URI para consultar la operación y el URI para el resultado se devuelven en el encabezado de respuesta como se muestra en la siguiente respuesta:</span><span class="sxs-lookup"><span data-stu-id="5f8d0-131">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="5f8d0-132">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="5f8d0-132">**Important Values**</span></span>

* <span data-ttu-id="5f8d0-133">**Azure AsyncOperation**: esta propiedad contiene el URI para consultar la operación asincrónica de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5f8d0-133">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="5f8d0-134">**Ubicación**: esta propiedad contiene el URI donde se encuentran los resultados una vez completada la operación</span><span class="sxs-lookup"><span data-stu-id="5f8d0-134">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="5f8d0-135">Consulta del estado acabado de la operación asincrónica</span><span class="sxs-lookup"><span data-stu-id="5f8d0-135">Query the async operation for completion</span></span>

<span data-ttu-id="5f8d0-136">Utilice las operaciones de URI para consultar el progreso de la operación tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5f8d0-136">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="5f8d0-137">Mientras la operación está en curso, se muestra la respuesta **InProgress**, tal como se ven en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5f8d0-137">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="5f8d0-138">Una vez completada la operación, el estado cambia a **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-138">When the operation is complete the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-the-results"></a><span data-ttu-id="5f8d0-139">Recuperación de los resultados</span><span class="sxs-lookup"><span data-stu-id="5f8d0-139">Retrieve the results</span></span>

<span data-ttu-id="5f8d0-140">Una vez que el estado devuelto es **Succeeded**, llame a un método GET en el URI operationResult para recuperar los resultados de la operación.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-140">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="5f8d0-141">Las respuestas siguientes son ejemplos de un típica respuesta degradada devuelta al consultar los resultados de la solución de problemas de una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-141">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span></span> <span data-ttu-id="5f8d0-142">Consulte [Descripción de los resultados](#understanding-the-results) para obtener información más detallada sobre lo que significan las propiedades en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-142">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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


## <a name="troubleshoot-connections"></a><span data-ttu-id="5f8d0-143">Solución de problemas de conexión</span><span class="sxs-lookup"><span data-stu-id="5f8d0-143">Troubleshoot Connections</span></span>

<span data-ttu-id="5f8d0-144">En el ejemplo siguiente se consulta el estado de una conexión.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-144">The following example queries the status of a Connection.</span></span>

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
> <span data-ttu-id="5f8d0-145">La operación de solución de problemas no se puede ejecutar en paralelo en una conexión y sus puertas de enlace correspondientes.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-145">The troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="5f8d0-146">La operación tiene que completarse antes de ejecutarla en el recurso anterior.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-146">The operation must complete prior to running it on the previous resource.</span></span>

<span data-ttu-id="5f8d0-147">Puesto que esta es una transacción de larga ejecución, en el encabezado de respuesta, el URI para consultar la operación y el URI para el resultado se devuelven como se muestra en la siguiente respuesta:</span><span class="sxs-lookup"><span data-stu-id="5f8d0-147">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span></span>

<span data-ttu-id="5f8d0-148">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="5f8d0-148">**Important Values**</span></span>

* <span data-ttu-id="5f8d0-149">**Azure AsyncOperation**: esta propiedad contiene el URI para consultar la operación asincrónica de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5f8d0-149">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="5f8d0-150">**Ubicación**: esta propiedad contiene el URI donde se encuentran los resultados una vez completada la operación</span><span class="sxs-lookup"><span data-stu-id="5f8d0-150">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="5f8d0-151">Consulta del estado acabado de la operación asincrónica</span><span class="sxs-lookup"><span data-stu-id="5f8d0-151">Query the async operation for completion</span></span>

<span data-ttu-id="5f8d0-152">Utilice las operaciones de URI para consultar el progreso de la operación tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5f8d0-152">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="5f8d0-153">Mientras la operación está en curso, se muestra la respuesta **InProgress**, tal como se ven en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5f8d0-153">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="5f8d0-154">Una vez completada la operación, el estado cambia a **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-154">When the operation is complete, the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="5f8d0-155">Las respuestas siguientes son ejemplos de un típica respuesta devuelta al consultar los resultados de la solución de problemas de una conexión.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

### <a name="retrieve-the-results"></a><span data-ttu-id="5f8d0-156">Recuperación de los resultados</span><span class="sxs-lookup"><span data-stu-id="5f8d0-156">Retrieve the results</span></span>

<span data-ttu-id="5f8d0-157">Una vez que el estado devuelto es **Succeeded**, llame a un método GET en el URI operationResult para recuperar los resultados de la operación.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-157">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="5f8d0-158">Las respuestas siguientes son ejemplos de un típica respuesta devuelta al consultar los resultados de la solución de problemas de una conexión.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-158">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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

## <a name="understanding-the-results"></a><span data-ttu-id="5f8d0-159">Descripción de los resultados</span><span class="sxs-lookup"><span data-stu-id="5f8d0-159">Understanding the results</span></span>

<span data-ttu-id="5f8d0-160">El texto de la acción ofrece instrucciones generales sobre cómo resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-160">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="5f8d0-161">Si se puede realizar una acción para el problema, se proporciona un vínculo con instrucciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-161">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="5f8d0-162">Si no hay instrucciones adicionales, la respuesta proporciona la dirección URL para abrir un caso de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-162">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="5f8d0-163">Para más información acerca de las propiedades de la respuesta y lo que incluye, consulte la [introducción a la solución de problemas en Network Watcher](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5f8d0-163">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="5f8d0-164">Para más instrucciones acerca de cómo descargar archivos desde cuentas de Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="5f8d0-164">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="5f8d0-165">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="5f8d0-166">Encontrará más información acerca del Explorador de Storage en el siguiente vínculo: [Explorador de Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="5f8d0-166">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f8d0-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5f8d0-167">Next steps</span></span>

<span data-ttu-id="5f8d0-168">Si se cambió la configuración y la conectividad de VPN se ha detenido, consulte [Administración de grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para realizar un seguimiento de los grupos de seguridad de red y las reglas de seguridad que pueden estar afectados.</span><span class="sxs-lookup"><span data-stu-id="5f8d0-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
