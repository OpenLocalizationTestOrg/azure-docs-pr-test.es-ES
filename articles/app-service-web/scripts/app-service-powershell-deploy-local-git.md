---
title: "aaaAzure ejemplo de Script de PowerShell: crear una aplicación web e implementar código desde un repositorio Git local | Documentos de Microsoft"
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
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="59eb4-103">Creación de una aplicación web e implementación de código desde un repositorio local de Git</span><span class="sxs-lookup"><span data-stu-id="59eb4-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="59eb4-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web en un repositorio local de GitHub.</span><span class="sxs-lookup"><span data-stu-id="59eb4-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="59eb4-105">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="59eb4-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="59eb4-106">Además, el código de aplicación debe toobe confirmado en un repositorio Git local.</span><span class="sxs-lookup"><span data-stu-id="59eb4-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="59eb4-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="59eb4-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="59eb4-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="59eb4-108">Clean up deployment</span></span> 

<span data-ttu-id="59eb4-109">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="59eb4-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="59eb4-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="59eb4-110">Script explanation</span></span>

<span data-ttu-id="59eb4-111">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="59eb4-111">This script uses hello following commands.</span></span> <span data-ttu-id="59eb4-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="59eb4-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="59eb4-113">Comando</span><span class="sxs-lookup"><span data-stu-id="59eb4-113">Command</span></span> | <span data-ttu-id="59eb4-114">Notas</span><span class="sxs-lookup"><span data-stu-id="59eb4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="59eb4-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="59eb4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="59eb4-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="59eb4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="59eb4-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="59eb4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="59eb4-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="59eb4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="59eb4-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="59eb4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="59eb4-120">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="59eb4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="59eb4-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="59eb4-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="59eb4-122">Modifica un recurso en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="59eb4-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="59eb4-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="59eb4-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="59eb4-124">Obtenga el perfil de publicación de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="59eb4-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="59eb4-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59eb4-125">Next steps</span></span>

<span data-ttu-id="59eb4-126">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="59eb4-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="59eb4-127">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="59eb4-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
