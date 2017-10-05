---
title: "Ejemplo de script de Azure PowerShell: escalado manual de una aplicación web mediante | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: escalado manual de una aplicación web mediante"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="5a7c2-103">Escalado manual de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="5a7c2-103">Scale a web app manually</span></span>

<span data-ttu-id="5a7c2-104">En este escenario, aprenderá a crear un grupo de recursos, un plan de App Service y una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="5a7c2-105">A continuación, escalará el plan de App Service desde una sola instancia a varias instancias.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="5a7c2-106">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](/powershell/azure/overview) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="5a7c2-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5a7c2-107">Sample script</span></span>

<span data-ttu-id="5a7c2-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Escalado manual de una aplicación web")]</span><span class="sxs-lookup"><span data-stu-id="5a7c2-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5a7c2-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="5a7c2-109">Clean up deployment</span></span> 

<span data-ttu-id="5a7c2-110">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="5a7c2-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5a7c2-111">Script explanation</span></span>

<span data-ttu-id="5a7c2-112">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-112">This script uses the following commands.</span></span> <span data-ttu-id="5a7c2-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5a7c2-114">Comando</span><span class="sxs-lookup"><span data-stu-id="5a7c2-114">Command</span></span> | <span data-ttu-id="5a7c2-115">Notas</span><span class="sxs-lookup"><span data-stu-id="5a7c2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5a7c2-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5a7c2-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5a7c2-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5a7c2-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5a7c2-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="5a7c2-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="5a7c2-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5a7c2-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5a7c2-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="5a7c2-121">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-121">Creates a web app.</span></span> |
| [<span data-ttu-id="5a7c2-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5a7c2-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="5a7c2-123">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5a7c2-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a7c2-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a7c2-124">Next steps</span></span>

<span data-ttu-id="5a7c2-125">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5a7c2-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5a7c2-126">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5a7c2-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
