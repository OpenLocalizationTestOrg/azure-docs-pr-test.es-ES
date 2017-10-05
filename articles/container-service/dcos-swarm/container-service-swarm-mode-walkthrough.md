---
title: "Guía de inicio rápido: clúster de Azure Docker CE para Linux | Microsoft Docs"
description: "Aprenda rápidamente a crear un clúster de Docker CE para contenedores de Linux en Azure Container Service con la CLI de Azure."
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 7b8336e3865e7032e3ee0d5e4ee712bcb95aa4b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="4c407-103">Implementación del clúster de Docker CE</span><span class="sxs-lookup"><span data-stu-id="4c407-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="4c407-104">En esta guía de inicio rápido, se implementa un clúster de Docker CE mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c407-104">In this quick start, a Docker CE cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="4c407-105">A continuación, se ejecuta e implementa en el clúster una aplicación de varios contenedores que consta de un front-end web y una instancia de Redis.</span><span class="sxs-lookup"><span data-stu-id="4c407-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="4c407-106">Una vez finalizado el proceso, la aplicación es accesible a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="4c407-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="4c407-107">Docker CE en Azure Container Service se encuentra en versión preliminar y **no se debe usar con cargas de trabajo de producción**.</span><span class="sxs-lookup"><span data-stu-id="4c407-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="4c407-108">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="4c407-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="4c407-109">Si decide instalar y usar la CLI localmente, para esta guía de inicio rápido es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4c407-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4c407-110">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="4c407-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="4c407-111">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4c407-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="4c407-112">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4c407-112">Create a resource group</span></span>

<span data-ttu-id="4c407-113">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4c407-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4c407-114">Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c407-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="4c407-115">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *ukwest*.</span><span class="sxs-lookup"><span data-stu-id="4c407-115">The following example creates a resource group named *myResourceGroup* in the *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="4c407-116">Salida:</span><span class="sxs-lookup"><span data-stu-id="4c407-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="4c407-117">Creación de un clúster de Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="4c407-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="4c407-118">Cree un clúster de Docker CE en Azure Container Service con el comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="4c407-118">Create a Docker CE cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="4c407-119">En el ejemplo siguiente, se crea un clúster denominado *mySwarmCluster* con un nodo maestro de Linux y tres nodos de agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="4c407-119">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="4c407-120">Después de varios minutos, el comando se completa y devuelve información en formato json sobre el clúster.</span><span class="sxs-lookup"><span data-stu-id="4c407-120">After several minutes, the command completes and returns json formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="4c407-121">Conexión al clúster</span><span class="sxs-lookup"><span data-stu-id="4c407-121">Connect to the cluster</span></span>

<span data-ttu-id="4c407-122">A lo largo de este tutorial de inicio rápido, necesitará el FQDN del maestro de Docker Swarm y del grupo de agentes de Docker.</span><span class="sxs-lookup"><span data-stu-id="4c407-122">Throughout this quick start, you need the FQDN of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="4c407-123">Ejecute el siguiente comando para devolver los FQDN del maestro y del agente.</span><span class="sxs-lookup"><span data-stu-id="4c407-123">Run the following command to return both the master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="4c407-124">Salida:</span><span class="sxs-lookup"><span data-stu-id="4c407-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="4c407-125">Cree un túnel SSH al maestro de Swarm.</span><span class="sxs-lookup"><span data-stu-id="4c407-125">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="4c407-126">Reemplace `MasterFQDN` por la dirección de FQDN del maestro de Swarm.</span><span class="sxs-lookup"><span data-stu-id="4c407-126">Replace `MasterFQDN` with the FQDN address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="4c407-127">Establezca la variable de entorno `DOCKER_HOST`.</span><span class="sxs-lookup"><span data-stu-id="4c407-127">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="4c407-128">De esta forma podrá ejecutar comandos docker en Docker Swarm sin tener que especificar el nombre del host.</span><span class="sxs-lookup"><span data-stu-id="4c407-128">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="4c407-129">Ahora está listo para ejecutar servicios de Docker en Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="4c407-129">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="4c407-130">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4c407-130">Run the application</span></span>

<span data-ttu-id="4c407-131">Cree un archivo llamado `azure-vote.yaml` y copie en él el siguiente contenido.</span><span class="sxs-lookup"><span data-stu-id="4c407-131">Create a file named `azure-vote.yaml` and copy the following content into it.</span></span>


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="4c407-132">Ejecute el comando [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) para crear el servicio Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="4c407-132">Run the [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command to create the Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="4c407-133">Salida:</span><span class="sxs-lookup"><span data-stu-id="4c407-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="4c407-134">Use el comando [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) para devolver el estado de implementación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c407-134">Use the [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command to return the deployment status of the application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="4c407-135">Cuando el valor de `CURRENT STATE` de cada servicio sea `Running`, la aplicación está lista.</span><span class="sxs-lookup"><span data-stu-id="4c407-135">Once the `CURRENT STATE` of each service is `Running`, the application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-the-application"></a><span data-ttu-id="4c407-136">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4c407-136">Test the application</span></span>

<span data-ttu-id="4c407-137">Busque el FQDN del grupo de agentes de Swarm para probar la aplicación Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="4c407-137">Browse to the FQDN of the Swarm agent pool to test out the Azure Vote application.</span></span>

![Imagen de la exploración hasta Azure Vote](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="4c407-139">Eliminación de clúster</span><span class="sxs-lookup"><span data-stu-id="4c407-139">Delete cluster</span></span>
<span data-ttu-id="4c407-140">Cuando un clúster ya no se necesite, puede usar el comando [az group delete](/cli/azure/group#delete) para quitar el grupo de recursos, el servicio de contenedor y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4c407-140">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="4c407-141">Obtención del código</span><span class="sxs-lookup"><span data-stu-id="4c407-141">Get the code</span></span>

<span data-ttu-id="4c407-142">En este tutorial de inicio rápido, se han usado imágenes de un contenedor creado previamente para crear un servicio de Docker.</span><span class="sxs-lookup"><span data-stu-id="4c407-142">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="4c407-143">El código de la aplicación relacionado, Dockerfile, y el archivo de Compose están disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="4c407-143">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="4c407-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="4c407-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="4c407-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c407-145">Next steps</span></span>

<span data-ttu-id="4c407-146">En este tutorial de inicio rápido, implementará un clúster de Docker Swarm y, en él, una aplicación de varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="4c407-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="4c407-147">Para aprender sobre la integración de Docker Swarm con Visual Studio Team Services, consulte el artículo sobre CI/CD con Docker Swarm y VSTS.</span><span class="sxs-lookup"><span data-stu-id="4c407-147">To learn about integrating Docker warm with Visual Studio Team Services, continue to the CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4c407-148">Integración y entrega continuas con Docker Swarm y VSTS</span><span class="sxs-lookup"><span data-stu-id="4c407-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)