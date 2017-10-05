---
title: "Ejemplo de script de la CLI de Azure: supervisión de una aplicación web con registros de servidor web | Microsoft Docs"
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
ms.openlocfilehash: df4ca5b1270ada849e231ad9608a5b1d2edda8be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="35042-103">Supervisión de una aplicación web con registros de servidor web</span><span class="sxs-lookup"><span data-stu-id="35042-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="35042-104">En este escenario, creará un grupo de recursos, un plan de App Service y una aplicación web, además de configurar la aplicación web para habilitar los registros del servidor web.</span><span class="sxs-lookup"><span data-stu-id="35042-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="35042-105">A continuación, descargará los archivos de registro para revisarlos.</span><span class="sxs-lookup"><span data-stu-id="35042-105">You will then download the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="35042-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="35042-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="35042-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="35042-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="35042-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="35042-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="35042-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="35042-109">Sample script</span></span>

<span data-ttu-id="35042-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Registros de Monitor")]</span><span class="sxs-lookup"><span data-stu-id="35042-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="35042-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="35042-111">Script explanation</span></span>

<span data-ttu-id="35042-112">Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="35042-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="35042-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="35042-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="35042-114">Comando</span><span class="sxs-lookup"><span data-stu-id="35042-114">Command</span></span> | <span data-ttu-id="35042-115">Notas</span><span class="sxs-lookup"><span data-stu-id="35042-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="35042-116">az group create</span><span class="sxs-lookup"><span data-stu-id="35042-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="35042-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="35042-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="35042-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="35042-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="35042-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="35042-119">Creates an App Service plan.</span></span> <span data-ttu-id="35042-120">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="35042-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="35042-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="35042-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="35042-122">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="35042-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="35042-123">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="35042-123">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="35042-124">Configura los registros que conservará una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="35042-124">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="35042-125">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="35042-125">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="35042-126">Descarga los registros de una aplicación web de Azure en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="35042-126">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="35042-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35042-127">Next steps</span></span>

<span data-ttu-id="35042-128">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="35042-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="35042-129">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="35042-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
