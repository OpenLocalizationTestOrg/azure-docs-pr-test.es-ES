---
title: "Aplicación Web en Linux con CLI de Azure 2.0 aaaManage | Documentos de Microsoft"
description: "Administre Aplicación web en Linux mediante la CLI de Azure."
keywords: azure app service, web app, cli, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="b6a1a-104">Administración de Aplicación web en Linux mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b6a1a-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="b6a1a-105">Mediante comandos de hello en este artículo son capaz de toocreate y administrar una aplicación Web en Linux con CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="b6a1a-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="b6a1a-106">Puede comenzar a usar la nueva versión de hello de hello CLI de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="b6a1a-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="b6a1a-107">[Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en su equipo.</span><span class="sxs-lookup"><span data-stu-id="b6a1a-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="b6a1a-108">Uso de [Azure Cloud Shell (versión preliminar)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="b6a1a-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="b6a1a-109">Creación de un plan de App Service de Linux</span><span class="sxs-lookup"><span data-stu-id="b6a1a-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="b6a1a-110">toocreate un Plan de servicio de aplicaciones de Linux, puede usar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b6a1a-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="b6a1a-111">Creación de una aplicación web del contenedor de Docker personalizada</span><span class="sxs-lookup"><span data-stu-id="b6a1a-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="b6a1a-112">toocreate una aplicación web y configurarlo toorun contenedor Docker personalizado, puede usar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b6a1a-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="b6a1a-113">Activar el registro de contenedor de Docker de Hola</span><span class="sxs-lookup"><span data-stu-id="b6a1a-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="b6a1a-114">tooactivate Hola registro de contenedor de Docker, puede utilizar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b6a1a-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="b6a1a-115">Contenedor Docker cambio Hola personalizadas para una aplicación Web existente en Linux App</span><span class="sxs-lookup"><span data-stu-id="b6a1a-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="b6a1a-116">toochange una aplicación creada anteriormente, de hello actual Docker imagen tooa nueva imagen, puede usar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b6a1a-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="b6a1a-117">Uso de imágenes de Docker de un Registro privado</span><span class="sxs-lookup"><span data-stu-id="b6a1a-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="b6a1a-118">Puede configurar imágenes de toouse su aplicación desde un registro privada.</span><span class="sxs-lookup"><span data-stu-id="b6a1a-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="b6a1a-119">Necesitará tooprovide Hola url para el registro, el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="b6a1a-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="b6a1a-120">Esto puede lograrse mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b6a1a-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="b6a1a-121">Habilitación de implementaciones continuas para imágenes de Docker personalizadas</span><span class="sxs-lookup"><span data-stu-id="b6a1a-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="b6a1a-122">Con el siguiente comando de Hola puede habilitar la funcionalidad del CD de Hola y obtener la dirección url del webhook Hola.</span><span class="sxs-lookup"><span data-stu-id="b6a1a-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="b6a1a-123">Esta dirección url puede ser usado tooconfigure se DockerHub o del registro de contenedor de Azure repositorios.</span><span class="sxs-lookup"><span data-stu-id="b6a1a-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="b6a1a-124">Creación de una aplicación web en Linux mediante uno de nuestros marcos en tiempo de ejecución integrados</span><span class="sxs-lookup"><span data-stu-id="b6a1a-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="b6a1a-125">toocreate una aplicación PHP 5.6 en App Linux que, se puede usar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6a1a-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="b6a1a-126">Cambio de la versión de .NET Framework por una aplicación web en Linux existente</span><span class="sxs-lookup"><span data-stu-id="b6a1a-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="b6a1a-127">toochange una aplicación creada anteriormente, de hello actual framework versión tooNode.js 6.11, puede usar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b6a1a-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="b6a1a-128">Configuración de implementaciones Git para su aplicación web</span><span class="sxs-lookup"><span data-stu-id="b6a1a-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="b6a1a-129">tooset una de las implementaciones de Git para la aplicación, puede usar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b6a1a-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="b6a1a-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6a1a-130">Next steps</span></span>
* [<span data-ttu-id="b6a1a-131">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="b6a1a-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="b6a1a-132">Instalación de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b6a1a-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="b6a1a-133">Azure Cloud Shell (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="b6a1a-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="b6a1a-134">Configuración de entornos de ensayo en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b6a1a-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="b6a1a-135">Implementación continua con Azure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="b6a1a-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
