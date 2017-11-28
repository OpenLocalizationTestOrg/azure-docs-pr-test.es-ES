---
title: "Visualización de la topología de Azure Network Watcher (API de REST) | Microsoft Docs"
description: "En este artículo se describe cómo usar la API de REST para consultar la topología de red."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 568f3060da372f4a08cec342e04359172522cb69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="36811-103">Visualización de la topología de Network Watcher con la API de REST</span><span class="sxs-lookup"><span data-stu-id="36811-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="36811-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36811-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="36811-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="36811-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="36811-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="36811-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="36811-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="36811-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="36811-108">La característica Topología de Network Watcher proporciona una representación visual de los recursos de red de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="36811-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="36811-109">En el portal, esta visualización se muestra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="36811-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="36811-110">La información subyacente a la vista de topología en el portal se puede obtener mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36811-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="36811-111">Esta funcionalidad hace que la información de la topología sea más versátil porque otras herramientas pueden usar los datos para crear la visualización.</span><span class="sxs-lookup"><span data-stu-id="36811-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="36811-112">La interconexión se modela en dos relaciones.</span><span class="sxs-lookup"><span data-stu-id="36811-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="36811-113">**Contención**: por ejemplo, una red virtual contiene una subred que incluye una NIC.</span><span class="sxs-lookup"><span data-stu-id="36811-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="36811-114">**Asociación**: por ejemplo, la NIC está asociada a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="36811-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="36811-115">La lista siguiente muestra las propiedades que se devuelven cuando se consulta la API de REST de Topología.</span><span class="sxs-lookup"><span data-stu-id="36811-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="36811-116">**name**: nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="36811-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="36811-117">**id**: identificador URI del recurso.</span><span class="sxs-lookup"><span data-stu-id="36811-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="36811-118">**location**: ubicación donde existe el recurso.</span><span class="sxs-lookup"><span data-stu-id="36811-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="36811-119">**associations**: lista de asociaciones para el objeto al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="36811-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="36811-120">**name**: nombre del recurso al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="36811-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="36811-121">**resourceId**: identificador URI del recurso al que se hace referencia en la asociación.</span><span class="sxs-lookup"><span data-stu-id="36811-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="36811-122">**associationType**: este valor hace referencia a la relación entre los objetos secundario y primario.</span><span class="sxs-lookup"><span data-stu-id="36811-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="36811-123">Los valores válidos son **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="36811-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="36811-124">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="36811-124">Before you begin</span></span>

<span data-ttu-id="36811-125">En este escenario, se recupera la información de la topología.</span><span class="sxs-lookup"><span data-stu-id="36811-125">In this scenario, you retrieve the topology information.</span></span> <span data-ttu-id="36811-126">ARMclient se usa para llamar a la API de REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36811-126">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="36811-127">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="36811-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="36811-128">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="36811-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="36811-129">Escenario</span><span class="sxs-lookup"><span data-stu-id="36811-129">Scenario</span></span>

<span data-ttu-id="36811-130">El escenario descrito en este artículo recupera la respuesta de la topología para un grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="36811-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="36811-131">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="36811-131">Log in with ARMClient</span></span>

<span data-ttu-id="36811-132">Inicie sesión en armclient con las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="36811-132">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="36811-133">Recuperación de la topología</span><span class="sxs-lookup"><span data-stu-id="36811-133">Retrieve topology</span></span>

<span data-ttu-id="36811-134">En el ejemplo siguiente, se solicita la topología de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="36811-134">The following example requests the topology from the REST API.</span></span>  <span data-ttu-id="36811-135">El ejemplo se parametriza para aportar flexibilidad en la creación de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="36811-135">The example is parameterized to allow for flexibility in creating an example.</span></span>  <span data-ttu-id="36811-136">Reemplace todos los valores dentro de \< \>.</span><span class="sxs-lookup"><span data-stu-id="36811-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name to run topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="36811-137">La respuesta siguiente es un ejemplo de una respuesta reducida que se devuelve cuando se recupera la topología para un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="36811-137">The following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="36811-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="36811-138">Next steps</span></span>

<span data-ttu-id="36811-139">Aprenda a visualizar los registros de flujo de grupo de seguridad de red con Power BI en el artículo [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Visualización de registros de flujo de grupo de seguridad de red con Power BI).</span><span class="sxs-lookup"><span data-stu-id="36811-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

