---
title: "Administración de clústeres de Azure Swarm con la API de Docker | Microsoft Docs"
description: "Implementación de contenedores en un clúster de Docker Swarm en Azure Container Service"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 6ca2d2e49c4b7f5eb0580e7091b09209f8b73a7c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="69574-104">Administración de contenedores con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="69574-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="69574-105">Docker Swarm proporciona un entorno para implementar cargas de trabajo en contenedores a través de un conjunto agrupado de hosts de Docker.</span><span class="sxs-lookup"><span data-stu-id="69574-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="69574-106">Docker Swarm usa la API nativa de Docker.</span><span class="sxs-lookup"><span data-stu-id="69574-106">Docker Swarm uses the native Docker API.</span></span> <span data-ttu-id="69574-107">El flujo de trabajo para administrar contenedores en un Docker Swarm es casi idéntico al que sería en un host de un solo contenedor.</span><span class="sxs-lookup"><span data-stu-id="69574-107">The workflow for managing containers on a Docker Swarm is almost identical to what it would be on a single container host.</span></span> <span data-ttu-id="69574-108">Este documento proporciona ejemplos sencillos de la implementación de cargas de trabajo en contenedores en una instancia de Azure Container Service (servicio Contenedor de Azure) de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="69574-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="69574-109">Para obtener documentación más detallada sobre Docker Swarm, consulte [Docker Swarm en Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="69574-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="69574-110">Requisitos previos para los ejercicios de este documento:</span><span class="sxs-lookup"><span data-stu-id="69574-110">Prerequisites to the exercises in this document:</span></span>

[<span data-ttu-id="69574-111">Crear un clúster de Swarm en Azure Container Service (servicio Contenedor de Azure)</span><span class="sxs-lookup"><span data-stu-id="69574-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="69574-112">Conectar con el clúster de Swarm en Azure Container Service (servicio Contenedor de Azure)</span><span class="sxs-lookup"><span data-stu-id="69574-112">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="69574-113">Implementación de un contenedor nuevo</span><span class="sxs-lookup"><span data-stu-id="69574-113">Deploy a new container</span></span>
<span data-ttu-id="69574-114">Para crear un nuevo contenedor en Docker Swarm, use el comando `docker run` (asegúrese de que ha abierto un túnel SSH para los patrones de acuerdo con los requisitos previos anteriores).</span><span class="sxs-lookup"><span data-stu-id="69574-114">To create a new container in the Docker Swarm, use the `docker run` command (ensuring that you have opened an SSH tunnel to the masters as per the prerequisites above).</span></span> <span data-ttu-id="69574-115">Este ejemplo crea un contenedor a partir de la imagen `yeasy/simple-web` :</span><span class="sxs-lookup"><span data-stu-id="69574-115">This example creates a container from the `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="69574-116">Una vez creado el contenedor, utilice `docker ps` para devolver información acerca del mismo.</span><span class="sxs-lookup"><span data-stu-id="69574-116">After the container has been created, use `docker ps` to return information about the container.</span></span> <span data-ttu-id="69574-117">Observe que aparece el agente de Swarm que hospeda el contenedor:</span><span class="sxs-lookup"><span data-stu-id="69574-117">Notice here that the Swarm agent that is hosting the container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="69574-118">Ahora puede acceder a la aplicación que se ejecuta en este contenedor a través del nombre DNS público del equilibrador de carga del agente de Swarm.</span><span class="sxs-lookup"><span data-stu-id="69574-118">You can now access the application that is running in this container through the public DNS name of the Swarm agent load balancer.</span></span> <span data-ttu-id="69574-119">Puede encontrar esta información en el Portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="69574-119">You can find this information in the Azure portal:</span></span>  

![Resultados de la visita real](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="69574-121">De forma predeterminada, el equilibrador de carga tiene los puertos 80, 443 y 8080 abiertos.</span><span class="sxs-lookup"><span data-stu-id="69574-121">By default the Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="69574-122">Si va a conectar en otro puerto debe abrirlo en Azure Load Balancer para el grupo de agentes.</span><span class="sxs-lookup"><span data-stu-id="69574-122">If you want to connect on another port you will need to open that port on the Azure Load Balancer for the Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="69574-123">Implementación de varios contenedores</span><span class="sxs-lookup"><span data-stu-id="69574-123">Deploy multiple containers</span></span>
<span data-ttu-id="69574-124">Cuando se inician varios contenedores, al ejecutar varias veces "docker run", se puede usar el comando `docker ps` para ver en qué host se ejecutan los contenedores.</span><span class="sxs-lookup"><span data-stu-id="69574-124">As multiple containers are started, by executing 'docker run' multiple times, you can use the `docker ps` command to see which hosts the containers are running on.</span></span> <span data-ttu-id="69574-125">En el siguiente ejemplo, tres contenedores se propagan uniformemente por los tres agentes de Swarm:</span><span class="sxs-lookup"><span data-stu-id="69574-125">In the example below, three containers are spread evenly across the three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="69574-126">Implementación de contenedores mediante Docker Compose</span><span class="sxs-lookup"><span data-stu-id="69574-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="69574-127">Puede usar Docker Compose para automatizar la implementación y configuración de varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="69574-127">You can use Docker Compose to automate the deployment and configuration of multiple containers.</span></span> <span data-ttu-id="69574-128">Para ello, asegúrese de que se ha creado un túnel Secure Shell (SSH) y se ha establecido la variable DOCKER_HOST (consulte los requisitos previos anteriores).</span><span class="sxs-lookup"><span data-stu-id="69574-128">To do so, ensure that a Secure Shell (SSH) tunnel has been created and that the DOCKER_HOST variable has been set (see the pre-requisites above).</span></span>

<span data-ttu-id="69574-129">Cree un archivo docker-compose.yml en el sistema local.</span><span class="sxs-lookup"><span data-stu-id="69574-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="69574-130">Para ello, use este [ejemplo](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="69574-130">To do this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="69574-131">Ejecute `docker-compose up -d` para iniciar las implementaciones de contenedores:</span><span class="sxs-lookup"><span data-stu-id="69574-131">Run `docker-compose up -d` to start the container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="69574-132">Por último, se devolverá la lista de contenedores en ejecución.</span><span class="sxs-lookup"><span data-stu-id="69574-132">Finally, the list of running containers will be returned.</span></span> <span data-ttu-id="69574-133">Esta lista refleja los contenedores que se implementaron mediante Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="69574-133">This list reflects the containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="69574-134">Naturalmente, puede usar `docker-compose ps` para examinar solo los contenedores definidos en su archivo `compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="69574-134">Naturally, you can use `docker-compose ps` to examine only the containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69574-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69574-135">Next steps</span></span>
[<span data-ttu-id="69574-136">Más información acerca de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="69574-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

