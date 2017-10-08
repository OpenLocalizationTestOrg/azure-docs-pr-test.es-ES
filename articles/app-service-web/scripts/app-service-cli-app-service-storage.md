---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure conectarse a una cuenta de almacenamiento de tooa de aplicación web | Documentos de Microsoft"
description: "Script de CLI de Azure de ejemplo: conectar una cuenta de almacenamiento de tooa de aplicación web"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: affee2d39ef3f98c6043010850e08b67fb9ce54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="67771-103">Conectarse a una cuenta de almacenamiento de tooa de aplicación web</span><span class="sxs-lookup"><span data-stu-id="67771-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="67771-104">En este escenario, aprenderá cómo toocreate una cuenta de almacenamiento de Azure y un Azure aplicación web.</span><span class="sxs-lookup"><span data-stu-id="67771-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="67771-105">A continuación, vinculará Hola almacenamiento cuenta toohello web app con la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="67771-105">Then you will link hello storage account toohello web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="67771-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="67771-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="67771-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="67771-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="67771-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="67771-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="67771-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="67771-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="67771-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="67771-110">Script explanation</span></span>

<span data-ttu-id="67771-111">Este script utiliza Hola después comandos toocreate un grupo de recursos, aplicación web, cuenta de almacenamiento y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="67771-111">This script uses hello following commands toocreate a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="67771-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="67771-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="67771-113">Comando</span><span class="sxs-lookup"><span data-stu-id="67771-113">Command</span></span> | <span data-ttu-id="67771-114">Notas</span><span class="sxs-lookup"><span data-stu-id="67771-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="67771-115">az group create</span><span class="sxs-lookup"><span data-stu-id="67771-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="67771-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="67771-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="67771-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="67771-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="67771-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="67771-118">Creates an App Service plan.</span></span> <span data-ttu-id="67771-119">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="67771-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="67771-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="67771-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="67771-121">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="67771-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="67771-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="67771-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="67771-123">Crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="67771-123">Creates a storage account.</span></span> <span data-ttu-id="67771-124">Esto es donde se almacenan los activos de hello estáticos.</span><span class="sxs-lookup"><span data-stu-id="67771-124">This is where hello static assets will be stored.</span></span> |
| [<span data-ttu-id="67771-125">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="67771-125">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="67771-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="67771-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="67771-127">Crea o actualiza una configuración de aplicación para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="67771-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="67771-128">La configuración de la aplicación se expone como variables de entorno para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="67771-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="67771-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67771-129">Next steps</span></span>

<span data-ttu-id="67771-130">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="67771-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="67771-131">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="67771-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
