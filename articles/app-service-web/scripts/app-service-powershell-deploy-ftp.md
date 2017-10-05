---
title: "Ejemplo de script de Azure PowerShell Azure: carga de archivos en una aplicación web con FTP | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell Azure: carga de archivos en una aplicación web con FTP"
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
ms.openlocfilehash: 96b99110b63b037746fcc40eb15db5d718eb71a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="a0d77-103">Carga de archivos en una aplicación web con FTP</span><span class="sxs-lookup"><span data-stu-id="a0d77-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="a0d77-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web mediante FTP (a través de [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a0d77-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="a0d77-105">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](/powershell/azure/overview) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d77-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a0d77-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a0d77-106">Sample script</span></span>

<span data-ttu-id="a0d77-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Carga de archivos en una aplicación web con FTP")]</span><span class="sxs-lookup"><span data-stu-id="a0d77-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a0d77-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="a0d77-108">Clean up deployment</span></span> 

<span data-ttu-id="a0d77-109">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="a0d77-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a0d77-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="a0d77-110">Script explanation</span></span>

<span data-ttu-id="a0d77-111">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="a0d77-111">This script uses the following commands.</span></span> <span data-ttu-id="a0d77-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="a0d77-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a0d77-113">Comando</span><span class="sxs-lookup"><span data-stu-id="a0d77-113">Command</span></span> | <span data-ttu-id="a0d77-114">Notas</span><span class="sxs-lookup"><span data-stu-id="a0d77-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a0d77-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a0d77-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a0d77-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="a0d77-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a0d77-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a0d77-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a0d77-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="a0d77-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a0d77-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a0d77-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a0d77-120">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a0d77-120">Creates a web app.</span></span> |
| [<span data-ttu-id="a0d77-121">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="a0d77-121">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="a0d77-122">Obtenga el perfil de publicación de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a0d77-122">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a0d77-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a0d77-123">Next steps</span></span>

<span data-ttu-id="a0d77-124">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0d77-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a0d77-125">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a0d77-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
