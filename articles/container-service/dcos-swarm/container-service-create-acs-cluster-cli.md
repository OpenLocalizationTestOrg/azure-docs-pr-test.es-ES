---
title: "aaaDeploy un clúster de contenedor de Docker - CLI de Azure | Documentos de Microsoft"
description: "Implementación de una solución Kubernetes, DC/OS o Docker Swarm en Azure Container Service mediante la CLI de Azure 2.0"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a><span data-ttu-id="7b801-103">Implementar un contenedor de Docker con hello Azure CLI 2.0 de solución de hospedaje</span><span class="sxs-lookup"><span data-stu-id="7b801-103">Deploy a Docker container hosting solution using hello Azure CLI 2.0</span></span>

<span data-ttu-id="7b801-104">Hola de uso `az acs` comandos de CLI de Azure 2.0 hello toocreate y administrar los clústeres en el servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b801-104">Use hello `az acs` commands in hello Azure CLI 2.0 toocreate and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="7b801-105">También puede implementar un clúster de servicio de contenedor de Azure mediante el uso de hello [portal de Azure](container-service-deployment.md) u Hola API de servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b801-105">You can also deploy an Azure Container Service cluster by using hello [Azure portal](container-service-deployment.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="7b801-106">Para obtener ayuda sobre `az acs` comandos, pasar hello `-h` comando tooany de parámetro.</span><span class="sxs-lookup"><span data-stu-id="7b801-106">For help on `az acs` commands, pass hello `-h` parameter tooany command.</span></span> <span data-ttu-id="7b801-107">Por ejemplo: `az acs create -h`.</span><span class="sxs-lookup"><span data-stu-id="7b801-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="7b801-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7b801-108">Prerequisites</span></span>
<span data-ttu-id="7b801-109">toocreate un clúster de servicio de contenedor de Azure con Hola 2.0 de CLI de Azure, debe:</span><span class="sxs-lookup"><span data-stu-id="7b801-109">toocreate an Azure Container Service cluster using hello Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="7b801-110">tener una cuenta de Azure ([obtenga aquí una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="7b801-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="7b801-111">tener instalado y configurado hello [2.0 de CLI de Azure](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="7b801-111">have installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="7b801-112">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="7b801-112">Get started</span></span> 
### <a name="log-in-tooyour-account"></a><span data-ttu-id="7b801-113">Inicie sesión en la cuenta de tooyour</span><span class="sxs-lookup"><span data-stu-id="7b801-113">Log in tooyour account</span></span>
```azurecli
az login 
```

<span data-ttu-id="7b801-114">Siga toolog de mensajes de Hola en forma interactiva.</span><span class="sxs-lookup"><span data-stu-id="7b801-114">Follow hello prompts toolog in interactively.</span></span> <span data-ttu-id="7b801-115">Para otro toolog métodos en, consulte [empezar a trabajar con Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7b801-115">For other methods toolog in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="7b801-116">Establecimiento de una suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="7b801-116">Set your Azure subscription</span></span>

<span data-ttu-id="7b801-117">Si tiene más de una suscripción de Azure, establezca suscripción predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b801-117">If you have more than one Azure subscription, set hello default subscription.</span></span> <span data-ttu-id="7b801-118">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7b801-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="7b801-119">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7b801-119">Create a resource group</span></span>
<span data-ttu-id="7b801-120">Se recomienda crear un grupo de recursos para cada clúster.</span><span class="sxs-lookup"><span data-stu-id="7b801-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="7b801-121">Especifique una región de Azure en la que Azure Container Service esté [disponible](https://azure.microsoft.com/en-us/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="7b801-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="7b801-122">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7b801-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="7b801-123">Salida es la siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="7b801-123">Output is similar toohello following:</span></span>

![Crear un grupo de recursos](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="7b801-125">Creación de un clúster de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7b801-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="7b801-126">toocreate un clúster, use `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="7b801-126">toocreate a cluster, use `az acs create`.</span></span>
<span data-ttu-id="7b801-127">Un nombre para el clúster de Hola y específicos de Hola Hola del grupo de recursos creado en el paso anterior de hello son parámetros obligatorios.</span><span class="sxs-lookup"><span data-stu-id="7b801-127">A name for hello cluster and hello name of hello resource group created in hello previous step are mandatory parameters.</span></span> 

<span data-ttu-id="7b801-128">Otras entradas son valores del conjunto toodefault (vea Hola después de la pantalla), a menos que se sobrescribe con sus respectivos conmutadores.</span><span class="sxs-lookup"><span data-stu-id="7b801-128">Other inputs are set toodefault values (see hello following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="7b801-129">Por ejemplo, orchestrator hello es establecer predeterminado tooDC/OS.</span><span class="sxs-lookup"><span data-stu-id="7b801-129">For example, hello orchestrator is set by default tooDC/OS.</span></span> <span data-ttu-id="7b801-130">Y si no se especifica uno, un prefijo de nombre DNS se crea basándose en nombre del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="7b801-130">And if you don't specify one, a DNS name prefix is created based on hello cluster name.</span></span>

![Uso de az acs create](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="7b801-132">Uso rápido de `acs create` con los valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="7b801-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="7b801-133">Si tiene un archivo de clave público SSH RSA `id_rsa.pub` en la ubicación predeterminada de hello (o crear uno para [OS X y Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../../virtual-machines/linux/ssh-from-windows.md)), utilice un comando similar al siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="7b801-133">If you have an SSH RSA public key file `id_rsa.pub` in hello default location (or created one for [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use a command like hello following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="7b801-134">Si no tiene una clave pública SSH, use este segundo comando.</span><span class="sxs-lookup"><span data-stu-id="7b801-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="7b801-135">Este comando con hello `--generate-ssh-keys` conmutador crea uno automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7b801-135">This command with hello `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="7b801-136">Después de escribir el comando de hello, espere unos 10 minutos para hello clúster toobe creado.</span><span class="sxs-lookup"><span data-stu-id="7b801-136">After you enter hello command, wait for about 10 minutes for hello cluster toobe created.</span></span> <span data-ttu-id="7b801-137">resultado del comando Hello incluye nombres de dominio completo (FQDN) del patrón de Hola y nodos de agente y un tooconnect toohello SSH comando primer patrón.</span><span class="sxs-lookup"><span data-stu-id="7b801-137">hello command output includes fully qualified domain names (FQDNs) of hello master and agent nodes and an SSH command tooconnect toohello first master.</span></span> <span data-ttu-id="7b801-138">Este es un resultado abreviado:</span><span class="sxs-lookup"><span data-stu-id="7b801-138">Here is abbreviated output:</span></span>

![Imagen del comando create de ACS](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="7b801-140">Hola [Kubernetes tutorial](../kubernetes/container-service-kubernetes-walkthrough.md) muestra cómo toouse `az acs create` con toocreate de valores de forma predeterminada un Kubernetes de clúster.</span><span class="sxs-lookup"><span data-stu-id="7b801-140">hello [Kubernetes walkthrough](../kubernetes/container-service-kubernetes-walkthrough.md) shows how toouse `az acs create` with default values toocreate a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="7b801-141">Administración de clústeres de ACS</span><span class="sxs-lookup"><span data-stu-id="7b801-141">Manage ACS clusters</span></span>

<span data-ttu-id="7b801-142">Uso adicional `az acs` comandos toomanage el clúster.</span><span class="sxs-lookup"><span data-stu-id="7b801-142">Use additional `az acs` commands toomanage your cluster.</span></span> <span data-ttu-id="7b801-143">Estos son algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="7b801-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="7b801-144">Lista de clústeres de una suscripción</span><span class="sxs-lookup"><span data-stu-id="7b801-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="7b801-145">Lista de clústeres de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7b801-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="7b801-147">Visualización de los detalles de un clúster del servicio de contenedor</span><span class="sxs-lookup"><span data-stu-id="7b801-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a><span data-ttu-id="7b801-149">Clúster de Hola de escala</span><span class="sxs-lookup"><span data-stu-id="7b801-149">Scale hello cluster</span></span>
<span data-ttu-id="7b801-150">Se permite la reducción y el escalado horizontales de nodos de agente.</span><span class="sxs-lookup"><span data-stu-id="7b801-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="7b801-151">Hola parámetro `new-agent-count` es Hola nuevo número de agentes en el clúster de hello ACS.</span><span class="sxs-lookup"><span data-stu-id="7b801-151">hello parameter `new-agent-count` is hello new number of agents in hello ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="7b801-153">Eliminación de un clúster del servicio de contenedor</span><span class="sxs-lookup"><span data-stu-id="7b801-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="7b801-154">Este comando no elimina todos los recursos (red y almacenamiento) creados durante la creación de servicio de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b801-154">This command does not delete all resources (network and storage) created while creating hello container service.</span></span> <span data-ttu-id="7b801-155">toodelete todos los recursos fácilmente, se recomienda implementar cada clúster en un grupo de recursos distinto.</span><span class="sxs-lookup"><span data-stu-id="7b801-155">toodelete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="7b801-156">A continuación, eliminar grupo de recursos de hello cuando ya no se necesita el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b801-156">Then, delete hello resource group when hello cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b801-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b801-157">Next steps</span></span>
<span data-ttu-id="7b801-158">Ahora que tiene un clúster funcionando, consulte los siguientes documentos para obtener información detallada sobre conexión y administración:</span><span class="sxs-lookup"><span data-stu-id="7b801-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="7b801-159">Conectar el clúster del servicio de contenedor de Azure tooan</span><span class="sxs-lookup"><span data-stu-id="7b801-159">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="7b801-160">Administración de contenedores con la API de REST</span><span class="sxs-lookup"><span data-stu-id="7b801-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="7b801-161">Administración de contenedores con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="7b801-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="7b801-162">Trabajo con Azure Container Service y Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7b801-162">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)