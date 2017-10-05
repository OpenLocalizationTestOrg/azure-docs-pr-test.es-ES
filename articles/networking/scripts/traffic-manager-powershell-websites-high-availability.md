---
title: "Ejemplo de script de Azure PowerShell: enrutamiento del tráfico para la alta disponibilidad de las aplicaciones | Microsoft Docs"
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
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="13e45-103">Enrutamiento del tráfico para la alta disponibilidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="13e45-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="13e45-104">Este script crea un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="13e45-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="13e45-105">Traffic Manager dirige el tráfico a la aplicación en una región como la región primaria y a la región secundaria cuando no está disponible la aplicación en la región primaria.</span><span class="sxs-lookup"><span data-stu-id="13e45-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="13e45-106">Antes de ejecutar el script, debe cambiar los valores de MyWebApp, MyWebAppL1 y MyWebAppL2 a valores únicos en todo Azure.</span><span class="sxs-lookup"><span data-stu-id="13e45-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="13e45-107">Después de ejecutar el script, puede tener acceso a la aplicación en la región primaria con la dirección URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="13e45-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="13e45-108">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="13e45-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="13e45-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="13e45-109">Sample script</span></span>

<span data-ttu-id="13e45-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Enrutamiento del tráfico para la alta disponibilidad de las aplicaciones")]</span><span class="sxs-lookup"><span data-stu-id="13e45-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="13e45-111">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="13e45-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="13e45-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="13e45-112">Script explanation</span></span>

<span data-ttu-id="13e45-113">Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web, un perfil de Traffic Manager y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="13e45-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="13e45-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="13e45-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="13e45-115">Comando</span><span class="sxs-lookup"><span data-stu-id="13e45-115">Command</span></span> | <span data-ttu-id="13e45-116">Notas</span><span class="sxs-lookup"><span data-stu-id="13e45-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="13e45-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="13e45-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="13e45-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="13e45-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="13e45-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="13e45-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="13e45-120">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="13e45-120">Creates an App Service plan.</span></span> <span data-ttu-id="13e45-121">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="13e45-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="13e45-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="13e45-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="13e45-123">Crea una aplicación web de Azure en el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="13e45-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="13e45-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="13e45-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="13e45-125">Crea una aplicación web de Azure en el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="13e45-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="13e45-126">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="13e45-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="13e45-127">Crea un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="13e45-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="13e45-128">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="13e45-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="13e45-129">Añade un punto de conexión a un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="13e45-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="13e45-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13e45-130">Next steps</span></span>

<span data-ttu-id="13e45-131">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="13e45-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="13e45-132">En la [documentación de la información general de redes de Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json) puede encontrar ejemplos adicionales de script de PowerShell de redes.</span><span class="sxs-lookup"><span data-stu-id="13e45-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>