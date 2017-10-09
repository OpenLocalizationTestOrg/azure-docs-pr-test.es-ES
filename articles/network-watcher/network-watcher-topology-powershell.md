---
title: "topología de Monitor de red de Azure aaaView - PowerShell | Documentos de Microsoft"
description: "En este artículo se describe cómo toouse PowerShell tooquery la topología de red."
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
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="7dd5c-103">Visualización de la topología de Network Watcher con PowerShell</span><span class="sxs-lookup"><span data-stu-id="7dd5c-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7dd5c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7dd5c-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="7dd5c-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7dd5c-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="7dd5c-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7dd5c-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="7dd5c-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="7dd5c-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="7dd5c-108">característica de topología de Hola de Monitor de red proporciona una representación visual de los recursos de red de hello en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="7dd5c-109">En el portal de hello, esta visualización se presenta tooyou automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="7dd5c-110">puede recuperar la información de Hello detrás de la vista de topología de hello en el portal de Hola a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="7dd5c-111">Esta capacidad hace que la información de la topología de hello sea más versátil como datos de hello pueden utilizarse otro toobuild herramientas out visualización Hola.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="7dd5c-112">interconexión de Hola se modela en dos relaciones.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="7dd5c-113">**Contención**: por ejemplo, una red virtual contiene una subred que incluye una NIC.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="7dd5c-114">**Asociación**: por ejemplo, la NIC está asociada a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="7dd5c-115">Hello lista siguiente es propiedades que se devuelven cuando se consultan Hola API de REST de topología.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="7dd5c-116">**nombre** : hello nombre de recurso de Hola</span><span class="sxs-lookup"><span data-stu-id="7dd5c-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="7dd5c-117">**Id. de** -Hola uri del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="7dd5c-118">**ubicación** -Hola ubicación donde existe el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="7dd5c-119">**las asociaciones** -una lista de asociaciones toohello al que hace referencia el objeto.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="7dd5c-120">**nombre de** -nombre de Hola de hello hace referencia a recursos.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="7dd5c-121">**resourceId** -Hola resourceId es Hola uri del recurso de hello hace referencia en la asociación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="7dd5c-122">**associationType** -relación Hola entre Hola secundario y primario de hello hace referencia a este valor.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="7dd5c-123">Los valores válidos son **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7dd5c-124">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="7dd5c-124">Before you begin</span></span>

<span data-ttu-id="7dd5c-125">En este escenario, utilice hello `Get-AzureRmNetworkWatcherTopology` información de la topología de cmdlet tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="7dd5c-126">También hay un artículo sobre cómo demasiado[recuperar la topología de red con la API de REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="7dd5c-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="7dd5c-127">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="7dd5c-128">Escenario</span><span class="sxs-lookup"><span data-stu-id="7dd5c-128">Scenario</span></span>

<span data-ttu-id="7dd5c-129">escenario de Hello descrito en este artículo recupera la respuesta de la topología de Hola para un determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="7dd5c-130">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="7dd5c-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="7dd5c-131">Hola primer paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="7dd5c-132">Hola `$networkWatcher` pasa una variable toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="7dd5c-133">Recuperación de la topología</span><span class="sxs-lookup"><span data-stu-id="7dd5c-133">Retrieve topology</span></span>

<span data-ttu-id="7dd5c-134">Hola `Get-AzureRmNetworkWatcherTopology` cmdlet recupera la topología de Hola para un grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="7dd5c-135">Results</span><span class="sxs-lookup"><span data-stu-id="7dd5c-135">Results</span></span>

<span data-ttu-id="7dd5c-136">Hello resultados devueltos tienen una propiedad nombre "recursos", que contiene el cuerpo de respuesta json de Hola para hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7dd5c-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="7dd5c-137">respuesta de Hello contiene recursos de hello en hello grupo de seguridad de red y sus asociaciones (es decir, Contains, asociados).</span><span class="sxs-lookup"><span data-stu-id="7dd5c-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7dd5c-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7dd5c-138">Next steps</span></span>

<span data-ttu-id="7dd5c-139">Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="7dd5c-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


