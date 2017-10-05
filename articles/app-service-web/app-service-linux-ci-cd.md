---
title: "Implementación continua con Aplicación web de Azure en Linux | Microsoft Docs"
description: "En este artículo se describe cómo configurar una implementación continua en Azure Web App en Linux."
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
ms.openlocfilehash: f8f7d51003f8a55b7f51e8cc2cea838e8e5a6196
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="c8917-104">Implementación continua con Aplicación web de Azure en Linux</span><span class="sxs-lookup"><span data-stu-id="c8917-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="c8917-105">En este tutorial, configurará una implementación continua para una imagen de contenedor personalizada desde los repositorios administrados de [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) o [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="c8917-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="c8917-106">Paso 1: Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="c8917-106">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="c8917-107">Inicie sesión en Azure Portal: http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="c8917-107">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="c8917-108">Paso 2: Habilitación de la característica de implementación continua del contenedor</span><span class="sxs-lookup"><span data-stu-id="c8917-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="c8917-109">Puede habilitar la característica de implementación continua mediante la [CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), así como ejecutando el siguiente comando</span><span class="sxs-lookup"><span data-stu-id="c8917-109">You can enable the continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="c8917-110">En **[Azure Portal](https://portal.azure.com/)**, haga clic en la opción **App Service** del lado izquierdo de la página.</span><span class="sxs-lookup"><span data-stu-id="c8917-110">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="c8917-111">Haga clic en el nombre de la aplicación para la que desea configurar una implementación continua de Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="c8917-111">Click on the name of your app that you want to configure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="c8917-112">En la **configuración de la aplicación**, agregue una aplicación llamada `DOCKER_ENABLE_CI` con el valor `true`.</span><span class="sxs-lookup"><span data-stu-id="c8917-112">In the **App settings**, add an app setting called `DOCKER_ENABLE_CI` with the value `true`.</span></span>

![insert image of app setting](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="c8917-114">Paso 3: Preparación de la dirección URL de webhook</span><span class="sxs-lookup"><span data-stu-id="c8917-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="c8917-115">Puede obtener la dirección URL de webhook mediante la [CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), así como ejecutando el siguiente comando</span><span class="sxs-lookup"><span data-stu-id="c8917-115">You can obtain the Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="c8917-116">Para la URL del Webhook, debe tener el siguiente punto de conexión: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="c8917-116">For the Webhook URL, you need to have the following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="c8917-117">Puede obtener `publishingusername` y `publishingpwd` descargando el perfil de publicación de la aplicación web mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c8917-117">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![insert image of adding webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="c8917-119">Paso 4: Incorporación de webhook</span><span class="sxs-lookup"><span data-stu-id="c8917-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="c8917-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c8917-120">Azure Container Registry</span></span>

<span data-ttu-id="c8917-121">En la hoja del portal de registro, haga clic en **Webhooks** y cree un nuevo webhook haciendo clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c8917-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="c8917-122">En la hoja **Crear webhook**, asigne un nombre a su webhook.</span><span class="sxs-lookup"><span data-stu-id="c8917-122">In the **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="c8917-123">Para el URI de webhook, deberá proporcionar la dirección URL obtenida en el **paso 3**.</span><span class="sxs-lookup"><span data-stu-id="c8917-123">For the Webhook URI, you need to provide the URL obtained from **Step 3**</span></span>

<span data-ttu-id="c8917-124">Asegúrese de que define el ámbito como el repositorio que contiene la imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="c8917-124">Make sure that you define the scope as the repo that contains your container image.</span></span>

![insertar imagen de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="c8917-126">Cuando se actualiza la imagen, la aplicación web se actualizan automáticamente con la nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="c8917-126">When the image gets updated, the web app get updated automatically with the new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="c8917-127">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="c8917-127">Docker Hub</span></span>

<span data-ttu-id="c8917-128">En la página de Docker Hub, haga clic en **Webhooks** y, luego, en **CREAR NUEVO WEBHOOK**.</span><span class="sxs-lookup"><span data-stu-id="c8917-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![insert image of adding webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="c8917-130">Para la dirección URL de webhook, deberá proporcionar la dirección URL que se obtienen de **paso 3**</span><span class="sxs-lookup"><span data-stu-id="c8917-130">For the Webhook URL, you need to provide the URL obtained from **Step 3**</span></span>

![insert image of adding webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="c8917-132">Cuando se actualiza la imagen, la aplicación web se actualizan automáticamente con la nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="c8917-132">When the image gets updated, the web app get updated automatically with the new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8917-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c8917-133">Next steps</span></span>
* [<span data-ttu-id="c8917-134">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="c8917-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="c8917-135">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c8917-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="c8917-136">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="c8917-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="c8917-137">Uso de .NET Core en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="c8917-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="c8917-138">Uso de Ruby en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="c8917-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="c8917-139">Uso de una imagen personalizada de Docker para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="c8917-139">How to use a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="c8917-140">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c8917-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="c8917-141">Administración de Aplicación web en Linux mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c8917-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



