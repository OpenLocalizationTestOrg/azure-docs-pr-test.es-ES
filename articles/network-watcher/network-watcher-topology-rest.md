---
title: "topología de Monitor de red de Azure aaaView: API de REST | Documentos de Microsoft"
description: "En este artículo se describe cómo toouse REST API tooquery la topología de red."
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
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="e2264-103">Visualización de la topología de Network Watcher con la API de REST</span><span class="sxs-lookup"><span data-stu-id="e2264-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e2264-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2264-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="e2264-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e2264-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="e2264-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e2264-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="e2264-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="e2264-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="e2264-108">característica de topología de Hola de Monitor de red proporciona una representación visual de los recursos de red de hello en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="e2264-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="e2264-109">En el portal de hello, esta visualización se presenta tooyou automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e2264-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="e2264-110">puede recuperar la información de Hello detrás de la vista de topología de hello en el portal de Hola a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2264-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="e2264-111">Esta capacidad hace que la información de la topología de hello sea más versátil como datos de hello pueden utilizarse otro toobuild herramientas out visualización Hola.</span><span class="sxs-lookup"><span data-stu-id="e2264-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="e2264-112">interconexión de Hola se modela en dos relaciones.</span><span class="sxs-lookup"><span data-stu-id="e2264-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="e2264-113">**Contención**: por ejemplo, una red virtual contiene una subred que incluye una NIC.</span><span class="sxs-lookup"><span data-stu-id="e2264-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="e2264-114">**Asociación**: por ejemplo, la NIC está asociada a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e2264-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="e2264-115">Hello lista siguiente es propiedades que se devuelven cuando se consultan Hola API de REST de topología.</span><span class="sxs-lookup"><span data-stu-id="e2264-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="e2264-116">**nombre** : hello nombre de recurso de Hola</span><span class="sxs-lookup"><span data-stu-id="e2264-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="e2264-117">**Id. de** -Hola uri del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2264-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="e2264-118">**ubicación** -Hola ubicación donde existe el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2264-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="e2264-119">**las asociaciones** -una lista de asociaciones toohello al que hace referencia el objeto.</span><span class="sxs-lookup"><span data-stu-id="e2264-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="e2264-120">**nombre de** -nombre de Hola de hello hace referencia a recursos.</span><span class="sxs-lookup"><span data-stu-id="e2264-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="e2264-121">**resourceId** -Hola resourceId es Hola uri del recurso de hello hace referencia en la asociación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2264-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="e2264-122">**associationType** -relación Hola entre Hola secundario y primario de hello hace referencia a este valor.</span><span class="sxs-lookup"><span data-stu-id="e2264-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="e2264-123">Los valores válidos son **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="e2264-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e2264-124">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e2264-124">Before you begin</span></span>

<span data-ttu-id="e2264-125">En este escenario, recupera la información de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2264-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="e2264-126">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2264-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="e2264-127">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="e2264-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="e2264-128">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="e2264-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="e2264-129">Escenario</span><span class="sxs-lookup"><span data-stu-id="e2264-129">Scenario</span></span>

<span data-ttu-id="e2264-130">escenario de Hello descrito en este artículo recupera la respuesta de la topología de Hola para un determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2264-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="e2264-131">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="e2264-131">Log in with ARMClient</span></span>

<span data-ttu-id="e2264-132">Inicie sesión en tooarmclient con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2264-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="e2264-133">Recuperación de la topología</span><span class="sxs-lookup"><span data-stu-id="e2264-133">Retrieve topology</span></span>

<span data-ttu-id="e2264-134">Hola siguiendo el ejemplo de topología de hello las solicitudes de hello API de REST.</span><span class="sxs-lookup"><span data-stu-id="e2264-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="e2264-135">ejemplo de Hola es tooallow con parámetros para flexibilidad en la creación de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e2264-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="e2264-136">Reemplace todos los valores dentro de \< \>.</span><span class="sxs-lookup"><span data-stu-id="e2264-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="e2264-137">Hola después de la respuesta es un ejemplo de una respuesta reducida que se devuelve cuando recuperar topología para un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="e2264-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e2264-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2264-138">Next steps</span></span>

<span data-ttu-id="e2264-139">Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="e2264-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

