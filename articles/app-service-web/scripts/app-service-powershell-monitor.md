---
title: "Ejemplo de Script de PowerShell - aaaAzure supervisar una aplicación web con registros de servidor web | Documentos de Microsoft"
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
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="f6400-103">Supervisión de una aplicación web con registros de servidor web</span><span class="sxs-lookup"><span data-stu-id="f6400-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="f6400-104">En este escenario creará un grupo de recursos, el plan de servicio de aplicaciones, la aplicación web y configurar registros de servidor web de hello web app tooenable.</span><span class="sxs-lookup"><span data-stu-id="f6400-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="f6400-105">A continuación, se descargarán los archivos de registro de hello para su revisión.</span><span class="sxs-lookup"><span data-stu-id="f6400-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="f6400-106">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="f6400-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f6400-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f6400-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f6400-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="f6400-108">Clean up deployment</span></span> 

<span data-ttu-id="f6400-109">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="f6400-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f6400-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f6400-110">Script explanation</span></span>

<span data-ttu-id="f6400-111">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="f6400-111">This script uses hello following commands.</span></span> <span data-ttu-id="f6400-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="f6400-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f6400-113">Comando</span><span class="sxs-lookup"><span data-stu-id="f6400-113">Command</span></span> | <span data-ttu-id="f6400-114">Notas</span><span class="sxs-lookup"><span data-stu-id="f6400-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f6400-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f6400-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f6400-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f6400-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f6400-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f6400-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f6400-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="f6400-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f6400-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f6400-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f6400-120">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f6400-120">Creates a web app.</span></span> |
| [<span data-ttu-id="f6400-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f6400-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f6400-122">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f6400-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="f6400-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="f6400-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="f6400-124">Obtiene las métricas de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f6400-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f6400-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6400-125">Next steps</span></span>

<span data-ttu-id="f6400-126">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f6400-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f6400-127">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f6400-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
