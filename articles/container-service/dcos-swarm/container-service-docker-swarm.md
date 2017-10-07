---
title: "aaaManage Swarm de Azure de clúster con la API de Docker | Documentos de Microsoft"
description: "Implementar contenedores tooa Docker Swarm clúster en el servicio de contenedor de Azure"
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
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="6522c-104">Administración de contenedores con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="6522c-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="6522c-105">Docker Swarm proporciona un entorno para implementar cargas de trabajo en contenedores a través de un conjunto agrupado de hosts de Docker.</span><span class="sxs-lookup"><span data-stu-id="6522c-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="6522c-106">Conjunto de docker utiliza API de Docker nativa de Hola.</span><span class="sxs-lookup"><span data-stu-id="6522c-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="6522c-107">flujo de trabajo de Hello para la administración de contenedores en un Docker Swarm es casi idéntico toowhat sería en un host de contenedor único.</span><span class="sxs-lookup"><span data-stu-id="6522c-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="6522c-108">Este documento proporciona ejemplos sencillos de la implementación de cargas de trabajo en contenedores en una instancia de Azure Container Service (servicio Contenedor de Azure) de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="6522c-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="6522c-109">Para obtener documentación más detallada sobre Docker Swarm, consulte [Docker Swarm en Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="6522c-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="6522c-110">Ejercicios de toohello de requisitos previos en este documento:</span><span class="sxs-lookup"><span data-stu-id="6522c-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="6522c-111">Crear un clúster de Swarm en Azure Container Service (servicio Contenedor de Azure)</span><span class="sxs-lookup"><span data-stu-id="6522c-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="6522c-112">Conectar con el clúster de conjunto de hello en el servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="6522c-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="6522c-113">Implementación de un contenedor nuevo</span><span class="sxs-lookup"><span data-stu-id="6522c-113">Deploy a new container</span></span>
<span data-ttu-id="6522c-114">toocreate un nuevo contenedor de hello Docker Swarm, usar hello `docker run` comando (asegúrese de que ha abierto un maestros de toohello de túnel SSH según los requisitos previos de hello anteriores).</span><span class="sxs-lookup"><span data-stu-id="6522c-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="6522c-115">Este ejemplo crea un contenedor de hello `yeasy/simple-web` imagen:</span><span class="sxs-lookup"><span data-stu-id="6522c-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="6522c-116">Una vez creado el contenedor de hello, use `docker ps` tooreturn información sobre el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="6522c-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="6522c-117">Aquí, tenga en cuenta que el agente Hola conjunto que se hospeda el contenedor de Hola aparece:</span><span class="sxs-lookup"><span data-stu-id="6522c-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="6522c-118">Ahora puede acceder a aplicación Hola que se está ejecutando en este contenedor a través del nombre DNS público de Hola Hola conjunto agente del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="6522c-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="6522c-119">Puede encontrar esta información en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="6522c-119">You can find this information in hello Azure portal:</span></span>  

![Resultados de la visita real](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="6522c-121">De forma predeterminada Hola equilibrador de carga tiene los puertos 80, 443 y 8080 abierto.</span><span class="sxs-lookup"><span data-stu-id="6522c-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="6522c-122">Si desea que tooconnect en otro puerto necesitará tooopen ese puerto en hello equilibrador de carga de Azure para hello grupo de agente.</span><span class="sxs-lookup"><span data-stu-id="6522c-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="6522c-123">Implementación de varios contenedores</span><span class="sxs-lookup"><span data-stu-id="6522c-123">Deploy multiple containers</span></span>
<span data-ttu-id="6522c-124">Cuando se inician varios contenedores, mediante la ejecución de 'run de docker' varias veces, puede usar hello `docker ps` toosee de comando que hospeda contenedores Hola se ejecutan en.</span><span class="sxs-lookup"><span data-stu-id="6522c-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="6522c-125">En el ejemplo de Hola siguiente, tres contenedores están repartidos por igual entre tres agentes de conjunto hello:</span><span class="sxs-lookup"><span data-stu-id="6522c-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="6522c-126">Implementación de contenedores mediante Docker Compose</span><span class="sxs-lookup"><span data-stu-id="6522c-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="6522c-127">Puede usar la implementación de hello tooautomate Docker Compose y la configuración de varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="6522c-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="6522c-128">toodo por lo tanto, asegúrese de que se ha creado un túnel de Shell seguro (SSH) y se ha establecido esa variable DOCKER_HOST Hola (vea Hola cumplen los requisitos previos anteriores).</span><span class="sxs-lookup"><span data-stu-id="6522c-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="6522c-129">Cree un archivo docker-compose.yml en el sistema local.</span><span class="sxs-lookup"><span data-stu-id="6522c-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="6522c-130">toodo, utilícelo [ejemplo](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="6522c-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

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

<span data-ttu-id="6522c-131">Ejecutar `docker-compose up -d` las implementaciones de contenedor de Hola toostart:</span><span class="sxs-lookup"><span data-stu-id="6522c-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

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

<span data-ttu-id="6522c-132">Por último, se devolverá la lista de Hola de contenedores en ejecución.</span><span class="sxs-lookup"><span data-stu-id="6522c-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="6522c-133">Esta lista figuran los contenedores de Hola que se implementaron mediante Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="6522c-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="6522c-134">Naturalmente, puede usar `docker-compose ps` tooexamine sólo Hola contenedores definidos en su `compose.yml` archivo.</span><span class="sxs-lookup"><span data-stu-id="6522c-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6522c-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6522c-135">Next steps</span></span>
[<span data-ttu-id="6522c-136">Más información acerca de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="6522c-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

