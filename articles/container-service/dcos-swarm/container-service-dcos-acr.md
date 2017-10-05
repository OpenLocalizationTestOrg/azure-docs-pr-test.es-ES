---
title: "Usar ACR con un clúster DC/OS de Azure | Microsoft Docs"
description: "Use un Azure Container Registry con un clúster DC/OS en Azure Container Service"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, contenedores, microservicios, Mesos, Azure, recurso compartido de archivos, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 618d32ca919e50d41b85c800225fe72c3b94e537
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-acr-with-a-dcos-cluster-to-deploy-your-application"></a><span data-ttu-id="c9823-104">Use ACR con un clúster de DC/OS para implementar la aplicación</span><span class="sxs-lookup"><span data-stu-id="c9823-104">Use ACR with a DC/OS cluster to deploy your application</span></span>

<span data-ttu-id="c9823-105">En este artículo, exploraremos cómo usar Azure Container Registry con un clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="c9823-105">In this article, we explore how to use Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="c9823-106">Usar ACR le permite almacenar y administrar imágenes del contenedor de forma privada.</span><span class="sxs-lookup"><span data-stu-id="c9823-106">Using ACR allows you to privately store and manage container images.</span></span> <span data-ttu-id="c9823-107">En este tutorial se describen las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9823-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c9823-108">Implementación de Azure Container Registry (en caso de ser necesaria)</span><span class="sxs-lookup"><span data-stu-id="c9823-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="c9823-109">Configuración de la autenticación de ACR en un clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="c9823-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="c9823-110">Carga de una imagen en Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c9823-110">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="c9823-111">Ejecución de una imagen de contenedor de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c9823-111">Run a container image from the Azure Container Registry</span></span>

<span data-ttu-id="c9823-112">Necesita un clúster de DC/OS de ACS para completar los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c9823-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="c9823-113">Si es necesario, este [script de ejemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) puede crear uno.</span><span class="sxs-lookup"><span data-stu-id="c9823-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="c9823-114">Para realizar este tutorial es necesaria la versión 2.0.4 o superior de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9823-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c9823-115">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="c9823-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="c9823-116">Si necesita actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c9823-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="c9823-117">Implementación de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c9823-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="c9823-118">Si es necesario, cree un Azure Container Registry con el comando [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="c9823-118">If needed, create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="c9823-119">En el ejemplo siguiente, se crea un registro con un nombre generado de forma aleatoria.</span><span class="sxs-lookup"><span data-stu-id="c9823-119">The following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="c9823-120">El registro también se configura con una cuenta de administrador mediante el argumento `--admin-enabled`.</span><span class="sxs-lookup"><span data-stu-id="c9823-120">The registry is also configured with an admin account using the `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="c9823-121">Una vez creado el registro, la CLI de Azure da como resultado datos similares a los que aparecen a continuación.</span><span class="sxs-lookup"><span data-stu-id="c9823-121">Once the registry has been created, the Azure CLI outputs data similar to the following.</span></span> <span data-ttu-id="c9823-122">Anote `name` y `loginServer`, ya que se usarán en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="c9823-122">Take note of the `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="c9823-123">Obtenga las credenciales del registro de contenedor mediante el comando [az acr credential show](/cli/azure/acr/credential).</span><span class="sxs-lookup"><span data-stu-id="c9823-123">Get the container registry credentials using the [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="c9823-124">Sustituya el `--name` con el que anotó en el último paso.</span><span class="sxs-lookup"><span data-stu-id="c9823-124">Substitute the `--name` with the one noted in the last step.</span></span> <span data-ttu-id="c9823-125">Tome nota de una contraseña, ya que es necesaria más adelante.</span><span class="sxs-lookup"><span data-stu-id="c9823-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="c9823-126">Para obtener más información sobre Azure Container Registry, consulte [Introducción a los registros privados del contenedor Docker](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="c9823-126">For more information on Azure Container Registry, see [Introduction to private Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="c9823-127">Administración de la autenticación de ACR</span><span class="sxs-lookup"><span data-stu-id="c9823-127">Manage ACR authentication</span></span>

<span data-ttu-id="c9823-128">La manera convencional de insertar y extraer una imagen de un registro privado es, en primer lugar, autenticarse en el registro.</span><span class="sxs-lookup"><span data-stu-id="c9823-128">The conventional way to push and pull image from a private registry is to first authenticate with the registry.</span></span> <span data-ttu-id="c9823-129">Para ello, usaría el comando `docker login` en cualquier cliente que necesite para tener acceso al registro privado.</span><span class="sxs-lookup"><span data-stu-id="c9823-129">To do so, you would use the `docker login` command on any client that needs to access the private registry.</span></span> <span data-ttu-id="c9823-130">Debido a que el clúster de DC/OS puede contener muchos nodos, los que deben autenticarse con ACR, es útil automatizar este proceso en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="c9823-130">Because a DC/OS cluster can contain many nodes, all of which need to be authenticated with the ACR, it is helpful to automate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="c9823-131">Creación de almacenamiento compartido</span><span class="sxs-lookup"><span data-stu-id="c9823-131">Create shared storage</span></span>

<span data-ttu-id="c9823-132">Este proceso utiliza un recurso compartido de archivos de Azure que se montó en cada nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="c9823-132">This process uses an Azure file share that has been mounted on each node in the cluster.</span></span> <span data-ttu-id="c9823-133">Si aún no se ha configurado el almacenamiento compartido, consulte [Configuración de un recurso compartido de archivos dentro de un clúster de DC/OS](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="c9823-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="c9823-134">Configuración de la autenticación de ACR</span><span class="sxs-lookup"><span data-stu-id="c9823-134">Configure ACR authentication</span></span>

<span data-ttu-id="c9823-135">En primer lugar, obtenga el FQDN del patrón de DC/OS y guárdelo en una variable.</span><span class="sxs-lookup"><span data-stu-id="c9823-135">First, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="c9823-136">Cree una conexión SSH con el patrón (o el primer patrón) del clúster basado en DC/OS.</span><span class="sxs-lookup"><span data-stu-id="c9823-136">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="c9823-137">Actualice el nombre de usuario si se utilizó un valor no predeterminado al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="c9823-137">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="c9823-138">Ejecute el siguiente comando para iniciar sesión en Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="c9823-138">Run the following command to login to the Azure Container Registry.</span></span> <span data-ttu-id="c9823-139">Reemplace el `--username` con el nombre del registro del contenedor y la `--password` con una de las contraseñas proporcionadas.</span><span class="sxs-lookup"><span data-stu-id="c9823-139">Replace the `--username` with the name of the container registry, and the `--password` with one of the provided passwords.</span></span> <span data-ttu-id="c9823-140">Reemplace el último argumento *mycontainerregistry.azurecr.io* en el ejemplo con el nombre loginServer del registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="c9823-140">Replace the last argument *mycontainerregistry.azurecr.io* in the example with the loginServer name of the container registry.</span></span> 

<span data-ttu-id="c9823-141">Este comando almacena los valores de autenticación localmente en la ruta de acceso `~/.docker`.</span><span class="sxs-lookup"><span data-stu-id="c9823-141">This command stores the authentication values locally under the `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="c9823-142">Cree un archivo comprimido que contenga los valores de autenticación del contenedor de registro.</span><span class="sxs-lookup"><span data-stu-id="c9823-142">Create a compressed file that contains the container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="c9823-143">Copie este archivo en el almacenamiento compartido del clúster.</span><span class="sxs-lookup"><span data-stu-id="c9823-143">Copy this file to the cluster shared storage.</span></span> <span data-ttu-id="c9823-144">Este paso hace que el archivo esté disponible en todos los nodos del clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="c9823-144">This step makes the file available on all nodes of the DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-to-acr"></a><span data-ttu-id="c9823-145">Carga de la imagen a ACR</span><span class="sxs-lookup"><span data-stu-id="c9823-145">Upload image to ACR</span></span>

<span data-ttu-id="c9823-146">Ahora desde una máquina de desarrollo, o cualquier otro sistema con Docker instalado, cree una imagen y cárguela en Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="c9823-146">Now from a development machine, or any other system with Docker installed, create an image and upload it to the Azure Container Registry.</span></span>

<span data-ttu-id="c9823-147">Cree un contenedor a partir de la imagen de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c9823-147">Create a container from the Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="c9823-148">Ahora capture el contenedor en una nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="c9823-148">Now capture the container into a new image.</span></span> <span data-ttu-id="c9823-149">El nombre de la imagen debe incluir el nombre `loginServer` del registro de contenedor con un formato de `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="c9823-149">The image name needs to include the `loginServer` name of the container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="c9823-150">Inicie sesión en Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="c9823-150">Login into the Azure Container Registry.</span></span> <span data-ttu-id="c9823-151">Reemplace el nombre con el nombre loginServer, el nombre de usuario con el nombre del registro de contenedor, y la contraseña con una de las contraseñas proporcionadas.</span><span class="sxs-lookup"><span data-stu-id="c9823-151">Replace the name with the loginServer name, the --username with the name of the container registry, and the --password with one of the provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="c9823-152">Finalmente, cargue la imagen en el registro de ACR.</span><span class="sxs-lookup"><span data-stu-id="c9823-152">Finally, upload the image to the ACR registry.</span></span> <span data-ttu-id="c9823-153">En este ejemplo, se carga una imagen llamada dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="c9823-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="c9823-154">Ejecución de una imagen desde ACR</span><span class="sxs-lookup"><span data-stu-id="c9823-154">Run an image from ACR</span></span>

<span data-ttu-id="c9823-155">Para utilizar una imagen del registro ACR, cree un archivo de nombres *acrDemo.json* y copie el siguiente texto en él.</span><span class="sxs-lookup"><span data-stu-id="c9823-155">To use an image from the ACR registry, create a file names *acrDemo.json* and copy the following text into it.</span></span> <span data-ttu-id="c9823-156">Reemplace el nombre de la imagen con el nombre loginServer del contenedor de registro y el nombre de la imagen. Por ejemplo, `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="c9823-156">Replace the image name with the container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="c9823-157">Tome nota de la propiedad `uris`.</span><span class="sxs-lookup"><span data-stu-id="c9823-157">Take note of the `uris` property.</span></span> <span data-ttu-id="c9823-158">Esta propiedad contiene la ubicación del archivo de autenticación del registro de contenedor, que en este caso es el recurso compartido de archivos de Azure que está montado en cada nodo del clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="c9823-158">This property holds the location of the container registry authentication file, which in this case is the Azure file share that is mounted on each node in the DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="c9823-159">Implemente la aplicación con la CLI de DC/OC.</span><span class="sxs-lookup"><span data-stu-id="c9823-159">Deploy the application with the DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="c9823-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9823-160">Next steps</span></span>

<span data-ttu-id="c9823-161">En este tutorial, configuró DC/OS para usar Azure Container Registry, incluidas las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="c9823-161">In this tutorial you have configure DC/OS to use Azure Container Registry including the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c9823-162">Implementación de Azure Container Registry (en caso de ser necesaria)</span><span class="sxs-lookup"><span data-stu-id="c9823-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="c9823-163">Configuración de la autenticación de ACR en un clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="c9823-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="c9823-164">Carga de una imagen en Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c9823-164">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="c9823-165">Ejecución de una imagen de contenedor de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c9823-165">Run a container image from the Azure Container Registry</span></span>
