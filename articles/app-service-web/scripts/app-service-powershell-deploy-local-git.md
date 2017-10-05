---
title: "Ejemplo de script de Azure PowerShell: creación de una aplicación web e implementación de código desde un repositorio local de Git | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: creación de una aplicación web e implementación de código desde un repositorio local de Git"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="5e8f3-103">Creación de una aplicación web e implementación de código desde un repositorio local de Git</span><span class="sxs-lookup"><span data-stu-id="5e8f3-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="5e8f3-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web en un repositorio local de GitHub.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="5e8f3-105">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](/powershell/azure/overview) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="5e8f3-106">Además, el código de aplicación debe confirmarse en un repositorio de Git local.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="5e8f3-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5e8f3-107">Sample script</span></span>

<span data-ttu-id="5e8f3-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Creación de una aplicación web e implementación de código desde un repositorio local de Git")]</span><span class="sxs-lookup"><span data-stu-id="5e8f3-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5e8f3-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="5e8f3-109">Clean up deployment</span></span> 

<span data-ttu-id="5e8f3-110">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="5e8f3-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5e8f3-111">Script explanation</span></span>

<span data-ttu-id="5e8f3-112">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-112">This script uses the following commands.</span></span> <span data-ttu-id="5e8f3-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5e8f3-114">Comando</span><span class="sxs-lookup"><span data-stu-id="5e8f3-114">Command</span></span> | <span data-ttu-id="5e8f3-115">Notas</span><span class="sxs-lookup"><span data-stu-id="5e8f3-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e8f3-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e8f3-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5e8f3-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5e8f3-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5e8f3-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="5e8f3-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="5e8f3-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5e8f3-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5e8f3-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="5e8f3-121">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-121">Creates a web app.</span></span> |
| [<span data-ttu-id="5e8f3-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5e8f3-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="5e8f3-123">Modifica un recurso en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="5e8f3-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="5e8f3-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="5e8f3-125">Obtenga el perfil de publicación de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5e8f3-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e8f3-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5e8f3-126">Next steps</span></span>

<span data-ttu-id="5e8f3-127">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e8f3-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5e8f3-128">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5e8f3-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
