---
title: "Ejemplo de secuencia de comandos de CLI: enrutar el tráfico para lograr alta disponibilidad de aplicaciones aaaAzure | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: enrutamiento del tráfico para la alta disponibilidad de las aplicaciones"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="9eb1a-103">Enrutamiento del tráfico para la alta disponibilidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9eb1a-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="9eb1a-104">Este script crea un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="9eb1a-105">Administrador de tráfico dirige la aplicación de toohello de tráfico en una región como región principal de Hola y región secundaria toohello cuando la aplicación hello en la región principal de hello no está disponible.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="9eb1a-106">Antes de ejecutar script de Hola, debe cambiar Hola MyWebApp, MyWebAppL1 y MyWebAppL2 valores toounique valores a través de Azure.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="9eb1a-107">Después de ejecutar el script de Hola, puede tener acceso a la aplicación hello en la región principal de hello con hello mywebapp.trafficmanager.net de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9eb1a-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9eb1a-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="9eb1a-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="9eb1a-109">Clean up deployment</span></span> 

<span data-ttu-id="9eb1a-110">Después de ejecutar el ejemplo de secuencia de comandos de hello, el comando de seguimiento de hello puede ser grupo de recursos de hello tooremove usado, aplicación de servicio de aplicaciones y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9eb1a-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="9eb1a-111">Script explanation</span></span>

<span data-ttu-id="9eb1a-112">Este script utiliza Hola después comandos toocreate un grupo de recursos, la aplicación web, el perfil del Administrador de tráfico y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="9eb1a-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9eb1a-114">Comando</span><span class="sxs-lookup"><span data-stu-id="9eb1a-114">Command</span></span> | <span data-ttu-id="9eb1a-115">Notas</span><span class="sxs-lookup"><span data-stu-id="9eb1a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9eb1a-116">az group create</span><span class="sxs-lookup"><span data-stu-id="9eb1a-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9eb1a-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9eb1a-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="9eb1a-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9eb1a-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="9eb1a-119">Creates an App Service plan.</span></span> <span data-ttu-id="9eb1a-120">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="9eb1a-121">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="9eb1a-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="9eb1a-122">Crea una aplicación web de Azure en hello plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="9eb1a-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="9eb1a-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="9eb1a-124">Crea un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="9eb1a-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="9eb1a-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="9eb1a-126">Agrega un perfil de Traffic Manager de Azure tooan de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="9eb1a-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9eb1a-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9eb1a-127">Next steps</span></span>

<span data-ttu-id="9eb1a-128">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9eb1a-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9eb1a-129">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [red Azure documentación](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9eb1a-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
