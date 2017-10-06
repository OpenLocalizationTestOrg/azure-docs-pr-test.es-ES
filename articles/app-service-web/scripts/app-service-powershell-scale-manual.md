---
title: "Ejemplo de Script de PowerShell - aaaAzure escalar una aplicación web manualmente | Documentos de Microsoft"
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
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="39c7b-103">Escalado manual de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="39c7b-103">Scale a web app manually</span></span>

<span data-ttu-id="39c7b-104">En este escenario, aprenderá toocreate un grupo de recursos, aplicación de servicio web y el plan de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="39c7b-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="39c7b-105">A continuación, se escalará Hola Plan de servicio de aplicaciones desde una instancia de toomultiple de instancia única.</span><span class="sxs-lookup"><span data-stu-id="39c7b-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="39c7b-106">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="39c7b-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="39c7b-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="39c7b-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="39c7b-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="39c7b-108">Clean up deployment</span></span> 

<span data-ttu-id="39c7b-109">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="39c7b-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="39c7b-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="39c7b-110">Script explanation</span></span>

<span data-ttu-id="39c7b-111">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="39c7b-111">This script uses hello following commands.</span></span> <span data-ttu-id="39c7b-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="39c7b-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="39c7b-113">Comando</span><span class="sxs-lookup"><span data-stu-id="39c7b-113">Command</span></span> | <span data-ttu-id="39c7b-114">Notas</span><span class="sxs-lookup"><span data-stu-id="39c7b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="39c7b-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="39c7b-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="39c7b-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="39c7b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="39c7b-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="39c7b-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="39c7b-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="39c7b-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="39c7b-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="39c7b-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="39c7b-120">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="39c7b-120">Creates a web app.</span></span> |
| [<span data-ttu-id="39c7b-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="39c7b-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="39c7b-122">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="39c7b-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="39c7b-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39c7b-123">Next steps</span></span>

<span data-ttu-id="39c7b-124">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="39c7b-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="39c7b-125">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="39c7b-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
