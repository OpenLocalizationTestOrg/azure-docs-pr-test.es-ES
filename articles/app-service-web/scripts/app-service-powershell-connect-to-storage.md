---
title: "Ejemplo de script de Azure PowerShell: conexión de una aplicación web a una cuenta de almacenamiento | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: conexión de una aplicación web a una cuenta de almacenamiento"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="629cc-103">Conexión de una aplicación web a una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="629cc-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="629cc-104">En este escenario aprenderá a crear una cuenta de Azure Storage y una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="629cc-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="629cc-105">Y, después, vinculará la cuenta de almacenamiento a la aplicación web mediante la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="629cc-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="629cc-106">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](/powershell/azure/overview) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="629cc-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="629cc-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="629cc-107">Sample script</span></span>

<span data-ttu-id="629cc-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Conexión de una aplicación web a una cuenta de almacenamiento")]</span><span class="sxs-lookup"><span data-stu-id="629cc-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="629cc-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="629cc-109">Clean up deployment</span></span> 

<span data-ttu-id="629cc-110">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, la aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="629cc-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="629cc-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="629cc-111">Script explanation</span></span>

<span data-ttu-id="629cc-112">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="629cc-112">This script uses the following commands.</span></span> <span data-ttu-id="629cc-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="629cc-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="629cc-114">Comando</span><span class="sxs-lookup"><span data-stu-id="629cc-114">Command</span></span> | <span data-ttu-id="629cc-115">Notas</span><span class="sxs-lookup"><span data-stu-id="629cc-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="629cc-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="629cc-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="629cc-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="629cc-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="629cc-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="629cc-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="629cc-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="629cc-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="629cc-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="629cc-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="629cc-121">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="629cc-121">Creates a web app.</span></span> |
| [<span data-ttu-id="629cc-122">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="629cc-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="629cc-123">Crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="629cc-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="629cc-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="629cc-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="629cc-125">Obtiene las claves de acceso de una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="629cc-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="629cc-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="629cc-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="629cc-127">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="629cc-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="629cc-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="629cc-128">Next steps</span></span>

<span data-ttu-id="629cc-129">Para más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="629cc-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="629cc-130">Puede encontrar ejemplos de Azure PowerShell para Azure App Service Web Apps en los [ejemplos de PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="629cc-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
