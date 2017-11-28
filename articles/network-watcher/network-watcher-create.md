---
title: "Creación de una instancia de Azure Network Watcher | Microsoft Docs"
description: "En esta página se proporcionan los pasos necesarios para crear una instancia de Network Watcher mediante el portal y la API de REST de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2aeaffdd5ab552e18677cbd1a24a748dd14bf172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="4942b-103">Creación de una instancia de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="4942b-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="4942b-104">Network Watcher es un servicio regional que permite supervisar y diagnosticar problemas en un nivel de escenario de red mediante Azure.</span><span class="sxs-lookup"><span data-stu-id="4942b-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="4942b-105">La supervisión del nivel de escenario permite diagnosticar problemas en una vista de nivel de red de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="4942b-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span></span> <span data-ttu-id="4942b-106">Las herramientas de visualización y diagnóstico de red que incluye Network Watcher le ayudan a conocer, diagnosticar y obtener información acerca de cualquier red de Azure.</span><span class="sxs-lookup"><span data-stu-id="4942b-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="4942b-107">Debido a que, por el momento, Network Watcher solo es compatible con CLI 1.0, las instrucciones para crear una nueva instancia de Network Watcher son las mismas que para CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="4942b-107">As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-the-portal"></a><span data-ttu-id="4942b-108">Creación de una instancia de Network Watcher en el portal</span><span class="sxs-lookup"><span data-stu-id="4942b-108">Create a Network Watcher in the portal</span></span>

<span data-ttu-id="4942b-109">Navegue a **Más servicios** > **Redes** > **Network Watcher**.</span><span class="sxs-lookup"><span data-stu-id="4942b-109">Navigate to **More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="4942b-110">Puede seleccionar todas las suscripciones para las que desee habilitar Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="4942b-110">You can select all the subscriptions you want to enable Network Watcher for.</span></span> <span data-ttu-id="4942b-111">Esta acción crea una instancia de Network Watcher en todas las regiones que estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="4942b-111">This action creates a Network Watcher in every region that is available.</span></span>

![crear una instancia de network watcher][1]

<span data-ttu-id="4942b-113">Cuando habilita Network Watcher mediante el Portal, el nombre de la instancia de Network Watcher se establecerá automáticamente en Network_region_name, donde region_name corresponde a la región de Azure donde se habilitó la instancia.</span><span class="sxs-lookup"><span data-stu-id="4942b-113">When you enable Network Watcher using the Portal, the name of the Network Watcher instance will automatically be set to NetworkWatcher_region_name where region_name corresponds to the Azure Region where the instance was enabled.</span></span>  <span data-ttu-id="4942b-114">Por ejemplo, una instancia de Network Watcher habilitada en la región Centro occidental de EE. UU. se denominará NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="4942b-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="4942b-115">Además, la instancia de Network Watcher se agregará automáticamente a un grupo de recursos llamado NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="4942b-115">Additionally, the Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="4942b-116">Se creará este grupo de recursos si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="4942b-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="4942b-117">Si desea personalizar el nombre de una instancia de Network Watcher y el grupo de recursos en que se encuentra, puede usar PowerShell, la API de REST o los métodos de ARMClient que se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="4942b-117">If you wish to customize the name of a Network Watcher instance and the Resource Group it's placed into, you can use Powershell, the REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="4942b-118">En cada opción, el grupo de recursos debe existir antes de que ubique Network Watcher ahí.</span><span class="sxs-lookup"><span data-stu-id="4942b-118">In each option, the Resource Group must exist before you place the Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="4942b-119">Creación de una instancia de Network Watcher con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4942b-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="4942b-120">Para crear una instancia de Network Watcher, ejecute el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4942b-120">To create an instance of Network Watcher, run the following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a><span data-ttu-id="4942b-121">Creación de una instancia de Network Watcher con la API de REST</span><span class="sxs-lookup"><span data-stu-id="4942b-121">Create a Network Watcher with the REST API</span></span>

<span data-ttu-id="4942b-122">ARMclient se usa para llamar a la API de REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4942b-122">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="4942b-123">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="4942b-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="4942b-124">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="4942b-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a><span data-ttu-id="4942b-125">Creación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="4942b-125">Create the network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="4942b-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4942b-126">Next steps</span></span>

<span data-ttu-id="4942b-127">Ahora que tiene una instancia de Network Watcher, obtenga información acerca de las características disponibles:</span><span class="sxs-lookup"><span data-stu-id="4942b-127">Now that you have an instance of Network Watcher, learn about the features available:</span></span>

* [<span data-ttu-id="4942b-128">Topología</span><span class="sxs-lookup"><span data-stu-id="4942b-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="4942b-129">Captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="4942b-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="4942b-130">Comprobación de flujo de IP</span><span class="sxs-lookup"><span data-stu-id="4942b-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="4942b-131">Próximo salto</span><span class="sxs-lookup"><span data-stu-id="4942b-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="4942b-132">Vista de grupo de seguridad</span><span class="sxs-lookup"><span data-stu-id="4942b-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="4942b-133">Registro de flujo de NSG</span><span class="sxs-lookup"><span data-stu-id="4942b-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="4942b-134">Solución de problemas de una puerta de enlace de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="4942b-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="4942b-135">Una vez creada una instancia de Network Watcher, para configurar la captura de paquetes vea el artículo [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md) (Crear una captura de paquetes desencadenada por alertas).</span><span class="sxs-lookup"><span data-stu-id="4942b-135">Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











