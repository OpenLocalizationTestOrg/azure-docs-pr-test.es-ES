---
title: Ejemplo de Script de PowerShell - carga archivos tooa web app mediante FTP aaaAzure | Documentos de Microsoft
description: Ejemplo de Script de PowerShell Azure - carga archivos tooa web app mediante FTP
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="37a3d-103">Cargar archivos tooa web app mediante FTP</span><span class="sxs-lookup"><span data-stu-id="37a3d-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="37a3d-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web mediante FTP (a través de [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="37a3d-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="37a3d-105">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="37a3d-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="37a3d-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="37a3d-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="37a3d-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="37a3d-107">Clean up deployment</span></span> 

<span data-ttu-id="37a3d-108">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="37a3d-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="37a3d-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="37a3d-109">Script explanation</span></span>

<span data-ttu-id="37a3d-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="37a3d-110">This script uses hello following commands.</span></span> <span data-ttu-id="37a3d-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="37a3d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="37a3d-112">Comando</span><span class="sxs-lookup"><span data-stu-id="37a3d-112">Command</span></span> | <span data-ttu-id="37a3d-113">Notas</span><span class="sxs-lookup"><span data-stu-id="37a3d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="37a3d-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="37a3d-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="37a3d-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="37a3d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="37a3d-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="37a3d-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="37a3d-117">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="37a3d-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="37a3d-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="37a3d-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="37a3d-119">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="37a3d-119">Creates a web app.</span></span> |
| [<span data-ttu-id="37a3d-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="37a3d-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="37a3d-121">Obtenga el perfil de publicación de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="37a3d-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="37a3d-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37a3d-122">Next steps</span></span>

<span data-ttu-id="37a3d-123">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="37a3d-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="37a3d-124">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="37a3d-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
