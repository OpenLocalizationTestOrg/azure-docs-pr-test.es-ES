---
title: 'conectividad de aaaCheck con Monitor de red de Azure: portal de Azure | Documentos de Microsoft'
description: "Esta página explica cómo toocheck conectividad con Monitor de red en Hola portal de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="9d7b6-103">Compruebe la conectividad con el Monitor de red de Azure con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9d7b6-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9d7b6-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9d7b6-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="9d7b6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d7b6-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="9d7b6-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9d7b6-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="9d7b6-107">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="9d7b6-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="9d7b6-108">Obtenga información acerca de cómo se puede establecer toouse conectividad tooverify si una conexión TCP directa de una tooa de máquina virtual tiene el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9d7b6-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9d7b6-109">Before you begin</span></span>

<span data-ttu-id="9d7b6-110">En este artículo se supone que tiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="9d7b6-111">Una instancia del Monitor de red en la región de Hola que desea toocheck conectividad.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="9d7b6-112">Conectividad de toocheck de máquinas virtuales con.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="9d7b6-113">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="9d7b6-114">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="9d7b6-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="9d7b6-115">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="9d7b6-116">La comprobación de conectividad requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="9d7b6-117">Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="9d7b6-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="9d7b6-118">Registrar capacidades de vista previa de Hola</span><span class="sxs-lookup"><span data-stu-id="9d7b6-118">Register hello preview capability</span></span>

<span data-ttu-id="9d7b6-119">Comprobación de conectividad está actualmente en versión preliminar pública, toouse esta característica necesita toobe registrado.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="9d7b6-120">toodo, ejecución Hola siguiendo el ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="9d7b6-121">registro de hello tooverify fue correcto, ejecute hello siguiendo el ejemplo de Powershell:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="9d7b6-122">Si se ha registrado correctamente la característica de hello, salida de hello debe coincidir con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="9d7b6-123">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="9d7b6-123">Log in with ARMClient</span></span>

<span data-ttu-id="9d7b6-124">Inicie sesión en tooarmclient con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="9d7b6-125">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9d7b6-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="9d7b6-126">Ejecutar Hola después tooreturn de secuencia de comandos en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="9d7b6-127">Esta información es necesaria para ejecutar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="9d7b6-128">Hola después el código necesita valores para hello siguientes variables:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="9d7b6-129">**Id. de suscripción** -Hola toouse de Id. de suscripción.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="9d7b6-130">**resourceGroupName** : hello nombre de un grupo de recursos que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="9d7b6-131">Desde siguiente Hola resultado, Id. de Hola de máquina virtual de Hola se usa en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="9d7b6-132">Compruebe la conectividad tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="9d7b6-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="9d7b6-133">Este ejemplo comprueba la máquina virtual de conectividad tooa destino en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="9d7b6-134">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9d7b6-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="9d7b6-135">Puesto que esta operación es larga ejecutando, Hola URI para el resultado de hello se devuelve en el encabezado de respuesta de hello tal como se muestra en hello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="9d7b6-136">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="9d7b6-136">**Important Values**</span></span>

* <span data-ttu-id="9d7b6-137">**Ubicación** -esta propiedad contiene Hola URI donde hello resultados no están cuando hello operación está completa</span><span class="sxs-lookup"><span data-stu-id="9d7b6-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="9d7b6-138">Response</span><span class="sxs-lookup"><span data-stu-id="9d7b6-138">Response</span></span>

<span data-ttu-id="9d7b6-139">Hola después de la respuesta es del anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="9d7b6-140">En esta respuesta, Hola `ConnectionStatus` es **inaccesible**.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="9d7b6-141">Puede ver que Hola a todos los sondeos errores de envío.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="9d7b6-142">no se pudo conectividad Hello en dispositivo virtual Hola due tooa configurada por el usuario `NetworkSecurityRule` denominado **UserRule_Port80**, configurado tooblock el tráfico entrante en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="9d7b6-143">Esta información puede ser problemas de conexión de tooresearch usado.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-143">This information can be used tooresearch connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="9d7b6-144">Problemas de validación de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="9d7b6-144">Validate routing issues</span></span>

<span data-ttu-id="9d7b6-145">ejemplo de Hola comprueba la conectividad entre una máquina virtual y un extremo remoto.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="9d7b6-146">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9d7b6-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="9d7b6-147">Puesto que esta operación es larga ejecutando, Hola URI para el resultado de hello se devuelve en el encabezado de respuesta de hello tal como se muestra en hello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="9d7b6-148">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="9d7b6-148">**Important Values**</span></span>

* <span data-ttu-id="9d7b6-149">**Ubicación** -esta propiedad contiene Hola URI donde hello resultados no están cuando hello operación está completa</span><span class="sxs-lookup"><span data-stu-id="9d7b6-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="9d7b6-150">Response</span><span class="sxs-lookup"><span data-stu-id="9d7b6-150">Response</span></span>

<span data-ttu-id="9d7b6-151">En el siguiente ejemplo de Hola Hola `connectionStatus` se muestra como **inaccesible**.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="9d7b6-152">Hola `hops` obtener más información, consulte en `issues` que se bloqueó el tráfico de hello due tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="9d7b6-153">Comprobación de la latencia del sitio web</span><span class="sxs-lookup"><span data-stu-id="9d7b6-153">Check website latency</span></span>

<span data-ttu-id="9d7b6-154">Hello en el ejemplo siguiente se busca en hello conectividad tooa sitio Web.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="9d7b6-155">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9d7b6-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="9d7b6-156">Puesto que esta operación es larga ejecutando, Hola URI para el resultado de hello se devuelve en el encabezado de respuesta de hello tal como se muestra en hello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="9d7b6-157">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="9d7b6-157">**Important Values**</span></span>

* <span data-ttu-id="9d7b6-158">**Ubicación** -esta propiedad contiene Hola URI donde hello resultados no están cuando hello operación está completa</span><span class="sxs-lookup"><span data-stu-id="9d7b6-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="9d7b6-159">Response</span><span class="sxs-lookup"><span data-stu-id="9d7b6-159">Response</span></span>

<span data-ttu-id="9d7b6-160">Hola después de respuesta, puede ver hello `connectionStatus` se muestra como **alcanzable**.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="9d7b6-161">Cuando una conexión se establece correctamente, se proporcionan los valores de latencia.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="9d7b6-162">Compruebe el punto de conexión de almacenamiento de tooa de conectividad</span><span class="sxs-lookup"><span data-stu-id="9d7b6-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="9d7b6-163">Hello en el ejemplo siguiente se comprueba la conectividad Hola desde una cuenta de almacenamiento de máquina virtual tooa blog.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="9d7b6-164">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9d7b6-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="9d7b6-165">Puesto que esta operación es larga ejecutando, Hola URI para el resultado de hello se devuelve en el encabezado de respuesta de hello tal como se muestra en hello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="9d7b6-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="9d7b6-166">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="9d7b6-166">**Important Values**</span></span>

* <span data-ttu-id="9d7b6-167">**Ubicación** -esta propiedad contiene Hola URI donde hello resultados no están cuando hello operación está completa</span><span class="sxs-lookup"><span data-stu-id="9d7b6-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="9d7b6-168">Response</span><span class="sxs-lookup"><span data-stu-id="9d7b6-168">Response</span></span>

<span data-ttu-id="9d7b6-169">Hello en el ejemplo siguiente se es respuesta Hola ejecutaran llamada de API de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="9d7b6-170">Hola como Hola comprobación es correcta, `connectionStatus` propiedad se muestra como **alcanzable**.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="9d7b6-171">Se proporcionan detalles de hello sobre Hola número de saltos necesarios tooreach Hola almacenamiento de blobs y la latencia.</span><span class="sxs-lookup"><span data-stu-id="9d7b6-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="9d7b6-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d7b6-172">Next steps</span></span>

<span data-ttu-id="9d7b6-173">Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="9d7b6-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="9d7b6-174">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9d7b6-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














