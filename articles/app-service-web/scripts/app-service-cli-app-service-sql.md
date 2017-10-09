---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure conectar una base de datos SQL de web app tooa | Documentos de Microsoft
description: "Script de CLI de Azure de ejemplo: conectar una base de datos SQL del tooa de aplicación web"
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
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="aa5ff-103">Conectarse a una base de datos SQL del tooa de aplicación web</span><span class="sxs-lookup"><span data-stu-id="aa5ff-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="aa5ff-104">En este escenario, aprenderá cómo toocreate una base de datos de SQL Azure y un Azure aplicación web.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="aa5ff-105">A continuación, vinculará Hola SQL base de datos toohello web app con la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aa5ff-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="aa5ff-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="aa5ff-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aa5ff-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="aa5ff-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="aa5ff-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="aa5ff-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="aa5ff-110">Script explanation</span></span>

<span data-ttu-id="aa5ff-111">Este script utiliza Hola después comandos toocreate un grupo de recursos, aplicación web, base de datos SQL y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="aa5ff-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="aa5ff-113">Comando</span><span class="sxs-lookup"><span data-stu-id="aa5ff-113">Command</span></span> | <span data-ttu-id="aa5ff-114">Notas</span><span class="sxs-lookup"><span data-stu-id="aa5ff-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aa5ff-115">az group create</span><span class="sxs-lookup"><span data-stu-id="aa5ff-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="aa5ff-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="aa5ff-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="aa5ff-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="aa5ff-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="aa5ff-118">Creates an App Service plan.</span></span> <span data-ttu-id="aa5ff-119">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="aa5ff-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="aa5ff-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="aa5ff-121">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="aa5ff-122">az sql server create</span><span class="sxs-lookup"><span data-stu-id="aa5ff-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="aa5ff-123">Crea un servidor de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="aa5ff-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="aa5ff-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="aa5ff-125">Crea una nueva base de datos con hello base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="aa5ff-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="aa5ff-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="aa5ff-127">Crea o actualiza una configuración de aplicación para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="aa5ff-128">La configuración de la aplicación se expone como variables de entorno para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa5ff-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aa5ff-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa5ff-129">Next steps</span></span>

<span data-ttu-id="aa5ff-130">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aa5ff-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="aa5ff-131">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="aa5ff-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
