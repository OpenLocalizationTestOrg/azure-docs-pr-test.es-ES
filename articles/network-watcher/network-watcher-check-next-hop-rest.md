---
title: "Búsqueda de Next Hop con Azure Network Watcher (REST) | Microsoft Docs"
description: "En este artículo se describe cómo encontrar el tipo del próximo salto y la dirección IP usando la funcionalidad Next Hop con la API de REST de Azure."
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
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="cf135-103">Descubra cuál es el tipo del próximo salto que usa la funcionalidad Next Hop en Azure Network Watcher mediante la API de REST de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf135-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="cf135-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cf135-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="cf135-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf135-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="cf135-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="cf135-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="cf135-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cf135-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="cf135-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="cf135-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="cf135-109">Next Hop es una característica de Network Watcher que permite obtener el tipo del próximo salto y la dirección IP para una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="cf135-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="cf135-110">Esta funcionalidad es útil para determinar si el tráfico que sale de una máquina virtual atraviesa una puerta de enlace, Internet o redes virtuales para llegar a su destino.</span><span class="sxs-lookup"><span data-stu-id="cf135-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cf135-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="cf135-111">Before you begin</span></span>

<span data-ttu-id="cf135-112">ARMclient se usa para llamar a la API de REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf135-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="cf135-113">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="cf135-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="cf135-114">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="cf135-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="cf135-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="cf135-115">Scenario</span></span>

<span data-ttu-id="cf135-116">El escenario descrito en este artículo usa Next Hop, una característica de Network Watcher, para averiguar el tipo de próximo salto y la dirección IP de un recurso.</span><span class="sxs-lookup"><span data-stu-id="cf135-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="cf135-117">Para más información acerca de Next Hop, consulte la [introducción a Next Hop](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf135-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="cf135-118">En este escenario va a:</span><span class="sxs-lookup"><span data-stu-id="cf135-118">In this scenario, you will:</span></span>

* <span data-ttu-id="cf135-119">Recuperar el próximo salto para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cf135-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="cf135-120">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="cf135-120">Log in with ARMClient</span></span>

<span data-ttu-id="cf135-121">Inicie sesión en armclient con las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf135-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="cf135-122">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cf135-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="cf135-123">Ejecute el siguiente script para devolver una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cf135-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="cf135-124">Esta información es necesaria para ejecutar el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="cf135-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="cf135-125">El código siguiente necesita valores para las siguientes variables:</span><span class="sxs-lookup"><span data-stu-id="cf135-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="cf135-126">**subscriptionId**: el identificador de suscripción que se usará.</span><span class="sxs-lookup"><span data-stu-id="cf135-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="cf135-127">**resourceGroupName**: el nombre del grupo de recursos que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cf135-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="cf135-128">En el resultado siguiente, se usa el id. de la máquina virtual en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cf135-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="cf135-129">Obtención del próximo salto</span><span class="sxs-lookup"><span data-stu-id="cf135-129">Get Next Hop</span></span>

<span data-ttu-id="cf135-130">Cuando se ha creado el encabezado de autorización, se puede recuperar el próximo salto de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cf135-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="cf135-131">Para que funcione el ejemplo de código, se deben reemplazar los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="cf135-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="cf135-132">En las llamadas a la API de REST de Network Watcher, el nombre del grupo de recursos en el identificador URI de la solicitud es el grupo de recursos que contiene Network Watcher, y no los recursos sobre los que realiza las acciones de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="cf135-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

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
> <span data-ttu-id="cf135-133">Un requisito del próximo salto es que el recurso de máquina virtual esté asignado para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="cf135-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="cf135-134">Results</span><span class="sxs-lookup"><span data-stu-id="cf135-134">Results</span></span>

<span data-ttu-id="cf135-135">El fragmento de código siguiente es un ejemplo del resultado recibido.</span><span class="sxs-lookup"><span data-stu-id="cf135-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="cf135-136">Los resultados contienen los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="cf135-136">The results contain the following values:</span></span>

* <span data-ttu-id="cf135-137">**nextHopType**: este valor es uno de los siguientes valores: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway o None.</span><span class="sxs-lookup"><span data-stu-id="cf135-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="cf135-138">**nextHopIpAddress**: la dirección IP del próximo salto.</span><span class="sxs-lookup"><span data-stu-id="cf135-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="cf135-139">**routeTableId**: el valor es un identificador URI para la tabla de enrutamiento asociada con la ruta o, si no se especifica ninguna ruta definida por el usuario, se devuelve el valor de *ruta del sistema*.</span><span class="sxs-lookup"><span data-stu-id="cf135-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="cf135-140">Estos son los resultados en formato json.</span><span class="sxs-lookup"><span data-stu-id="cf135-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="cf135-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf135-141">Next steps</span></span>

<span data-ttu-id="cf135-142">Cuando haya descubierto el próximo salto de una máquina virtual, puede ver la seguridad de sus recursos de red en el artículo [Introducción a las vistas de seguridad](network-watcher-security-group-view-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf135-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














