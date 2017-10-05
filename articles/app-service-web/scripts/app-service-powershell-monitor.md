---
title: "Ejemplo de script de Azure PowerShell: supervisión de una aplicación web con registros de servidor web | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: supervisión de una aplicación web con registros de servidor web"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 34a3dd318cb9896342fce870922ecd113b3ed08d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="fbe02-103">Supervisión de una aplicación web con registros de servidor web</span><span class="sxs-lookup"><span data-stu-id="fbe02-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="fbe02-104">En este escenario, creará un grupo de recursos, un plan de App Service y una aplicación web, además de configurar la aplicación web para habilitar los registros del servidor web.</span><span class="sxs-lookup"><span data-stu-id="fbe02-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="fbe02-105">A continuación, descargará los archivos de registro para revisarlos.</span><span class="sxs-lookup"><span data-stu-id="fbe02-105">You will then download the log files for review.</span></span>

<span data-ttu-id="fbe02-106">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](/powershell/azure/overview) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe02-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="fbe02-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="fbe02-107">Sample script</span></span>

<span data-ttu-id="fbe02-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Supervisión de una aplicación web con registros de servidor web")]</span><span class="sxs-lookup"><span data-stu-id="fbe02-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fbe02-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="fbe02-109">Clean up deployment</span></span> 

<span data-ttu-id="fbe02-110">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fbe02-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="fbe02-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="fbe02-111">Script explanation</span></span>

<span data-ttu-id="fbe02-112">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="fbe02-112">This script uses the following commands.</span></span> <span data-ttu-id="fbe02-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="fbe02-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fbe02-114">Comando</span><span class="sxs-lookup"><span data-stu-id="fbe02-114">Command</span></span> | <span data-ttu-id="fbe02-115">Notas</span><span class="sxs-lookup"><span data-stu-id="fbe02-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fbe02-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fbe02-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fbe02-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="fbe02-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fbe02-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="fbe02-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="fbe02-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="fbe02-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="fbe02-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="fbe02-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="fbe02-121">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="fbe02-121">Creates a web app.</span></span> |
| [<span data-ttu-id="fbe02-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="fbe02-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="fbe02-123">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="fbe02-123">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="fbe02-124">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="fbe02-124">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="fbe02-125">Obtiene las métricas de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="fbe02-125">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fbe02-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbe02-126">Next steps</span></span>

<span data-ttu-id="fbe02-127">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbe02-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fbe02-128">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fbe02-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
