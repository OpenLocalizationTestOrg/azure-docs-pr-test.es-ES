---
title: "tutorial de instancias de contenedor - aaaAzure Prepare su aplicación | Documentos de Azure"
description: "Preparar una aplicación para la implementación tooAzure instancias de contenedor"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="6e571-103">Crear contenedor de implementación tooAzure instancias de contenedor</span><span class="sxs-lookup"><span data-stu-id="6e571-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="6e571-104">Azure Container Instances permite la implementación de contenedores de Docker en la infraestructura de Azure sin necesidad de aprovisionar ninguna máquina virtual o adoptar algún servicio de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="6e571-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="6e571-105">En este tutorial, compilará una aplicación web simple en Node.js y la empaquetará en un contenedor que se pueden ejecutar mediante Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="6e571-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="6e571-106">Se tratarán los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="6e571-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e571-107">La clonación de origen de la aplicación desde GitHub</span><span class="sxs-lookup"><span data-stu-id="6e571-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="6e571-108">La creación de imágenes de contenedor desde el origen de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6e571-108">Creating container images from application source</span></span>
> * <span data-ttu-id="6e571-109">Pruebe imágenes de hello en un entorno local de Docker</span><span class="sxs-lookup"><span data-stu-id="6e571-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="6e571-110">En los tutoriales posteriores, se cargue su tooan de imagen del registro de contenedor de Azure y, a continuación, implementarlos tooAzure instancias de contenedor.</span><span class="sxs-lookup"><span data-stu-id="6e571-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6e571-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="6e571-111">Before you begin</span></span>

<span data-ttu-id="6e571-112">En este tutorial se supone que el usuario tiene un conocimiento básico de los principales conceptos de Docker, como los contenedores, las imágenes de contenedor y los comandos básicos de Docker.</span><span class="sxs-lookup"><span data-stu-id="6e571-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="6e571-113">Si es necesario, consulte la [introducción a Docker]( https://docs.docker.com/get-started/), donde encontrará datos básicos acerca de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="6e571-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="6e571-114">toocomplete este tutorial, necesitará un entorno de desarrollo de Docker.</span><span class="sxs-lookup"><span data-stu-id="6e571-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="6e571-115">Docker proporciona paquetes que permiten configurar Docker fácilmente en cualquier sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) o [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="6e571-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="6e571-116">Obtención del código de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6e571-116">Get application code</span></span>

<span data-ttu-id="6e571-117">ejemplo de Hola en este tutorial incluye una aplicación web simple generada [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="6e571-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="6e571-118">aplicación Hello sirve una página HTML estática y el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="6e571-118">hello app serves a static HTML page and looks like this:</span></span>

![Aplicación del tutorial tal como se muestra en un explorador][aci-tutorial-app]

<span data-ttu-id="6e571-120">Ejemplo de Hola a Use git toodownload:</span><span class="sxs-lookup"><span data-stu-id="6e571-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="6e571-121">Crear imagen de contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="6e571-121">Build hello container image</span></span>

<span data-ttu-id="6e571-122">Hola Dockerfile proporcionado en el repositorio de ejemplo de Hola muestra cómo se crea el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e571-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="6e571-123">Se inicia desde un [imagen oficial de Node.js] [ dockerhub-nodeimage] basado en [Linux Alpine](https://alpinelinux.org/), una distribución pequeña que es idóneo toouse con contenedores.</span><span class="sxs-lookup"><span data-stu-id="6e571-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="6e571-124">A continuación, copia los archivos de la aplicación hello en el contenedor de hello, instala las dependencias mediante Administrador de paquetes de nodo de Hola y finalmente inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6e571-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="6e571-125">Hola de uso `docker build` comando toocreate Hola imagen del contenedor, etiquetado como *aplicación de tutorial de aci*:</span><span class="sxs-lookup"><span data-stu-id="6e571-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="6e571-126">Hola de uso `docker images` toosee imagen de hello integrada:</span><span class="sxs-lookup"><span data-stu-id="6e571-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="6e571-127">Salida:</span><span class="sxs-lookup"><span data-stu-id="6e571-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="6e571-128">Ejecutar el contenedor de hello localmente</span><span class="sxs-lookup"><span data-stu-id="6e571-128">Run hello container locally</span></span>

<span data-ttu-id="6e571-129">Antes de intentar implementar Hola contenedor tooAzure instancias de contenedor, ejecutarla localmente tooconfirm que funciona.</span><span class="sxs-lookup"><span data-stu-id="6e571-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="6e571-130">Hola `-d` conmutador permite la ejecución en segundo plano de hello, de contenedor de hello mientras `-p` permite toomap un puerto arbitrario en su tooport cálculo 80 en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e571-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="6e571-131">Hola abra Explorador toohttp://localhost:8080 tooconfirm que Hola contenedor se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="6e571-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Aplicación en ejecución Hola localmente en el Explorador de Hola][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="6e571-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e571-133">Next steps</span></span>

<span data-ttu-id="6e571-134">En este tutorial, ha creado una imagen de contenedor que puede ser implementado tooAzure instancias de contenedor.</span><span class="sxs-lookup"><span data-stu-id="6e571-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="6e571-135">se completaron Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6e571-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e571-136">Origen de clonación de aplicación Hola desde GitHub</span><span class="sxs-lookup"><span data-stu-id="6e571-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="6e571-137">La creación de imágenes de contenedor desde el origen de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6e571-137">Creating container images from application source</span></span>
> * <span data-ttu-id="6e571-138">Contenedor de hello pruebas localmente</span><span class="sxs-lookup"><span data-stu-id="6e571-138">Testing hello container locally</span></span>

<span data-ttu-id="6e571-139">Avanzar toohello toolearn de tutorial siguiente sobre el almacenamiento de imágenes del contenedor en un registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e571-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e571-140">Insertar imágenes tooAzure del registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="6e571-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png