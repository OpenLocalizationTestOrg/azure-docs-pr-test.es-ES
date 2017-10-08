---
title: "Ejemplo de Script de PowerShell - aaaAzure conectar una cuenta de almacenamiento de tooa de aplicación web | Documentos de Microsoft"
description: "Script de Azure PowerShell de ejemplo: conectar una cuenta de almacenamiento de tooa de aplicación web"
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
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="16e2f-103">Conectarse a una cuenta de almacenamiento de tooa de aplicación web</span><span class="sxs-lookup"><span data-stu-id="16e2f-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="16e2f-104">En este escenario, aprenderá cómo toocreate una cuenta de almacenamiento de Azure y un Azure aplicación web.</span><span class="sxs-lookup"><span data-stu-id="16e2f-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="16e2f-105">A continuación, vinculará Hola almacenamiento cuenta toohello web app con la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16e2f-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="16e2f-106">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="16e2f-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="16e2f-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="16e2f-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="16e2f-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="16e2f-108">Clean up deployment</span></span> 

<span data-ttu-id="16e2f-109">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="16e2f-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="16e2f-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="16e2f-110">Script explanation</span></span>

<span data-ttu-id="16e2f-111">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="16e2f-111">This script uses hello following commands.</span></span> <span data-ttu-id="16e2f-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="16e2f-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="16e2f-113">Comando</span><span class="sxs-lookup"><span data-stu-id="16e2f-113">Command</span></span> | <span data-ttu-id="16e2f-114">Notas</span><span class="sxs-lookup"><span data-stu-id="16e2f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="16e2f-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="16e2f-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="16e2f-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="16e2f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="16e2f-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="16e2f-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="16e2f-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="16e2f-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="16e2f-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="16e2f-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="16e2f-120">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="16e2f-120">Creates a web app.</span></span> |
| [<span data-ttu-id="16e2f-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="16e2f-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="16e2f-122">Crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="16e2f-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="16e2f-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="16e2f-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="16e2f-124">Obtiene las claves de acceso de Hola para una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="16e2f-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="16e2f-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="16e2f-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="16e2f-126">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="16e2f-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="16e2f-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16e2f-127">Next steps</span></span>

<span data-ttu-id="16e2f-128">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="16e2f-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="16e2f-129">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="16e2f-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
