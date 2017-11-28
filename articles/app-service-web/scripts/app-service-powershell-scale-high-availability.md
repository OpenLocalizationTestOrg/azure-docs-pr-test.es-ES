---
title: "Ejemplo de Script de PowerShell - aaaAzure escalar una aplicación web en todo el mundo con una arquitectura de alta disponibilidad | Documentos de Microsoft"
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
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="25223-103">Escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="25223-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="25223-104">En este escenario, creará un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="25223-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="25223-105">Cuando se complete el ejercicio de hello tendrá una alta disponibilidad arquitectura que permite que proporciona disponibilidad global de la aplicación web en función de la latencia de red más baja de Hola.</span><span class="sxs-lookup"><span data-stu-id="25223-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="25223-106">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="25223-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="25223-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="25223-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="25223-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="25223-108">Clean up deployment</span></span> 

<span data-ttu-id="25223-109">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="25223-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="25223-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="25223-110">Script explanation</span></span>

<span data-ttu-id="25223-111">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="25223-111">This script uses hello following commands.</span></span> <span data-ttu-id="25223-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="25223-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="25223-113">Comando</span><span class="sxs-lookup"><span data-stu-id="25223-113">Command</span></span> | <span data-ttu-id="25223-114">Notas</span><span class="sxs-lookup"><span data-stu-id="25223-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="25223-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="25223-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="25223-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="25223-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="25223-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="25223-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="25223-118">Crea un perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="25223-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="25223-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="25223-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="25223-120">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="25223-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="25223-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="25223-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="25223-122">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="25223-122">Creates a web app.</span></span> |
| [<span data-ttu-id="25223-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="25223-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="25223-124">Crea un punto de conexión en un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="25223-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="25223-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25223-125">Next steps</span></span>

<span data-ttu-id="25223-126">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25223-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="25223-127">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="25223-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
