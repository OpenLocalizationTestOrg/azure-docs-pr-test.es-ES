---
title: "aaaAzure ejemplo de Script de PowerShell: crear una aplicación web e implementar el entorno de ensayo de tooa de código | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell de Azure - crear una aplicación web e implementar el entorno de ensayo de tooa de código"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="f4818-103">Crear una aplicación web e implementar el entorno de ensayo de tooa de código</span><span class="sxs-lookup"><span data-stu-id="f4818-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="f4818-104">Este script de ejemplo crea una aplicación web en el servicio de aplicaciones con una ranura de implementación adicionales que se denomina "ensayo" y, a continuación, implementa una toohello de aplicación de ejemplo "ensayo" ranura.</span><span class="sxs-lookup"><span data-stu-id="f4818-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="f4818-105">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="f4818-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f4818-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4818-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f4818-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="f4818-107">Clean up deployment</span></span> 

<span data-ttu-id="f4818-108">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="f4818-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f4818-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f4818-109">Script explanation</span></span>

<span data-ttu-id="f4818-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="f4818-110">This script uses hello following commands.</span></span> <span data-ttu-id="f4818-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="f4818-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f4818-112">Comando</span><span class="sxs-lookup"><span data-stu-id="f4818-112">Command</span></span> | <span data-ttu-id="f4818-113">Notas</span><span class="sxs-lookup"><span data-stu-id="f4818-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f4818-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f4818-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f4818-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f4818-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f4818-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f4818-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f4818-117">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="f4818-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f4818-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f4818-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f4818-119">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f4818-119">Creates a web app.</span></span> |
| [<span data-ttu-id="f4818-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f4818-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="f4818-121">Modifica un toochange del plan de servicio de aplicaciones en su nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="f4818-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="f4818-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="f4818-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="f4818-123">Crea un espacio de implementación para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f4818-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="f4818-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="f4818-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="f4818-125">Modifica un recurso en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4818-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="f4818-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="f4818-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="f4818-127">Cambia el espacio de implementación de una aplicación web a producción.</span><span class="sxs-lookup"><span data-stu-id="f4818-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f4818-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4818-128">Next steps</span></span>

<span data-ttu-id="f4818-129">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f4818-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f4818-130">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f4818-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
