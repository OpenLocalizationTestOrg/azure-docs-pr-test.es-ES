---
title: "aaaQuickstart - clúster de Azure Docker CE para Linux | Documentos de Microsoft"
description: "Aprender rápidamente toocreate un clúster de Docker CE para contenedores de Linux en el servicio de contenedor de Azure con hello CLI de Azure."
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
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="29ba7-103">Implementación del clúster de Docker CE</span><span class="sxs-lookup"><span data-stu-id="29ba7-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="29ba7-104">En esta guía de inicio rápido, un clúster de CE de Docker se implementa mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="29ba7-104">In this quick start, a Docker CE cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="29ba7-105">Una aplicación de contenedor múltiples que consta de front-end web y una instancia de Redis es, a continuación, implementar y ejecutar en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="29ba7-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="29ba7-106">Una vez completado, la aplicación hello es accesible a través de internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="29ba7-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="29ba7-107">Docker CE en Azure Container Service se encuentra en versión preliminar y **no se debe usar con cargas de trabajo de producción**.</span><span class="sxs-lookup"><span data-stu-id="29ba7-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="29ba7-108">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="29ba7-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="29ba7-109">Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="29ba7-109">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="29ba7-110">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="29ba7-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="29ba7-111">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="29ba7-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="29ba7-112">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="29ba7-112">Create a resource group</span></span>

<span data-ttu-id="29ba7-113">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="29ba7-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="29ba7-114">Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="29ba7-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="29ba7-115">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *ukwest* ubicación.</span><span class="sxs-lookup"><span data-stu-id="29ba7-115">hello following example creates a resource group named *myResourceGroup* in hello *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="29ba7-116">Salida:</span><span class="sxs-lookup"><span data-stu-id="29ba7-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="29ba7-117">Creación de un clúster de Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="29ba7-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="29ba7-118">Crear un clúster de CE de Docker en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="29ba7-118">Create a Docker CE cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="29ba7-119">Hello en el ejemplo siguiente se crea un clúster denominado *mySwarmCluster* con un Linux maestro de nodo y tres nodos de agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="29ba7-119">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="29ba7-120">Tras varios minutos, comando hello completa y devuelve información de formato json sobre clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="29ba7-120">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="29ba7-121">Conectar el clúster toohello</span><span class="sxs-lookup"><span data-stu-id="29ba7-121">Connect toohello cluster</span></span>

<span data-ttu-id="29ba7-122">En esta guía de inicio rápido, deberá Hola FQDN del maestro de hello Docker Swarm y grupo de agente de Docker de Hola.</span><span class="sxs-lookup"><span data-stu-id="29ba7-122">Throughout this quick start, you need hello FQDN of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="29ba7-123">Ejecute hello siguiente comando tooreturn ambos Hola FQDN maestra y el agente.</span><span class="sxs-lookup"><span data-stu-id="29ba7-123">Run hello following command tooreturn both hello master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="29ba7-124">Salida:</span><span class="sxs-lookup"><span data-stu-id="29ba7-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="29ba7-125">Crear un SSH conjunto maestro de túnel toohello.</span><span class="sxs-lookup"><span data-stu-id="29ba7-125">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="29ba7-126">Reemplace `MasterFQDN` con la dirección FQDN de hello del maestro de conjunto de Hola.</span><span class="sxs-lookup"><span data-stu-id="29ba7-126">Replace `MasterFQDN` with hello FQDN address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="29ba7-127">Conjunto hello `DOCKER_HOST` variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="29ba7-127">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="29ba7-128">Esto le permite comandos de docker de toorun contra Hola Docker Swarm sin necesidad de toospecify Hola nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="29ba7-128">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="29ba7-129">Ya estás listo toorun servicios de Docker en hello Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="29ba7-129">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="29ba7-130">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="29ba7-130">Run hello application</span></span>

<span data-ttu-id="29ba7-131">Cree un archivo denominado `azure-vote.yaml` y Hola copia siguen contenido en él.</span><span class="sxs-lookup"><span data-stu-id="29ba7-131">Create a file named `azure-vote.yaml` and copy hello following content into it.</span></span>


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

<span data-ttu-id="29ba7-132">Ejecute hello [implementar pila docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) comando servicio de toocreate Hola voto de Azure.</span><span class="sxs-lookup"><span data-stu-id="29ba7-132">Run hello [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command toocreate hello Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="29ba7-133">Salida:</span><span class="sxs-lookup"><span data-stu-id="29ba7-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="29ba7-134">Hola de uso [docker ps de pila](https://docs.docker.com/engine/reference/commandline/stack_ps/) comando estado de implementación de hello tooreturn de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="29ba7-134">Use hello [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command tooreturn hello deployment status of hello application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="29ba7-135">Una vez Hola `CURRENT STATE` de cada servicio es `Running`, aplicación hello está listo.</span><span class="sxs-lookup"><span data-stu-id="29ba7-135">Once hello `CURRENT STATE` of each service is `Running`, hello application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a><span data-ttu-id="29ba7-136">Probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="29ba7-136">Test hello application</span></span>

<span data-ttu-id="29ba7-137">Examinar toohello FQDN del grupo de agente de hello conjunto tootest out Hola aplicación voto de Azure.</span><span class="sxs-lookup"><span data-stu-id="29ba7-137">Browse toohello FQDN of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Imagen de la exploración tooAzure voto](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="29ba7-139">Eliminación de clúster</span><span class="sxs-lookup"><span data-stu-id="29ba7-139">Delete cluster</span></span>
<span data-ttu-id="29ba7-140">Cuando ya no se necesita el clúster hello, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, servicio de contenedor y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="29ba7-140">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="29ba7-141">Obtener el código de hello</span><span class="sxs-lookup"><span data-stu-id="29ba7-141">Get hello code</span></span>

<span data-ttu-id="29ba7-142">En esta guía de inicio rápido, imágenes del contenedor creada previamente han sido toocreate usa un servicio de Docker.</span><span class="sxs-lookup"><span data-stu-id="29ba7-142">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="29ba7-143">Hola relacionadas con código de aplicación, Dockerfile, y crear archivos están disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="29ba7-143">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="29ba7-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="29ba7-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="29ba7-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29ba7-145">Next steps</span></span>

<span data-ttu-id="29ba7-146">En esta guía de inicio rápido, implementar un clúster de Docker Swarm e implementa una aplicación de contenedor de varios tooit.</span><span class="sxs-lookup"><span data-stu-id="29ba7-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="29ba7-147">toolearn sobre la integración de Docker activa con Visual Studio Team Services, continuar toohello CI/CD con Docker Swarm y VSTS.</span><span class="sxs-lookup"><span data-stu-id="29ba7-147">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29ba7-148">Integración y entrega continuas con Docker Swarm y VSTS</span><span class="sxs-lookup"><span data-stu-id="29ba7-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)