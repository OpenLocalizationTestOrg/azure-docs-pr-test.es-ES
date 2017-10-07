---
title: "Ejemplo de Script de PowerShell - aaaAzure enlazar una aplicación de web de tooa de certificado SSL personalizada | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - enlace una aplicación de web de tooa de certificado SSL personalizada"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="7b93d-103">Enlazar una aplicación de web de tooa de certificado SSL personalizada</span><span class="sxs-lookup"><span data-stu-id="7b93d-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="7b93d-104">Este script de ejemplo crea una aplicación web en el servicio de aplicaciones con sus recursos relacionados, a continuación, enlaza el certificado SSL de Hola de un tooit de nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="7b93d-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="7b93d-105">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7b93d-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="7b93d-106">Asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b93d-106">Also, ensure that:</span></span>

- <span data-ttu-id="7b93d-107">Se ha creado una conexión con Azure mediante hello `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="7b93d-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="7b93d-108">Tiene la página de configuración de DNS del registrador de dominios de acceso tooyour.</span><span class="sxs-lookup"><span data-stu-id="7b93d-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="7b93d-109">Tiene un válido. Archivo PFX y su contraseña para hello SSL certificado que desee tooupload y enlazar.</span><span class="sxs-lookup"><span data-stu-id="7b93d-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7b93d-110">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7b93d-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7b93d-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="7b93d-111">Clean up deployment</span></span> 

<span data-ttu-id="7b93d-112">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="7b93d-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7b93d-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="7b93d-113">Script explanation</span></span>

<span data-ttu-id="7b93d-114">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="7b93d-114">This script uses hello following commands.</span></span> <span data-ttu-id="7b93d-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="7b93d-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7b93d-116">Comando</span><span class="sxs-lookup"><span data-stu-id="7b93d-116">Command</span></span> | <span data-ttu-id="7b93d-117">Notas</span><span class="sxs-lookup"><span data-stu-id="7b93d-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7b93d-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7b93d-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7b93d-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="7b93d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7b93d-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7b93d-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7b93d-121">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="7b93d-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7b93d-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7b93d-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7b93d-123">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7b93d-123">Creates a web app.</span></span> |
| [<span data-ttu-id="7b93d-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7b93d-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="7b93d-125">Modifica un toochange del plan de servicio de aplicaciones en su nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="7b93d-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="7b93d-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7b93d-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="7b93d-127">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7b93d-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="7b93d-128">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="7b93d-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="7b93d-129">Crea un enlace de certificado SSL para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7b93d-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7b93d-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b93d-130">Next steps</span></span>

<span data-ttu-id="7b93d-131">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7b93d-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7b93d-132">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7b93d-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
