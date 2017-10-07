---
title: "aaaFind próximo salto con Azure red Monitor de próximo salto - REST | Documentos de Microsoft"
description: "En este artículo se describe cómo puede ver qué Hola siguiente tipo de salto es y dirección ip mediante el uso de salto siguiente Hola API de REST de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="8a608-103">Averiguar qué tipo de hello próximo salto es con capacidad de próximo salto de hello en Monitor de red de Azure mediante la API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="8a608-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8a608-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8a608-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="8a608-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a608-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="8a608-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8a608-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="8a608-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8a608-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="8a608-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="8a608-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="8a608-109">Próximo salto es una característica del Monitor de red que proporciona la capacidad de hello obtener tipo hello de próximo salto y la dirección IP basándose en una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="8a608-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="8a608-110">Esta capacidad es útil para determinar si el tráfico que sale de una máquina virtual recorre una puerta de enlace, internet o redes virtuales tooget tooits destino.</span><span class="sxs-lookup"><span data-stu-id="8a608-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a608-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8a608-111">Before you begin</span></span>

<span data-ttu-id="8a608-112">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a608-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="8a608-113">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="8a608-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="8a608-114">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="8a608-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="8a608-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="8a608-115">Scenario</span></span>

<span data-ttu-id="8a608-116">escenario de Hello descrito en este artículo usa próximo salto, una característica de Monitor de red que se determina el tipo de próximo salto hello y dirección IP para un recurso.</span><span class="sxs-lookup"><span data-stu-id="8a608-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="8a608-117">toolearn más información acerca de próximo salto, visite [información general sobre salto siguiente](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a608-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="8a608-118">En este escenario va a:</span><span class="sxs-lookup"><span data-stu-id="8a608-118">In this scenario, you will:</span></span>

* <span data-ttu-id="8a608-119">Recuperar próximo salto Hola para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8a608-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="8a608-120">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="8a608-120">Log in with ARMClient</span></span>

<span data-ttu-id="8a608-121">Inicie sesión en tooarmclient con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="8a608-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="8a608-122">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8a608-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="8a608-123">Ejecutar Hola después tooreturn de secuencia de comandos en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8a608-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="8a608-124">Esta información es necesaria para ejecutar el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="8a608-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="8a608-125">Hola después el código necesita valores para hello siguientes variables:</span><span class="sxs-lookup"><span data-stu-id="8a608-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="8a608-126">**Id. de suscripción** -Hola toouse de Id. de suscripción.</span><span class="sxs-lookup"><span data-stu-id="8a608-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="8a608-127">**resourceGroupName** : hello nombre de un grupo de recursos que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8a608-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="8a608-128">Desde la siguiente Hola resultado, Id. de Hola de máquina virtual de Hola se usa en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="8a608-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="8a608-129">Obtención del próximo salto</span><span class="sxs-lookup"><span data-stu-id="8a608-129">Get Next Hop</span></span>

<span data-ttu-id="8a608-130">Una vez creado el encabezado de autorización de hello, se puede recuperar el próximo salto de Hola desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8a608-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="8a608-131">Hello valores siguientes se deben reemplazar para toowork de ejemplo de código de hello.</span><span class="sxs-lookup"><span data-stu-id="8a608-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="8a608-132">Para la API de REST de Monitor de red llamadas Hola nombre de grupo de recursos en solicitud de hello que URI es el grupo de recursos de Hola que contiene Hola Monitor de red, no se está realizando acciones de diagnóstico de hello en recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a608-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="8a608-133">Salto siguiente requiere que el recurso de máquina virtual de Hola se asigna toorun.</span><span class="sxs-lookup"><span data-stu-id="8a608-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="8a608-134">Results</span><span class="sxs-lookup"><span data-stu-id="8a608-134">Results</span></span>

<span data-ttu-id="8a608-135">Hello fragmento de código siguiente es un ejemplo de salida de hello recibido.</span><span class="sxs-lookup"><span data-stu-id="8a608-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="8a608-136">resultados de Hello contienen Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="8a608-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="8a608-137">**nextHopType** -este valor es uno de hello siguientes valores: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway o ninguno.</span><span class="sxs-lookup"><span data-stu-id="8a608-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="8a608-138">**nextHopIpAddress** -Hola dirección IP del próximo salto de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a608-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="8a608-139">**routeTableId** : valor de hello es un identificador uri para la tabla de ruta de hello asociado a la ruta de hello, o si no definido por el usuario ruta es valor Hola definido de *ruta del sistema* se devuelve.</span><span class="sxs-lookup"><span data-stu-id="8a608-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="8a608-140">siguiente Hola se muestran resultados de hello en formato json.</span><span class="sxs-lookup"><span data-stu-id="8a608-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="8a608-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8a608-141">Next steps</span></span>

<span data-ttu-id="8a608-142">Una vez que han sido capaz de toofind out próximo salto Hola para una máquina virtual, puede ver seguridad Hola de los recursos de red visitando [información general de la vista de la seguridad](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8a608-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














