---
title: "Ejemplo de script de Azure PowerShell: escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 9acd1cf4d1a5705811c4dedc545505ec0ac55fc7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="d5a24-103">Escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="d5a24-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="d5a24-104">En este escenario, creará un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d5a24-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="d5a24-105">Una vez completado el ejercicio, tendrá una arquitectura de alta disponibilidad que garantizará la disponibilidad global de la aplicación web en función de la latencia de red más baja.</span><span class="sxs-lookup"><span data-stu-id="d5a24-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="d5a24-106">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](/powershell/azure/overview) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="d5a24-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d5a24-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d5a24-107">Sample script</span></span>

<span data-ttu-id="d5a24-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad")]</span><span class="sxs-lookup"><span data-stu-id="d5a24-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d5a24-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="d5a24-109">Clean up deployment</span></span> 

<span data-ttu-id="d5a24-110">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d5a24-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d5a24-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="d5a24-111">Script explanation</span></span>

<span data-ttu-id="d5a24-112">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="d5a24-112">This script uses the following commands.</span></span> <span data-ttu-id="d5a24-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="d5a24-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d5a24-114">Comando</span><span class="sxs-lookup"><span data-stu-id="d5a24-114">Command</span></span> | <span data-ttu-id="d5a24-115">Notas</span><span class="sxs-lookup"><span data-stu-id="d5a24-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d5a24-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d5a24-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d5a24-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d5a24-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d5a24-118">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="d5a24-118">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="d5a24-119">Crea un perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d5a24-119">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="d5a24-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d5a24-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d5a24-121">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="d5a24-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d5a24-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d5a24-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d5a24-123">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d5a24-123">Creates a web app.</span></span> |
| [<span data-ttu-id="d5a24-124">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="d5a24-124">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="d5a24-125">Crea un punto de conexión en un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d5a24-125">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d5a24-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5a24-126">Next steps</span></span>

<span data-ttu-id="d5a24-127">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d5a24-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d5a24-128">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d5a24-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
