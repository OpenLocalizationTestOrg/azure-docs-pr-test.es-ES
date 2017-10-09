---
title: "Ejemplo de Script de PowerShell - aaaAzure asignar una aplicación web de tooa de dominio personalizado | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - asignar una aplicación web de tooa de dominio personalizado"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="46f04-103">Asignar una aplicación web de tooa de dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="46f04-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="46f04-104">Este script de ejemplo crea una aplicación web en el servicio de aplicaciones con sus recursos relacionados y, a continuación, asigna `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="46f04-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="46f04-105">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="46f04-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="46f04-106">Además, deberá página de configuración de DNS del registrador de dominios de toohave acceso tooyour.</span><span class="sxs-lookup"><span data-stu-id="46f04-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="46f04-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="46f04-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="46f04-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="46f04-108">Clean up deployment</span></span> 

<span data-ttu-id="46f04-109">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="46f04-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="46f04-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="46f04-110">Script explanation</span></span>

<span data-ttu-id="46f04-111">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="46f04-111">This script uses hello following commands.</span></span> <span data-ttu-id="46f04-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="46f04-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="46f04-113">Comando</span><span class="sxs-lookup"><span data-stu-id="46f04-113">Command</span></span> | <span data-ttu-id="46f04-114">Notas</span><span class="sxs-lookup"><span data-stu-id="46f04-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="46f04-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="46f04-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="46f04-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="46f04-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="46f04-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="46f04-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="46f04-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="46f04-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="46f04-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="46f04-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="46f04-120">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="46f04-120">Creates a web app.</span></span> |
| [<span data-ttu-id="46f04-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="46f04-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="46f04-122">Modifica un toochange del plan de servicio de aplicaciones en su nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="46f04-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="46f04-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="46f04-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="46f04-124">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="46f04-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="46f04-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46f04-125">Next steps</span></span>

<span data-ttu-id="46f04-126">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="46f04-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="46f04-127">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="46f04-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
