---
title: "Ejemplo de script de la CLI de Azure: enrutamiento del tráfico para la alta disponibilidad de las aplicaciones | Microsoft Docs"
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
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="fc66a-103">Enrutamiento del tráfico para la alta disponibilidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fc66a-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="fc66a-104">Este script crea un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fc66a-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="fc66a-105">Traffic Manager dirige el tráfico a la aplicación en una región como la región primaria y a la región secundaria cuando no está disponible la aplicación en la región primaria.</span><span class="sxs-lookup"><span data-stu-id="fc66a-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="fc66a-106">Antes de ejecutar el script, debe cambiar los valores de MyWebApp, MyWebAppL1 y MyWebAppL2 a valores únicos en todo Azure.</span><span class="sxs-lookup"><span data-stu-id="fc66a-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="fc66a-107">Después de ejecutar el script, puede tener acceso a la aplicación en la región primaria con la dirección URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="fc66a-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fc66a-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="fc66a-108">Sample script</span></span>

<span data-ttu-id="fc66a-109">[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Enrutamiento del tráfico para la alta disponibilidad de las aplicaciones")]</span><span class="sxs-lookup"><span data-stu-id="fc66a-109">[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="fc66a-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="fc66a-110">Clean up deployment</span></span> 

<span data-ttu-id="fc66a-111">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación de App Service y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fc66a-111">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="fc66a-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="fc66a-112">Script explanation</span></span>

<span data-ttu-id="fc66a-113">Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web, un perfil de Traffic Manager y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fc66a-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="fc66a-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="fc66a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fc66a-115">Comando</span><span class="sxs-lookup"><span data-stu-id="fc66a-115">Command</span></span> | <span data-ttu-id="fc66a-116">Notas</span><span class="sxs-lookup"><span data-stu-id="fc66a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc66a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="fc66a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fc66a-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="fc66a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc66a-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="fc66a-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fc66a-120">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="fc66a-120">Creates an App Service plan.</span></span> <span data-ttu-id="fc66a-121">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc66a-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="fc66a-122">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="fc66a-122">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="fc66a-123">Crea una aplicación web de Azure en el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="fc66a-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="fc66a-124">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="fc66a-124">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="fc66a-125">Crea un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fc66a-125">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="fc66a-126">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="fc66a-126">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="fc66a-127">Añade un punto de conexión a un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fc66a-127">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc66a-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc66a-128">Next steps</span></span>

<span data-ttu-id="fc66a-129">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc66a-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fc66a-130">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Redes de Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc66a-130">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>
