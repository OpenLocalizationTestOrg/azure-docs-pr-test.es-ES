---
title: aaaCreate una instancia del Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona Hola pasos toocreate una instancia del Monitor de red mediante el portal de Hola y la API de REST de Azure"
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
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="92fd1-103">Creación de una instancia de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="92fd1-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="92fd1-104">Monitor de red es un servicio regional que permite toomonitor y diagnosticar condiciones en un nivel de escenario de red, hacia y desde Azure.</span><span class="sxs-lookup"><span data-stu-id="92fd1-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="92fd1-105">Supervisión del nivel de escenario permite toodiagnose problemas en una vista de nivel de red de tooend final.</span><span class="sxs-lookup"><span data-stu-id="92fd1-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="92fd1-106">Diagnóstico de red y herramientas de visualización disponibles con Monitor de red ayudan a comprender, diagnosticar y obtener red tooyour de visión en Azure.</span><span class="sxs-lookup"><span data-stu-id="92fd1-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="92fd1-107">Monitor de red actualmente solo admite CLI 1.0, Hola instrucciones toocreate una nueva instancia de Monitor de red se proporciona para CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="92fd1-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="92fd1-108">Crear un monitor de red en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="92fd1-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="92fd1-109">Navegue demasiado**más servicios** > **red** > **Monitor de red**.</span><span class="sxs-lookup"><span data-stu-id="92fd1-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="92fd1-110">Puede seleccionar todas las suscripciones de hello desea tooenable Monitor de red para.</span><span class="sxs-lookup"><span data-stu-id="92fd1-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="92fd1-111">Esta acción crea una instancia de Network Watcher en todas las regiones que estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="92fd1-111">This action creates a Network Watcher in every region that is available.</span></span>

![crear una instancia de network watcher][1]

<span data-ttu-id="92fd1-113">Cuando se habilita el Monitor de red mediante el Portal de Hola, nombre de Hola de instancia de Monitor de red de hello establecerá automáticamente tooNetworkWatcher_region_name donde region_name corresponde toohello región de Azure donde se habilitó la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="92fd1-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="92fd1-114">Por ejemplo, una instancia de Network Watcher habilitada en la región Centro occidental de EE. UU. se denominará NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="92fd1-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="92fd1-115">Además, la instancia de Monitor de red de Hola se agregará automáticamente en un grupo de recursos denominado NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="92fd1-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="92fd1-116">Se creará este grupo de recursos si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="92fd1-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="92fd1-117">Si desea que el nombre de hello toocustomize de una instancia del Monitor de red y Hola grupo de recursos se ha colocado en, puede usar métodos de Powershell, API de REST de Hola o ARMClient que se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="92fd1-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="92fd1-118">En cada opción, Hola grupo de recursos debe existir antes de colocar Hola Monitor de red en él.</span><span class="sxs-lookup"><span data-stu-id="92fd1-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="92fd1-119">Creación de una instancia de Network Watcher con PowerShell</span><span class="sxs-lookup"><span data-stu-id="92fd1-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="92fd1-120">una instancia del Monitor de red, ejecute el siguiente ejemplo de Hola toocreate:</span><span class="sxs-lookup"><span data-stu-id="92fd1-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="92fd1-121">Crear un monitor de red con hello API de REST</span><span class="sxs-lookup"><span data-stu-id="92fd1-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="92fd1-122">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92fd1-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="92fd1-123">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="92fd1-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="92fd1-124">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="92fd1-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="92fd1-125">Crear Monitor de red de Hola</span><span class="sxs-lookup"><span data-stu-id="92fd1-125">Create hello network watcher</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="92fd1-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="92fd1-126">Next steps</span></span>

<span data-ttu-id="92fd1-127">Ahora que tiene una instancia del Monitor de red, obtener información acerca de las características de hello disponibles:</span><span class="sxs-lookup"><span data-stu-id="92fd1-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="92fd1-128">Topología</span><span class="sxs-lookup"><span data-stu-id="92fd1-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="92fd1-129">Captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="92fd1-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="92fd1-130">Comprobación de flujo de IP</span><span class="sxs-lookup"><span data-stu-id="92fd1-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="92fd1-131">Próximo salto</span><span class="sxs-lookup"><span data-stu-id="92fd1-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="92fd1-132">Vista de grupo de seguridad</span><span class="sxs-lookup"><span data-stu-id="92fd1-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="92fd1-133">Registro de flujo de NSG</span><span class="sxs-lookup"><span data-stu-id="92fd1-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="92fd1-134">Solución de problemas de una puerta de enlace de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="92fd1-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="92fd1-135">Una vez creada una instancia del Monitor de red, captura de paquete puede configurarse mediante el siguiente artículo de hello: [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="92fd1-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











