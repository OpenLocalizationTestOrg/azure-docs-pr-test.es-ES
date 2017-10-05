---
title: "Ejemplo de script de Azure PowerShell: creación de una aplicación web e implementación de código desde GitHub | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: creación de una aplicación web e implementación de código desde GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1f7fc21dc12c334f5d347ae9918bd62945bede64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="4b249-103">Creación de una aplicación web e implementación de código desde GitHub</span><span class="sxs-lookup"><span data-stu-id="4b249-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="4b249-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web desde un repositorio de GitHub (sin una implementación continua).</span><span class="sxs-lookup"><span data-stu-id="4b249-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="4b249-105">Para la implementación de GitHub con una implementación continua, consulte [Creación de una aplicación web con implementación continua desde GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="4b249-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="4b249-106">Si es necesario, instale PowerShell con la instrucción que se encuentra en la [Guía de instalación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4b249-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="4b249-107">Además, necesita un vínculo al repositorio de GitHub que contiene el código de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4b249-107">Also, you need a link to GitHub repository that contains the web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="4b249-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4b249-108">Sample script</span></span>

<span data-ttu-id="4b249-109">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Creación de una aplicación web e implementación de código desde GitHub")]</span><span class="sxs-lookup"><span data-stu-id="4b249-109">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4b249-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="4b249-110">Clean up deployment</span></span> 

<span data-ttu-id="4b249-111">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4b249-111">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4b249-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="4b249-112">Script explanation</span></span>

<span data-ttu-id="4b249-113">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="4b249-113">This script uses the following commands.</span></span> <span data-ttu-id="4b249-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="4b249-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4b249-115">Comando</span><span class="sxs-lookup"><span data-stu-id="4b249-115">Command</span></span> | <span data-ttu-id="4b249-116">Notas</span><span class="sxs-lookup"><span data-stu-id="4b249-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4b249-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4b249-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4b249-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="4b249-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4b249-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4b249-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4b249-120">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="4b249-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4b249-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4b249-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4b249-122">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4b249-122">Creates a web app.</span></span> |
| [<span data-ttu-id="4b249-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4b249-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="4b249-124">Modifica un recurso en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4b249-124">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4b249-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b249-125">Next steps</span></span>

<span data-ttu-id="4b249-126">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4b249-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4b249-127">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4b249-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
