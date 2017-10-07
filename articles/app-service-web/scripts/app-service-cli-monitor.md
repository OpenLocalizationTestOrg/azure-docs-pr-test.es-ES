---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure supervisar una aplicación web con registros de servidor web | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: supervisión de una aplicación web con registros de servidor web"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="c9e82-103">Supervisión de una aplicación web con registros de servidor web</span><span class="sxs-lookup"><span data-stu-id="c9e82-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="c9e82-104">En este escenario creará un grupo de recursos, el plan de servicio de aplicaciones, la aplicación web y configurar registros de servidor web de hello web app tooenable.</span><span class="sxs-lookup"><span data-stu-id="c9e82-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="c9e82-105">A continuación, se descargarán los archivos de registro de hello para su revisión.</span><span class="sxs-lookup"><span data-stu-id="c9e82-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c9e82-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c9e82-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c9e82-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9e82-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c9e82-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c9e82-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c9e82-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c9e82-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c9e82-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="c9e82-110">Script explanation</span></span>

<span data-ttu-id="c9e82-111">Este script utiliza Hola siguientes comandos toocreate un grupo de recursos, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="c9e82-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="c9e82-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="c9e82-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c9e82-113">Comando</span><span class="sxs-lookup"><span data-stu-id="c9e82-113">Command</span></span> | <span data-ttu-id="c9e82-114">Notas</span><span class="sxs-lookup"><span data-stu-id="c9e82-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9e82-115">az group create</span><span class="sxs-lookup"><span data-stu-id="c9e82-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c9e82-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="c9e82-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9e82-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c9e82-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c9e82-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="c9e82-118">Creates an App Service plan.</span></span> <span data-ttu-id="c9e82-119">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e82-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="c9e82-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c9e82-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c9e82-121">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e82-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c9e82-122">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="c9e82-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="c9e82-123">Configura los registros que conservará una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e82-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="c9e82-124">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="c9e82-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="c9e82-125">Hola de descargas de los registros del programa Hola a un equipo local de la tooyour de aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e82-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9e82-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9e82-126">Next steps</span></span>

<span data-ttu-id="c9e82-127">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9e82-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c9e82-128">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c9e82-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
