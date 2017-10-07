---
title: conectividad de aaaCheck con Monitor de red de Azure - 2.0 de CLI de Azure | Documentos de Microsoft
description: "Esta página explica cómo comprobar la conectividad de toouse con Monitor de red mediante Azure CLI 2.0"
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
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="f4634-103">Comprobación de la conectividad con Azure Network Watcher usando la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f4634-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f4634-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4634-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="f4634-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f4634-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="f4634-106">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="f4634-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="f4634-107">Obtenga información acerca de cómo se puede establecer toouse conectividad tooverify si una conexión TCP directa de una tooa de máquina virtual tiene el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="f4634-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f4634-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f4634-108">Before you begin</span></span>

<span data-ttu-id="f4634-109">En este artículo se supone que tiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4634-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="f4634-110">Una instancia del Monitor de red en la región de Hola que desea toocheck conectividad.</span><span class="sxs-lookup"><span data-stu-id="f4634-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="f4634-111">Conectividad de toocheck de máquinas virtuales con.</span><span class="sxs-lookup"><span data-stu-id="f4634-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="f4634-112">La comprobación de conectividad requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="f4634-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="f4634-113">Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="f4634-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="f4634-114">Registrar capacidades de vista previa de Hola</span><span class="sxs-lookup"><span data-stu-id="f4634-114">Register hello preview capability</span></span> 

<span data-ttu-id="f4634-115">Comprobación de conectividad está actualmente en versión preliminar pública, toouse esta característica necesita toobe registrado.</span><span class="sxs-lookup"><span data-stu-id="f4634-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="f4634-116">toodo, Hola ejecución según muestra CLI</span><span class="sxs-lookup"><span data-stu-id="f4634-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="f4634-117">registro de hello tooverify fue correcto, ejecute el siguiente comando CLI de hello:</span><span class="sxs-lookup"><span data-stu-id="f4634-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="f4634-118">Si se ha registrado correctamente la característica de hello, salida de hello debe coincidir con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f4634-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="f4634-119">Compruebe la conectividad tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="f4634-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="f4634-120">Este ejemplo comprueba la máquina virtual de conectividad tooa destino en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="f4634-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="f4634-121">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4634-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="f4634-122">Response</span><span class="sxs-lookup"><span data-stu-id="f4634-122">Response</span></span>

<span data-ttu-id="f4634-123">Hola después de la respuesta es del anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4634-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="f4634-124">En esta respuesta, Hola `ConnectionStatus` es **inaccesible**.</span><span class="sxs-lookup"><span data-stu-id="f4634-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="f4634-125">Puede ver que Hola a todos los sondeos errores de envío.</span><span class="sxs-lookup"><span data-stu-id="f4634-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="f4634-126">no se pudo conectividad Hello en dispositivo virtual Hola due tooa configurada por el usuario `NetworkSecurityRule` denominado **UserRule_Port80**, configurado tooblock el tráfico entrante en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="f4634-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="f4634-127">Esta información puede ser problemas de conexión de tooresearch usado.</span><span class="sxs-lookup"><span data-stu-id="f4634-127">This information can be used tooresearch connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="f4634-128">Problemas de validación de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="f4634-128">Validate routing issues</span></span>

<span data-ttu-id="f4634-129">ejemplo de Hola comprueba la conectividad entre una máquina virtual y un extremo remoto.</span><span class="sxs-lookup"><span data-stu-id="f4634-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="f4634-130">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4634-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="f4634-131">Response</span><span class="sxs-lookup"><span data-stu-id="f4634-131">Response</span></span>

<span data-ttu-id="f4634-132">En el siguiente ejemplo de Hola Hola `connectionStatus` se muestra como **inaccesible**.</span><span class="sxs-lookup"><span data-stu-id="f4634-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="f4634-133">Hola `hops` obtener más información, consulte en `issues` que se bloqueó el tráfico de hello due tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="f4634-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="f4634-134">Comprobación de la latencia del sitio web</span><span class="sxs-lookup"><span data-stu-id="f4634-134">Check website latency</span></span>

<span data-ttu-id="f4634-135">Hello en el ejemplo siguiente se busca en hello conectividad tooa sitio Web.</span><span class="sxs-lookup"><span data-stu-id="f4634-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="f4634-136">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4634-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="f4634-137">Response</span><span class="sxs-lookup"><span data-stu-id="f4634-137">Response</span></span>

<span data-ttu-id="f4634-138">Hola después de respuesta, puede ver hello `connectionStatus` se muestra como **alcanzable**.</span><span class="sxs-lookup"><span data-stu-id="f4634-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="f4634-139">Cuando una conexión se establece correctamente, se proporcionan los valores de latencia.</span><span class="sxs-lookup"><span data-stu-id="f4634-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="f4634-140">Compruebe el punto de conexión de almacenamiento de tooa de conectividad</span><span class="sxs-lookup"><span data-stu-id="f4634-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="f4634-141">Hello en el ejemplo siguiente se comprueba la conectividad Hola desde una cuenta de almacenamiento de máquina virtual tooa blog.</span><span class="sxs-lookup"><span data-stu-id="f4634-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="f4634-142">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4634-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="f4634-143">Response</span><span class="sxs-lookup"><span data-stu-id="f4634-143">Response</span></span>

<span data-ttu-id="f4634-144">Hola siguiente json es respuesta de ejemplo de Hola de ejecución del cmdlet anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="f4634-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="f4634-145">Hola como Hola comprobación es correcta, `connectionStatus` propiedad se muestra como **alcanzable**.</span><span class="sxs-lookup"><span data-stu-id="f4634-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="f4634-146">Se proporcionan detalles de hello sobre Hola número de saltos necesarios tooreach Hola almacenamiento de blobs y la latencia.</span><span class="sxs-lookup"><span data-stu-id="f4634-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="f4634-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4634-147">Next steps</span></span>

<span data-ttu-id="f4634-148">Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="f4634-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="f4634-149">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f4634-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
