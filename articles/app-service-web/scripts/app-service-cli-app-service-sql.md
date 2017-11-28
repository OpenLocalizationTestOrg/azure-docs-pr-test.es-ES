---
title: "Ejemplo de script de la CLI de Azure: conexión de una aplicación web a una base de datos SQL | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: conexión de una aplicación web a una base de datos SQL"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ec5e22bfacc12a89f1fb5882487df4829369777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="bb53d-103">Conexión de una aplicación web a una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="bb53d-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="bb53d-104">En este escenario aprenderá a crear una instancia de Azure SQL Database y una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb53d-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="bb53d-105">Y, después, vinculará la base de datos SQL a la aplicación web mediante la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb53d-105">Then you will link the SQL database to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bb53d-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="bb53d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bb53d-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="bb53d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="bb53d-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb53d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bb53d-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb53d-109">Sample script</span></span>

<span data-ttu-id="bb53d-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="bb53d-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bb53d-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="bb53d-111">Script explanation</span></span>

<span data-ttu-id="bb53d-112">Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web, una base de datos SQL y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="bb53d-112">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="bb53d-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="bb53d-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bb53d-114">Comando</span><span class="sxs-lookup"><span data-stu-id="bb53d-114">Command</span></span> | <span data-ttu-id="bb53d-115">Notas</span><span class="sxs-lookup"><span data-stu-id="bb53d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bb53d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="bb53d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bb53d-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="bb53d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bb53d-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="bb53d-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bb53d-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="bb53d-119">Creates an App Service plan.</span></span> <span data-ttu-id="bb53d-120">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb53d-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="bb53d-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="bb53d-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="bb53d-122">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb53d-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="bb53d-123">az sql server create</span><span class="sxs-lookup"><span data-stu-id="bb53d-123">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="bb53d-124">Crea un servidor de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bb53d-124">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="bb53d-125">az sql db create</span><span class="sxs-lookup"><span data-stu-id="bb53d-125">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="bb53d-126">Crea una nueva base de datos con el servidor de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bb53d-126">Creates a new database with the SQL Database Server.</span></span> |
| [<span data-ttu-id="bb53d-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="bb53d-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="bb53d-128">Crea o actualiza una configuración de aplicación para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb53d-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="bb53d-129">La configuración de la aplicación se expone como variables de entorno para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb53d-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bb53d-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb53d-130">Next steps</span></span>

<span data-ttu-id="bb53d-131">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bb53d-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bb53d-132">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bb53d-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
