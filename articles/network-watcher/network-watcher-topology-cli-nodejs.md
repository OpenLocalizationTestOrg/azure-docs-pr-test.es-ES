---
title: "Visualización de la topología de Azure Network Watcher con la CLI de Azure 1.0 | Microsoft Docs"
description: "En este artículo se describe cómo usar la CLI de Azure 1.0 para consultar la topología de red."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9178c485a92e04564c95dae8073f045b5c639bb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="9c3a1-103">Visualización de la topología de Network Watcher con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9c3a1-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9c3a1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c3a1-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="9c3a1-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9c3a1-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="9c3a1-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9c3a1-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="9c3a1-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="9c3a1-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="9c3a1-108">La característica Topología de Network Watcher proporciona una representación visual de los recursos de red de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="9c3a1-109">En el portal, esta visualización se muestra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="9c3a1-110">La información subyacente a la vista de topología en el portal se puede obtener mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="9c3a1-111">Esta funcionalidad hace que la información de la topología sea más versátil porque otras herramientas pueden usar los datos para crear la visualización.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="9c3a1-112">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="9c3a1-113">La interconexión se modela en dos relaciones.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-113">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="9c3a1-114">**Contención**: por ejemplo, una red virtual contiene una subred que incluye una NIC.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="9c3a1-115">**Asociación**: por ejemplo, la NIC está asociada a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="9c3a1-116">La lista siguiente muestra las propiedades que se devuelven cuando se consulta la API de REST de Topología.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-116">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="9c3a1-117">**name**: nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-117">**name** - The name of the resource</span></span>
* <span data-ttu-id="9c3a1-118">**id**: identificador URI del recurso.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-118">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="9c3a1-119">**location**: ubicación donde existe el recurso.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-119">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="9c3a1-120">**associations**: lista de asociaciones para el objeto al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-120">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="9c3a1-121">**name**: nombre del recurso al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-121">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="9c3a1-122">**resourceId**: identificador URI del recurso al que se hace referencia en la asociación.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-122">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="9c3a1-123">**associationType**: este valor hace referencia a la relación entre los objetos secundario y primario.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-123">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="9c3a1-124">Los valores válidos son **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9c3a1-125">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9c3a1-125">Before you begin</span></span>

<span data-ttu-id="9c3a1-126">En este escenario, se usa el cmdlet `network watcher topology` para recuperar la información de la topología.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-126">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="9c3a1-127">También hay un artículo sobre cómo [recuperar la topología de red con la API de REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="9c3a1-127">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="9c3a1-128">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="9c3a1-129">Escenario</span><span class="sxs-lookup"><span data-stu-id="9c3a1-129">Scenario</span></span>

<span data-ttu-id="9c3a1-130">El escenario descrito en este artículo recupera la respuesta de la topología para un grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="9c3a1-131">Recuperación de la topología</span><span class="sxs-lookup"><span data-stu-id="9c3a1-131">Retrieve topology</span></span>

<span data-ttu-id="9c3a1-132">El cmdlet `network watcher topology` recupera la topología para un grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-132">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="9c3a1-133">Agregue el argumento "--json" para ver la salida en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-133">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="9c3a1-134">Results</span><span class="sxs-lookup"><span data-stu-id="9c3a1-134">Results</span></span>

<span data-ttu-id="9c3a1-135">Los resultados devueltos tienen una propiedad llamada "Resources", que contiene el cuerpo de la respuesta JSON para el cmdlet `network watcher topology`.</span><span class="sxs-lookup"><span data-stu-id="9c3a1-135">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="9c3a1-136">La respuesta contiene los recursos que hay en el grupo de seguridad de red y sus asociaciones (es decir, Contains, Associated).</span><span class="sxs-lookup"><span data-stu-id="9c3a1-136">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="9c3a1-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c3a1-137">Next steps</span></span>

<span data-ttu-id="9c3a1-138">Para más información sobre las reglas de seguridad que se aplican a los recursos de red, consulte la [información general de la vista de grupos de seguridad](network-watcher-security-group-view-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c3a1-138">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>