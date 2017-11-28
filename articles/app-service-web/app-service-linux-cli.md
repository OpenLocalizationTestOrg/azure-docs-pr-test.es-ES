---
title: "Administración de Aplicación web en Linux mediante la CLI de Azure 2.0 | Microsoft Docs"
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
ms.openlocfilehash: 04aceecf0cb4cad5c838b7254bf7079a36bbd0d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="e903c-104">Administración de Aplicación web en Linux mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e903c-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="e903c-105">Con los comandos de este artículo, podrá crear y administrar Aplicación web en Linux mediante la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="e903c-105">Using the commands in this article you are able to create and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="e903c-106">Puede empezar a usar la nueva versión de la CLI de dos formas:</span><span class="sxs-lookup"><span data-stu-id="e903c-106">You can start using the new version of the CLI in two ways:</span></span>

* <span data-ttu-id="e903c-107">[Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en su equipo.</span><span class="sxs-lookup"><span data-stu-id="e903c-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="e903c-108">Uso de [Azure Cloud Shell (versión preliminar)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="e903c-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="e903c-109">Creación de un plan de App Service de Linux</span><span class="sxs-lookup"><span data-stu-id="e903c-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="e903c-110">Para crear un plan de App Service de Linux, puede usar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e903c-110">To create a Linux App Service Plan, you can use the following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="e903c-111">Creación de una aplicación web del contenedor de Docker personalizada</span><span class="sxs-lookup"><span data-stu-id="e903c-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="e903c-112">Para crear una aplicación web y configurarla para ejecutar un contenedor de Docker personalizado, puede usar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e903c-112">To create a web app and configuring it to run a custom Docker container, you can use the following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-the-docker-container-logging"></a><span data-ttu-id="e903c-113">Activación del registro del contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="e903c-113">Activate the Docker container logging</span></span>

<span data-ttu-id="e903c-114">Para activar el registro del contenedor de Docker, puede usar el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e903c-114">To activate the Docker container logging, you can use the following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="e903c-115">Cambio del contenedor de Docker personalizado por una aplicación web en Linux existente</span><span class="sxs-lookup"><span data-stu-id="e903c-115">Change the custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="e903c-116">Para cambiar una aplicación creada anteriormente, de la imagen de Docker actual a una nueva imagen, puede usar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e903c-116">To change a previously created app, from the current Docker image to a new image, you can use the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="e903c-117">Uso de imágenes de Docker de un Registro privado</span><span class="sxs-lookup"><span data-stu-id="e903c-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="e903c-118">Puede configurar la aplicación para usar imágenes de un Registro privado.</span><span class="sxs-lookup"><span data-stu-id="e903c-118">You can configure your app to use images from a private registry.</span></span> <span data-ttu-id="e903c-119">Debe proporcionar la dirección URL de su Registro, nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="e903c-119">You need to provide the url for your registry, user name, and password.</span></span> <span data-ttu-id="e903c-120">Esto se puede lograr con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e903c-120">This can be achieved using the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="e903c-121">Habilitación de implementaciones continuas para imágenes de Docker personalizadas</span><span class="sxs-lookup"><span data-stu-id="e903c-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="e903c-122">Con el siguiente comando puede habilitar la funcionalidad de CD y obtener la dirección URL de webhook.</span><span class="sxs-lookup"><span data-stu-id="e903c-122">With the following command you can enable the CD functionality, and get the webhook url.</span></span> <span data-ttu-id="e903c-123">Esta dirección URL se puede usar para configurar su repositorio de Azure Container Registry o DockerHub.</span><span class="sxs-lookup"><span data-stu-id="e903c-123">This url can be used to configure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="e903c-124">Creación de una aplicación web en Linux mediante uno de nuestros marcos en tiempo de ejecución integrados</span><span class="sxs-lookup"><span data-stu-id="e903c-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="e903c-125">Para crear una aplicación web de PHP 5.6 en Linux, puede usar el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="e903c-125">To create a PHP 5.6 Web App on Linux App that, you can use the following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="e903c-126">Cambio de la versión de .NET Framework por una aplicación web en Linux existente</span><span class="sxs-lookup"><span data-stu-id="e903c-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="e903c-127">Para cambiar una aplicación creada anteriormente, de la versión de .NET Framework actual a Node.js 6.11, puede usar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e903c-127">To change a previously created app, from the current framework version to Node.js 6.11, you can use the following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="e903c-128">Configuración de implementaciones Git para su aplicación web</span><span class="sxs-lookup"><span data-stu-id="e903c-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="e903c-129">Para configurar implementaciones Git para su aplicación, puede usar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e903c-129">To set up Git deployments for your app, you can use the following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="e903c-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e903c-130">Next steps</span></span>
* [<span data-ttu-id="e903c-131">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="e903c-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="e903c-132">Instalación de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e903c-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="e903c-133">Azure Cloud Shell (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="e903c-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="e903c-134">Configuración de entornos de ensayo en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e903c-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="e903c-135">Implementación continua con Azure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="e903c-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
