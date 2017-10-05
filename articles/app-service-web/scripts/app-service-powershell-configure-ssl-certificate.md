---
title: "Ejemplo de script de Azure PowerShell: enlace de un certificado SSL personalizado a una aplicación web | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: enlace de un certificado SSL personalizado a una aplicación web"
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
ms.openlocfilehash: de8deccadcd9571be75447a117888bf2b3f571a0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="d1687-103">Enlace de un certificado SSL personalizado a una aplicación web</span><span class="sxs-lookup"><span data-stu-id="d1687-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="d1687-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, luego, enlaza el certificado SSL de un nombre de dominio personalizado a ella.</span><span class="sxs-lookup"><span data-stu-id="d1687-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> 

<span data-ttu-id="d1687-105">Si es necesario, instale PowerShell con la instrucción que se encuentra en la [Guía de instalación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1687-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="d1687-106">Asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d1687-106">Also, ensure that:</span></span>

- <span data-ttu-id="d1687-107">Se ha creado una conexión con Azure mediante el comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="d1687-107">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="d1687-108">Tiene acceso a la página de configuración DNS de su registrador de dominios.</span><span class="sxs-lookup"><span data-stu-id="d1687-108">You have access to your domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="d1687-109">Tiene un archivo PFX válido y su contraseña para el certificado SSL que desea cargar y enlazar.</span><span class="sxs-lookup"><span data-stu-id="d1687-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d1687-110">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d1687-110">Sample script</span></span>

<span data-ttu-id="d1687-111">[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Enlace de un certificado SSL personalizado a una aplicación web")]</span><span class="sxs-lookup"><span data-stu-id="d1687-111">[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d1687-112">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="d1687-112">Clean up deployment</span></span> 

<span data-ttu-id="d1687-113">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d1687-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d1687-114">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="d1687-114">Script explanation</span></span>

<span data-ttu-id="d1687-115">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="d1687-115">This script uses the following commands.</span></span> <span data-ttu-id="d1687-116">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="d1687-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d1687-117">Comando</span><span class="sxs-lookup"><span data-stu-id="d1687-117">Command</span></span> | <span data-ttu-id="d1687-118">Notas</span><span class="sxs-lookup"><span data-stu-id="d1687-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d1687-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d1687-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d1687-120">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d1687-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d1687-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d1687-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d1687-122">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="d1687-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d1687-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d1687-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d1687-124">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d1687-124">Creates a web app.</span></span> |
| [<span data-ttu-id="d1687-125">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d1687-125">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="d1687-126">Modifica un plan de App Service para cambiar su plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="d1687-126">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="d1687-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d1687-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="d1687-128">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d1687-128">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="d1687-129">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="d1687-129">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="d1687-130">Crea un enlace de certificado SSL para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d1687-130">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d1687-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1687-131">Next steps</span></span>

<span data-ttu-id="d1687-132">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1687-132">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d1687-133">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d1687-133">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
