---
title: "aaaAzure ejemplo de Script de PowerShell: crear una aplicación web e implementar código desde GitHub | Documentos de Microsoft"
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
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="3d513-103">Creación de una aplicación web e implementación de código desde GitHub</span><span class="sxs-lookup"><span data-stu-id="3d513-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="3d513-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web desde un repositorio de GitHub (sin una implementación continua).</span><span class="sxs-lookup"><span data-stu-id="3d513-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="3d513-105">Para la implementación de GitHub con una implementación continua, consulte [Creación de una aplicación web con implementación continua desde GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="3d513-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="3d513-106">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d513-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="3d513-107">Además, necesita un repositorio de tooGitHub de vínculo que contiene el código de la aplicación hello web.</span><span class="sxs-lookup"><span data-stu-id="3d513-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3d513-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3d513-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3d513-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="3d513-109">Clean up deployment</span></span> 

<span data-ttu-id="3d513-110">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="3d513-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3d513-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="3d513-111">Script explanation</span></span>

<span data-ttu-id="3d513-112">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="3d513-112">This script uses hello following commands.</span></span> <span data-ttu-id="3d513-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="3d513-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3d513-114">Comando</span><span class="sxs-lookup"><span data-stu-id="3d513-114">Command</span></span> | <span data-ttu-id="3d513-115">Notas</span><span class="sxs-lookup"><span data-stu-id="3d513-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d513-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3d513-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3d513-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="3d513-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3d513-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3d513-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="3d513-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="3d513-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3d513-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3d513-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="3d513-121">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3d513-121">Creates a web app.</span></span> |
| [<span data-ttu-id="3d513-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3d513-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="3d513-123">Modifica un recurso en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3d513-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d513-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3d513-124">Next steps</span></span>

<span data-ttu-id="3d513-125">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d513-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3d513-126">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3d513-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
