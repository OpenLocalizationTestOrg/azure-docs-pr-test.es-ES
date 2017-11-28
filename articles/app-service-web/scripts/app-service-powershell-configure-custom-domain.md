---
title: "Ejemplo de script de Azure PowerShell: asignación de un dominio personalizado a una aplicación web | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: asignación de un dominio personalizado a una aplicación web"
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
ms.openlocfilehash: 6d25fe8098848fc69470c77e3200bee554c1f875
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="11305-103">Asignación de un dominio personalizado a una aplicación web</span><span class="sxs-lookup"><span data-stu-id="11305-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="11305-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, le asigna `www.<yourdomain>`.</span><span class="sxs-lookup"><span data-stu-id="11305-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="11305-105">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](/powershell/azure/overview) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="11305-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="11305-106">También necesita acceso a la página de configuración DNS de su registrador de dominios.</span><span class="sxs-lookup"><span data-stu-id="11305-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="11305-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="11305-107">Sample script</span></span>

<span data-ttu-id="11305-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Asignación de un dominio personalizado a una aplicación web")]</span><span class="sxs-lookup"><span data-stu-id="11305-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="11305-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="11305-109">Clean up deployment</span></span> 

<span data-ttu-id="11305-110">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="11305-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="11305-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="11305-111">Script explanation</span></span>

<span data-ttu-id="11305-112">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="11305-112">This script uses the following commands.</span></span> <span data-ttu-id="11305-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="11305-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="11305-114">Comando</span><span class="sxs-lookup"><span data-stu-id="11305-114">Command</span></span> | <span data-ttu-id="11305-115">Notas</span><span class="sxs-lookup"><span data-stu-id="11305-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="11305-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="11305-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="11305-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="11305-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="11305-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="11305-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="11305-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="11305-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="11305-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="11305-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="11305-121">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="11305-121">Creates a web app.</span></span> |
| [<span data-ttu-id="11305-122">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="11305-122">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="11305-123">Modifica un plan de App Service para cambiar su plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="11305-123">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="11305-124">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="11305-124">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="11305-125">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="11305-125">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="11305-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11305-126">Next steps</span></span>

<span data-ttu-id="11305-127">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="11305-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="11305-128">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="11305-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
