---
title: "Ejemplo de script de Azure PowerShell: creación de una aplicación web e implementación de código en un entorno de ensayo | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: creación de una aplicación web e implementación de código en un entorno de ensayo"
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
ms.openlocfilehash: 55adc13350eb0f4711efa3c901f6e4e7755dfb27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="45798-103">Creación de una aplicación web e implementación de código en un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="45798-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="45798-104">Este script de ejemplo crea una aplicación web en App Service con una ranura de implementación adicional que se denomina "ensayo" y, a continuación, implementa una aplicación de ejemplo en la ranura "ensayo".</span><span class="sxs-lookup"><span data-stu-id="45798-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="45798-105">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](/powershell/azure/overview) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="45798-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="45798-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="45798-106">Sample script</span></span>

<span data-ttu-id="45798-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Creación de una aplicación web e implementación de código en un entorno de ensayo")]</span><span class="sxs-lookup"><span data-stu-id="45798-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="45798-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="45798-108">Clean up deployment</span></span> 

<span data-ttu-id="45798-109">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="45798-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="45798-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="45798-110">Script explanation</span></span>

<span data-ttu-id="45798-111">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="45798-111">This script uses the following commands.</span></span> <span data-ttu-id="45798-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="45798-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="45798-113">Comando</span><span class="sxs-lookup"><span data-stu-id="45798-113">Command</span></span> | <span data-ttu-id="45798-114">Notas</span><span class="sxs-lookup"><span data-stu-id="45798-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45798-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="45798-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="45798-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="45798-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="45798-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="45798-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="45798-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="45798-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="45798-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="45798-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="45798-120">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="45798-120">Creates a web app.</span></span> |
| [<span data-ttu-id="45798-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="45798-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="45798-122">Modifica un plan de App Service para cambiar su plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="45798-122">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="45798-123">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="45798-123">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="45798-124">Crea un espacio de implementación para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="45798-124">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="45798-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="45798-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="45798-126">Modifica un recurso en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="45798-126">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="45798-127">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="45798-127">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="45798-128">Cambia el espacio de implementación de una aplicación web a producción.</span><span class="sxs-lookup"><span data-stu-id="45798-128">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45798-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45798-129">Next steps</span></span>

<span data-ttu-id="45798-130">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45798-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="45798-131">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="45798-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
