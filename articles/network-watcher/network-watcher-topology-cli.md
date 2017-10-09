---
title: "topología de Monitor de red de Azure aaaView - CLI de Azure | Documentos de Microsoft"
description: "En este artículo se describe cómo toouse CLI de Azure tooquery la topología de red."
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
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="d7bda-103">Visualización de la topología de Network Watcher con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d7bda-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d7bda-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7bda-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="d7bda-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d7bda-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="d7bda-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d7bda-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="d7bda-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="d7bda-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="d7bda-108">característica de topología de Hola de Monitor de red proporciona una representación visual de los recursos de red de hello en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="d7bda-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="d7bda-109">En el portal de hello, esta visualización se presenta tooyou automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d7bda-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="d7bda-110">puede recuperar la información de Hello detrás de la vista de topología de hello en el portal de Hola a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7bda-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="d7bda-111">Esta capacidad hace que la información de la topología de hello sea más versátil como datos de hello pueden utilizarse otro toobuild herramientas out visualización Hola.</span><span class="sxs-lookup"><span data-stu-id="d7bda-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="d7bda-112">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="d7bda-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="d7bda-113">Network Watcher usa actualmente Azure CLI 1.0 para la compatibilidad con CLI.</span><span class="sxs-lookup"><span data-stu-id="d7bda-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="d7bda-114">interconexión de Hola se modela en dos relaciones.</span><span class="sxs-lookup"><span data-stu-id="d7bda-114">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="d7bda-115">**Contención**: por ejemplo, una red virtual contiene una subred que incluye una NIC.</span><span class="sxs-lookup"><span data-stu-id="d7bda-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="d7bda-116">**Asociación**: por ejemplo, la NIC está asociada a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7bda-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="d7bda-117">Hello lista siguiente es propiedades que se devuelven cuando se consultan Hola API de REST de topología.</span><span class="sxs-lookup"><span data-stu-id="d7bda-117">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="d7bda-118">**nombre** : hello nombre de recurso de Hola</span><span class="sxs-lookup"><span data-stu-id="d7bda-118">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="d7bda-119">**Id. de** -Hola uri del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7bda-119">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="d7bda-120">**ubicación** -Hola ubicación donde existe el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7bda-120">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="d7bda-121">**las asociaciones** -una lista de asociaciones toohello al que hace referencia el objeto.</span><span class="sxs-lookup"><span data-stu-id="d7bda-121">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="d7bda-122">**nombre de** -nombre de Hola de hello hace referencia a recursos.</span><span class="sxs-lookup"><span data-stu-id="d7bda-122">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="d7bda-123">**resourceId** -Hola resourceId es Hola uri del recurso de hello hace referencia en la asociación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7bda-123">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="d7bda-124">**associationType** -relación Hola entre Hola secundario y primario de hello hace referencia a este valor.</span><span class="sxs-lookup"><span data-stu-id="d7bda-124">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="d7bda-125">Los valores válidos son **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="d7bda-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d7bda-126">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="d7bda-126">Before you begin</span></span>

<span data-ttu-id="d7bda-127">En este escenario, utilice hello `network watcher topology` información de la topología de cmdlet tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="d7bda-127">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="d7bda-128">También hay un artículo sobre cómo demasiado[recuperar la topología de red con la API de REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d7bda-128">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="d7bda-129">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="d7bda-129">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d7bda-130">Escenario</span><span class="sxs-lookup"><span data-stu-id="d7bda-130">Scenario</span></span>

<span data-ttu-id="d7bda-131">escenario de Hello descrito en este artículo recupera la respuesta de la topología de Hola para un determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d7bda-131">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="d7bda-132">Recuperación de la topología</span><span class="sxs-lookup"><span data-stu-id="d7bda-132">Retrieve topology</span></span>

<span data-ttu-id="d7bda-133">Hola `network watcher topology` cmdlet recupera la topología de Hola para un grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="d7bda-133">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="d7bda-134">Agregue el argumento de Hola "--json" tooview hello oput en formato json</span><span class="sxs-lookup"><span data-stu-id="d7bda-134">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="d7bda-135">Results</span><span class="sxs-lookup"><span data-stu-id="d7bda-135">Results</span></span>

<span data-ttu-id="d7bda-136">Hello resultados devueltos tienen una propiedad nombre "recursos", que contiene el cuerpo de respuesta json de Hola para hello `network watcher topology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d7bda-136">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="d7bda-137">respuesta de Hello contiene recursos de hello en hello grupo de seguridad de red y sus asociaciones (es decir, Contains, asociados).</span><span class="sxs-lookup"><span data-stu-id="d7bda-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d7bda-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7bda-138">Next steps</span></span>

<span data-ttu-id="d7bda-139">Obtener más información sobre las reglas de seguridad de Hola que son los recursos de red aplicada tooyour visitando [información general de la vista de grupo de seguridad](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d7bda-139">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
