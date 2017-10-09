---
title: 'aaaAzure ejemplo de Script de PowerShell: conectarse a una base de datos SQL de web app tooa | Documentos de Microsoft'
description: "Script de Azure PowerShell de ejemplo: conectar una base de datos SQL del tooa de aplicación web"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8f80b940378d020cbcaec2c1bbc28bae1a3ef35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="506d4-103">Conectarse a una base de datos SQL del tooa de aplicación web</span><span class="sxs-lookup"><span data-stu-id="506d4-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="506d4-104">En este escenario, aprenderá cómo toocreate una base de datos de SQL Azure y un Azure aplicación web.</span><span class="sxs-lookup"><span data-stu-id="506d4-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="506d4-105">A continuación, vinculará Hola SQL base de datos toohello web app con la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="506d4-105">Then you will link hello SQL database toohello web app using app settings.</span></span>

<span data-ttu-id="506d4-106">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="506d4-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="506d4-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="506d4-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app tooa SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="506d4-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="506d4-108">Clean up deployment</span></span> 

<span data-ttu-id="506d4-109">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="506d4-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="506d4-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="506d4-110">Script explanation</span></span>

<span data-ttu-id="506d4-111">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="506d4-111">This script uses hello following commands.</span></span> <span data-ttu-id="506d4-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="506d4-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="506d4-113">Comando</span><span class="sxs-lookup"><span data-stu-id="506d4-113">Command</span></span> | <span data-ttu-id="506d4-114">Notas</span><span class="sxs-lookup"><span data-stu-id="506d4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="506d4-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="506d4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="506d4-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="506d4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="506d4-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="506d4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="506d4-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="506d4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="506d4-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="506d4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="506d4-120">Crea una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="506d4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="506d4-121">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="506d4-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="506d4-122">Crea un servidor de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="506d4-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="506d4-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="506d4-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="506d4-124">Crea una regla de firewall para un servidor SQL Database.</span><span class="sxs-lookup"><span data-stu-id="506d4-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="506d4-125">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="506d4-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="506d4-126">Crea una base de datos o una base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="506d4-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="506d4-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="506d4-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="506d4-128">Modifica la configuración de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="506d4-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="506d4-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="506d4-129">Next steps</span></span>

<span data-ttu-id="506d4-130">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="506d4-130">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="506d4-131">Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="506d4-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
