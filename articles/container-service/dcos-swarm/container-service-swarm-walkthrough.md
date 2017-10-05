---
title: "Tutorial de inicio rápido: clúster de Azure Docker Swarm para Linux | Microsoft Docs"
description: "Aprenda rápidamente a crear un clúster de Docker Swarm para contenedores de Linux en Azure Container Service con la CLI de Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 1d10c347795227ed056a95d1bcd4aff82af7b876
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="251d4-103">Implementación del clúster de Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="251d4-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="251d4-104">En este tutorial de inicio rápido, se implementa un clúster de Docker Swarm mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="251d4-104">In this quick start, a Docker Swarm cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="251d4-105">A continuación, se ejecuta e implementa en el clúster una aplicación de varios contenedores que consta de un front-end web y una instancia de Redis.</span><span class="sxs-lookup"><span data-stu-id="251d4-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="251d4-106">Una vez finalizado el proceso, la aplicación es accesible a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="251d4-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="251d4-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="251d4-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="251d4-108">Para realizar este tutorial de inicio rápido, es necesario ejecutar la versión 2.0.4 o superior de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="251d4-108">This quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="251d4-109">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="251d4-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="251d4-110">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="251d4-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="251d4-111">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="251d4-111">Create a resource group</span></span>

<span data-ttu-id="251d4-112">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="251d4-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="251d4-113">Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="251d4-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="251d4-114">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *westus*.</span><span class="sxs-lookup"><span data-stu-id="251d4-114">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="251d4-115">Salida:</span><span class="sxs-lookup"><span data-stu-id="251d4-115">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="251d4-116">Creación de un clúster de Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="251d4-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="251d4-117">Cree un clúster de Docker Swarm en Azure Container Service con el comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="251d4-117">Create a Docker Swarm cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="251d4-118">En el ejemplo siguiente, se crea un clúster denominado *mySwarmCluster* con un nodo maestro de Linux y tres nodos de agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="251d4-118">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="251d4-119">Después de varios minutos, el comando se completa y devuelve información en formato json sobre el clúster.</span><span class="sxs-lookup"><span data-stu-id="251d4-119">After several minutes, the command completes and returns json formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="251d4-120">Conexión al clúster</span><span class="sxs-lookup"><span data-stu-id="251d4-120">Connect to the cluster</span></span>

<span data-ttu-id="251d4-121">A lo largo de este tutorial de inicio rápido, necesitará la dirección IP del maestro de Docker Swarm y del grupo de agentes de Docker.</span><span class="sxs-lookup"><span data-stu-id="251d4-121">Throughout this quick start, you need the IP address of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="251d4-122">Ejecute el comando siguiente para ejecutar ambas direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="251d4-122">Run the following command to return both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="251d4-123">Salida:</span><span class="sxs-lookup"><span data-stu-id="251d4-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="251d4-124">Cree un túnel SSH al maestro de Swarm.</span><span class="sxs-lookup"><span data-stu-id="251d4-124">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="251d4-125">Reemplace `IPAddress` por la dirección IP del maestro de Swarm.</span><span class="sxs-lookup"><span data-stu-id="251d4-125">Replace `IPAddress` with the IP address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="251d4-126">Establezca la variable de entorno `DOCKER_HOST`.</span><span class="sxs-lookup"><span data-stu-id="251d4-126">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="251d4-127">De esta forma podrá ejecutar comandos docker en Docker Swarm sin tener que especificar el nombre del host.</span><span class="sxs-lookup"><span data-stu-id="251d4-127">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="251d4-128">Ahora está listo para ejecutar servicios de Docker en Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="251d4-128">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="251d4-129">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="251d4-129">Run the application</span></span>

<span data-ttu-id="251d4-130">Cree un archivo llamado `docker-compose.yaml` y copie en él el siguiente contenido.</span><span class="sxs-lookup"><span data-stu-id="251d4-130">Create a file named `docker-compose.yaml` and copy the following content into it.</span></span>

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="251d4-131">Ejecute el comando siguiente para crear el servicio Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="251d4-131">Run the following command to create the Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="251d4-132">Salida:</span><span class="sxs-lookup"><span data-stu-id="251d4-132">Output:</span></span>

```bash
Creating network "user_default" with the default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-the-application"></a><span data-ttu-id="251d4-133">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="251d4-133">Test the application</span></span>

<span data-ttu-id="251d4-134">Busque la dirección IP del grupo de agentes de Swarm para probar la aplicación Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="251d4-134">Browse to the IP address of the Swarm agent pool to test out the Azure Vote application.</span></span>

![Imagen de la exploración hasta Azure Vote](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="251d4-136">Eliminación de clúster</span><span class="sxs-lookup"><span data-stu-id="251d4-136">Delete cluster</span></span>
<span data-ttu-id="251d4-137">Cuando un clúster ya no se necesite, puede usar el comando [az group delete](/cli/azure/group#delete) para quitar el grupo de recursos, el servicio de contenedor y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="251d4-137">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="251d4-138">Obtención del código</span><span class="sxs-lookup"><span data-stu-id="251d4-138">Get the code</span></span>

<span data-ttu-id="251d4-139">En este tutorial de inicio rápido, se han usado imágenes de un contenedor creado previamente para crear un servicio de Docker.</span><span class="sxs-lookup"><span data-stu-id="251d4-139">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="251d4-140">El código de la aplicación relacionado, Dockerfile, y el archivo de Compose están disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="251d4-140">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="251d4-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="251d4-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="251d4-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="251d4-142">Next steps</span></span>

<span data-ttu-id="251d4-143">En este tutorial de inicio rápido, implementará un clúster de Docker Swarm y, en él, una aplicación de varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="251d4-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="251d4-144">Para aprender sobre la integración de Docker Swarm con Visual Studio Team Services, consulte el artículo sobre CI/CD con Docker Swarm y VSTS.</span><span class="sxs-lookup"><span data-stu-id="251d4-144">To learn about integrating Docker warm with Visual Studio Team Services, continue to the CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="251d4-145">Integración y entrega continuas con Docker Swarm y VSTS</span><span class="sxs-lookup"><span data-stu-id="251d4-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)