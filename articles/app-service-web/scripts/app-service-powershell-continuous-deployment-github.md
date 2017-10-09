---
title: "aaaAzure ejemplo de Script de PowerShell: crear una aplicación web con una implementación continua desde GitHub | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: creación de una aplicación web con implementación continua desde GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="8fab0-103">Creación de una aplicación web con implementación continua desde GitHub</span><span class="sxs-lookup"><span data-stu-id="8fab0-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="8fab0-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, configura la implementación continua desde un repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="8fab0-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="8fab0-105">Para la implementación de GitHub sin una implementación continua, consulte [Creación de una aplicación web e implementación de código desde GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="8fab0-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="8fab0-106">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8fab0-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="8fab0-107">Asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8fab0-107">Also, ensure that:</span></span>

- <span data-ttu-id="8fab0-108">Se ha creado una conexión con Azure mediante hello `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="8fab0-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="8fab0-109">código de la aplicación Hello está en un repositorio de GitHub público o privado que usted es el propietario.</span><span class="sxs-lookup"><span data-stu-id="8fab0-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="8fab0-110">Ha [creado un token de acceso en su cuenta de GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="8fab0-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="8fab0-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8fab0-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8fab0-112">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="8fab0-112">Clean up deployment</span></span> 

<span data-ttu-id="8fab0-113">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="8fab0-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="8fab0-114">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="8fab0-114">Script explanation</span></span>

<span data-ttu-id="8fab0-115">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="8fab0-115">This script uses hello following commands.</span></span> <span data-ttu-id="8fab0-116">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="8fab0-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8fab0-117">Comando</span><span class="sxs-lookup"><span data-stu-id="8fab0-117">Command</span></span> | <span data-ttu-id="8fab0-118">Notas</span><span class="sxs-lookup"><span data-stu-id="8fab0-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8fab0-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8fab0-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8fab0-120">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="8fab0-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8fab0-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8fab0-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="8fab0-122">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="8fab0-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8fab0-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8fab0-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="8fab0-124">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8fab0-124">Creates a web app.</span></span> |
| [<span data-ttu-id="8fab0-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="8fab0-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="8fab0-126">Modifica un recurso en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8fab0-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8fab0-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8fab0-127">Next steps</span></span>

<span data-ttu-id="8fab0-128">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8fab0-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8fab0-129">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8fab0-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
