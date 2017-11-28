---
title: "Visualización de la topología de Azure Network Watcher (PowerShell) | Microsoft Docs"
description: "En este artículo se describe cómo usar PowerShell para consultar una topología de red."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="fce27-103">Visualización de la topología de Network Watcher con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fce27-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fce27-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fce27-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="fce27-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fce27-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="fce27-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fce27-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="fce27-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="fce27-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="fce27-108">La característica Topología de Network Watcher proporciona una representación visual de los recursos de red de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="fce27-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="fce27-109">En el portal, esta visualización se muestra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fce27-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="fce27-110">La información subyacente a la vista de topología en el portal se puede obtener mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fce27-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="fce27-111">Esta funcionalidad hace que la información de la topología sea más versátil porque otras herramientas pueden usar los datos para crear la visualización.</span><span class="sxs-lookup"><span data-stu-id="fce27-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="fce27-112">La interconexión se modela en dos relaciones.</span><span class="sxs-lookup"><span data-stu-id="fce27-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="fce27-113">**Contención**: por ejemplo, una red virtual contiene una subred que incluye una NIC.</span><span class="sxs-lookup"><span data-stu-id="fce27-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="fce27-114">**Asociación**: por ejemplo, la NIC está asociada a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fce27-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="fce27-115">La lista siguiente muestra las propiedades que se devuelven cuando se consulta la API de REST de Topología.</span><span class="sxs-lookup"><span data-stu-id="fce27-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="fce27-116">**name**: nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="fce27-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="fce27-117">**id**: identificador URI del recurso.</span><span class="sxs-lookup"><span data-stu-id="fce27-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="fce27-118">**location**: ubicación donde existe el recurso.</span><span class="sxs-lookup"><span data-stu-id="fce27-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="fce27-119">**associations**: lista de asociaciones para el objeto al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="fce27-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="fce27-120">**name**: nombre del recurso al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="fce27-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="fce27-121">**resourceId**: identificador URI del recurso al que se hace referencia en la asociación.</span><span class="sxs-lookup"><span data-stu-id="fce27-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="fce27-122">**associationType**: este valor hace referencia a la relación entre los objetos secundario y primario.</span><span class="sxs-lookup"><span data-stu-id="fce27-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="fce27-123">Los valores válidos son **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="fce27-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fce27-124">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="fce27-124">Before you begin</span></span>

<span data-ttu-id="fce27-125">En este escenario, se usa el cmdlet `Get-AzureRmNetworkWatcherTopology` para recuperar la información de la topología.</span><span class="sxs-lookup"><span data-stu-id="fce27-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="fce27-126">También hay un artículo sobre cómo [recuperar la topología de red con la API de REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="fce27-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="fce27-127">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="fce27-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="fce27-128">Escenario</span><span class="sxs-lookup"><span data-stu-id="fce27-128">Scenario</span></span>

<span data-ttu-id="fce27-129">El escenario descrito en este artículo recupera la respuesta de la topología para un grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="fce27-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="fce27-130">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="fce27-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="fce27-131">El primer paso consiste en recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="fce27-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="fce27-132">La variable `$networkWatcher` se pasa al cmdlet `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="fce27-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="fce27-133">Recuperación de la topología</span><span class="sxs-lookup"><span data-stu-id="fce27-133">Retrieve topology</span></span>

<span data-ttu-id="fce27-134">El cmdlet `Get-AzureRmNetworkWatcherTopology` recupera la topología para un grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="fce27-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="fce27-135">Results</span><span class="sxs-lookup"><span data-stu-id="fce27-135">Results</span></span>

<span data-ttu-id="fce27-136">Los resultados devueltos tienen una propiedad llamada "Resources", que contiene el cuerpo de la respuesta JSON para el cmdlet `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="fce27-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="fce27-137">La respuesta contiene los recursos que hay en el grupo de seguridad de red y sus asociaciones (es decir, Contains, Associated).</span><span class="sxs-lookup"><span data-stu-id="fce27-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="fce27-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fce27-138">Next steps</span></span>

<span data-ttu-id="fce27-139">Aprenda a visualizar los registros de flujo de grupo de seguridad de red con Power BI en el artículo [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Visualización de registros de flujo de grupo de seguridad de red con Power BI).</span><span class="sxs-lookup"><span data-stu-id="fce27-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


