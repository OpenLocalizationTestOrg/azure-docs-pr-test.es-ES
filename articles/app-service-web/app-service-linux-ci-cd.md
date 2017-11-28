---
title: "Implementación de aplicación Web de Azure en Linux aaaContinuous | Documentos de Microsoft"
description: "¿Cómo toosetup la implementación continua en la aplicación Web de Azure en Linux."
keywords: azure app service, linux, oss, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="d5e83-104">Implementación continua con Aplicación web de Azure en Linux</span><span class="sxs-lookup"><span data-stu-id="d5e83-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="d5e83-105">En este tutorial, configurará una implementación continua para una imagen de contenedor personalizada desde los repositorios administrados de [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) o [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="d5e83-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="d5e83-106">Paso 1: tooAzure de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="d5e83-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="d5e83-107">Inicie sesión en toohello portal de Azure en http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="d5e83-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="d5e83-108">Paso 2: Habilitación de la característica de implementación continua del contenedor</span><span class="sxs-lookup"><span data-stu-id="d5e83-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="d5e83-109">Puede habilitar la característica de implementación continua de hello mediante [CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) y ejecutando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="d5e83-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="d5e83-110">Hola  **[portal de Azure](https://portal.azure.com/)**, haga clic en hello **servicio de aplicaciones** opción izquierda Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="d5e83-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="d5e83-111">Haga clic en el nombre de saludo de la aplicación que desee tooconfigure Docker Hub una implementación continua para.</span><span class="sxs-lookup"><span data-stu-id="d5e83-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="d5e83-112">Hola **configuración de la aplicación**, agregar una aplicación llamada `DOCKER_ENABLE_CI` con el valor de hello `true`.</span><span class="sxs-lookup"><span data-stu-id="d5e83-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![insert image of app setting](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="d5e83-114">Paso 3: Preparación de la dirección URL de webhook</span><span class="sxs-lookup"><span data-stu-id="d5e83-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="d5e83-115">Puede obtener utilizando de hello URL del Webhook [CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) y ejecutando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="d5e83-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="d5e83-116">Para hello URL del Webhook, necesita hello toohave después de punto de conexión: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="d5e83-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="d5e83-117">Puede obtener la `publishingusername` y `publishingpwd` mediante la descarga de aplicación web de hello publicar perfil mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5e83-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![insert image of adding webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="d5e83-119">Paso 4: Incorporación de webhook</span><span class="sxs-lookup"><span data-stu-id="d5e83-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="d5e83-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d5e83-120">Azure Container Registry</span></span>

<span data-ttu-id="d5e83-121">En la hoja del portal de registro, haga clic en **Webhooks** y cree un nuevo webhook haciendo clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d5e83-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="d5e83-122">Hola **crear webhook** hoja, asigne un nombre a su webhook.</span><span class="sxs-lookup"><span data-stu-id="d5e83-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="d5e83-123">Para hello Webhook URI, necesita tooprovide Hola URL obtenido de **paso 3**</span><span class="sxs-lookup"><span data-stu-id="d5e83-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="d5e83-124">Asegúrese de que define el ámbito de hello como Hola repositorio que contiene la imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="d5e83-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![insertar imagen de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="d5e83-126">Cuando se actualiza la imagen de hello, aplicación web de hello se actualizan automáticamente con la nueva imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5e83-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="d5e83-127">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="d5e83-127">Docker Hub</span></span>

<span data-ttu-id="d5e83-128">En la página de Docker Hub, haga clic en **Webhooks** y, luego, en **CREAR NUEVO WEBHOOK**.</span><span class="sxs-lookup"><span data-stu-id="d5e83-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![insert image of adding webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="d5e83-130">Para la dirección URL del Webhook hello, necesita tooprovide Hola URL obtenido de **paso 3**</span><span class="sxs-lookup"><span data-stu-id="d5e83-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![insert image of adding webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="d5e83-132">Cuando se actualiza la imagen de hello, aplicación web de hello se actualizan automáticamente con la nueva imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5e83-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5e83-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5e83-133">Next steps</span></span>
* [<span data-ttu-id="d5e83-134">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="d5e83-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="d5e83-135">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d5e83-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="d5e83-136">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="d5e83-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="d5e83-137">Uso de .NET Core en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="d5e83-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="d5e83-138">Uso de Ruby en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="d5e83-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="d5e83-139">Cómo la imagen toouse una Docker personalizada para la aplicación Web de Azure en Linux</span><span class="sxs-lookup"><span data-stu-id="d5e83-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="d5e83-140">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d5e83-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="d5e83-141">Administración de Aplicación web en Linux mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d5e83-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



