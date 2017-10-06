---
title: "aaaAzure ejemplo de Script de PowerShell - enrutar el tráfico para lograr alta disponibilidad de aplicaciones | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: enrutamiento del tráfico para la alta disponibilidad de las aplicaciones"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="1614a-103">Enrutamiento del tráfico para la alta disponibilidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1614a-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="1614a-104">Este script crea un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="1614a-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="1614a-105">Administrador de tráfico dirige la aplicación de toohello de tráfico en una región como región principal de Hola y región secundaria toohello cuando la aplicación hello en la región principal de hello no está disponible.</span><span class="sxs-lookup"><span data-stu-id="1614a-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="1614a-106">Antes de ejecutar script de Hola, debe cambiar Hola MyWebApp, MyWebAppL1 y MyWebAppL2 valores toounique valores a través de Azure.</span><span class="sxs-lookup"><span data-stu-id="1614a-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="1614a-107">Después de ejecutar el script de Hola, puede tener acceso a la aplicación hello en la región principal de hello con hello mywebapp.trafficmanager.net de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="1614a-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="1614a-108">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="1614a-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1614a-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1614a-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="1614a-110">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="1614a-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="1614a-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="1614a-111">Script explanation</span></span>

<span data-ttu-id="1614a-112">Este script utiliza Hola después comandos toocreate un grupo de recursos, la aplicación web, el perfil del Administrador de tráfico y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="1614a-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="1614a-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="1614a-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1614a-114">Comando</span><span class="sxs-lookup"><span data-stu-id="1614a-114">Command</span></span> | <span data-ttu-id="1614a-115">Notas</span><span class="sxs-lookup"><span data-stu-id="1614a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1614a-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1614a-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="1614a-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="1614a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1614a-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="1614a-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1614a-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="1614a-119">Creates an App Service plan.</span></span> <span data-ttu-id="1614a-120">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="1614a-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="1614a-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1614a-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1614a-122">Crea una aplicación web de Azure en hello plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1614a-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="1614a-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="1614a-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="1614a-124">Crea una aplicación web de Azure en hello plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1614a-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="1614a-125">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="1614a-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="1614a-126">Crea un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="1614a-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="1614a-127">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="1614a-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="1614a-128">Agrega un perfil de Traffic Manager de Azure tooan de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="1614a-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1614a-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1614a-129">Next steps</span></span>

<span data-ttu-id="1614a-130">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1614a-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="1614a-131">Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1614a-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
