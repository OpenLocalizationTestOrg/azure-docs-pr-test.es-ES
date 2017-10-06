---
title: "aaaUsing ACR con un clúster de Azure DC/OS | Documentos de Microsoft"
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
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="158d9-104">Usar ACR con un toodeploy de clúster de DC/OS la aplicación</span><span class="sxs-lookup"><span data-stu-id="158d9-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="158d9-105">En este artículo, exploraremos cómo toouse del registro de contenedor de Azure con un clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="158d9-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="158d9-106">Uso de ACR permite tooprivately almacén y administrar imágenes del contenedor.</span><span class="sxs-lookup"><span data-stu-id="158d9-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="158d9-107">Este tutorial trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="158d9-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="158d9-108">Implementación de Azure Container Registry (en caso de ser necesaria)</span><span class="sxs-lookup"><span data-stu-id="158d9-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="158d9-109">Configuración de la autenticación de ACR en un clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="158d9-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="158d9-110">Cargar un toohello de imagen del registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="158d9-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="158d9-111">Ejecutar una imagen de contenedor de hello del registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="158d9-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="158d9-112">Necesita un controlador de dominio ACS/OS hello toocomplete de clúster de los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="158d9-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="158d9-113">Si es necesario, este [script de ejemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) puede crear uno.</span><span class="sxs-lookup"><span data-stu-id="158d9-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="158d9-114">Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="158d9-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="158d9-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="158d9-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="158d9-116">Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="158d9-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="158d9-117">Implementación de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="158d9-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="158d9-118">Si es necesario, cree un registro de contenedor de Azure con hello [crear acr az](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="158d9-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="158d9-119">Hello en el ejemplo siguiente se crea un registro con un generar nombre de forma aleatoria.</span><span class="sxs-lookup"><span data-stu-id="158d9-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="158d9-120">registro de Hello también se configura con una cuenta de administrador con hello `--admin-enabled` argumento.</span><span class="sxs-lookup"><span data-stu-id="158d9-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="158d9-121">Una vez que se ha creado el registro de hello, Hola CLI de Azure da como resultado siguiente toohello similares de datos.</span><span class="sxs-lookup"><span data-stu-id="158d9-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="158d9-122">Tome nota de hello `name` y `loginServer`, se usan en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="158d9-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

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

<span data-ttu-id="158d9-123">Obtener credenciales de registro de contenedor hello mediante hello [show de credencial de acr az](/cli/azure/acr/credential) comando.</span><span class="sxs-lookup"><span data-stu-id="158d9-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="158d9-124">Hola sustituto `--name` con hello uno anotó en el último paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="158d9-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="158d9-125">Tome nota de una contraseña, ya que es necesaria más adelante.</span><span class="sxs-lookup"><span data-stu-id="158d9-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="158d9-126">Para obtener más información acerca del registro de contenedor de Azure, consulte [registros de contenedor de Docker de introducción tooprivate](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="158d9-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="158d9-127">Administración de la autenticación de ACR</span><span class="sxs-lookup"><span data-stu-id="158d9-127">Manage ACR authentication</span></span>

<span data-ttu-id="158d9-128">imagen toopush y extracción de un registro privado es toofirst de forma convencional de Hello autenticar con registro de hello.</span><span class="sxs-lookup"><span data-stu-id="158d9-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="158d9-129">toodo por lo tanto, se usaría hello `docker login` comando en cualquier cliente que necesita del registro de tooaccess Hola privada.</span><span class="sxs-lookup"><span data-stu-id="158d9-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="158d9-130">Dado que un clúster de DC/OS puede contener muchos nodos, todos ellos necesitan toobe autenticado con hello ACR, resulta útil tooautomate este proceso a través de cada nodo.</span><span class="sxs-lookup"><span data-stu-id="158d9-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="158d9-131">Creación de almacenamiento compartido</span><span class="sxs-lookup"><span data-stu-id="158d9-131">Create shared storage</span></span>

<span data-ttu-id="158d9-132">Este proceso utiliza un recurso compartido de archivos de Azure que se ha montado en cada nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="158d9-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="158d9-133">Si aún no se ha configurado el almacenamiento compartido, consulte [Configuración de un recurso compartido de archivos dentro de un clúster de DC/OS](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="158d9-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="158d9-134">Configuración de la autenticación de ACR</span><span class="sxs-lookup"><span data-stu-id="158d9-134">Configure ACR authentication</span></span>

<span data-ttu-id="158d9-135">En primer lugar, obtenga Hola FQDN de Hola DC/OS maestro y almacenarlo en una variable.</span><span class="sxs-lookup"><span data-stu-id="158d9-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="158d9-136">Crear una conexión SSH con hello (Hola primera maestra o) del clúster basadas en DC/OS.</span><span class="sxs-lookup"><span data-stu-id="158d9-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="158d9-137">Actualizar nombre de usuario de hello si se utilizó un valor no predeterminado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="158d9-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="158d9-138">Siguiente ejecución Hola comando toologin toohello del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="158d9-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="158d9-139">Reemplace hello `--username` por nombre de Hola de registro de contenedor de Hola y Hola `--password` con una de las contraseñas de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="158d9-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="158d9-140">Reemplace el último argumento de hello *mycontainerregistry.azurecr.io* en ejemplo de Hola con nombre de hello loginServer de registro de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="158d9-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="158d9-141">Este comando almacena los valores de autenticación de hello localmente en hello `~/.docker` ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="158d9-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="158d9-142">Crear un archivo comprimido que contiene los valores de autenticación de hello contenedor del registro.</span><span class="sxs-lookup"><span data-stu-id="158d9-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="158d9-143">Copie este almacenamiento de clúster compartido de archivo toohello.</span><span class="sxs-lookup"><span data-stu-id="158d9-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="158d9-144">Este paso realiza archivo hello disponible en todos los nodos del clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="158d9-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="158d9-145">Cargar imagen tooACR</span><span class="sxs-lookup"><span data-stu-id="158d9-145">Upload image tooACR</span></span>

<span data-ttu-id="158d9-146">Ahora desde un equipo de desarrollo, o cualquier otro sistema con Docker instalado, cree una imagen y cargarla toohello del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="158d9-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="158d9-147">Crear un contenedor de imagen de Ubuntu Hola.</span><span class="sxs-lookup"><span data-stu-id="158d9-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="158d9-148">Ahora captura Hola contenedor en una nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="158d9-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="158d9-149">nombre de la imagen de Hello necesita hello tooinclude `loginServer` nombre de hello contenedor registrywith un formato de `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="158d9-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="158d9-150">Inicio de sesión en hello del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="158d9-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="158d9-151">Sustituir el nombre de Hola por hello loginServer, Hola: nombre de usuario con el nombre de Hola de registro de contenedor de Hola y Hola--contraseña con una de las contraseñas de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="158d9-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="158d9-152">Por último, cargue el registro de hello imágenes toohello ACR.</span><span class="sxs-lookup"><span data-stu-id="158d9-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="158d9-153">En este ejemplo, se carga una imagen llamada dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="158d9-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="158d9-154">Ejecución de una imagen desde ACR</span><span class="sxs-lookup"><span data-stu-id="158d9-154">Run an image from ACR</span></span>

<span data-ttu-id="158d9-155">toouse una imagen desde el registro ACR hello, cree un archivo de nombres *acrDemo.json* y Hola copia siguiendo el texto en él.</span><span class="sxs-lookup"><span data-stu-id="158d9-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="158d9-156">Reemplazar el nombre de la imagen de Hola con nombre de loginServer de hello contenedor del registro y el nombre de la imagen, por ejemplo `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="158d9-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="158d9-157">Tome nota de hello `uris` propiedad.</span><span class="sxs-lookup"><span data-stu-id="158d9-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="158d9-158">Esta propiedad contiene la ubicación de Hola Hola contenedor autenticación del archivo registro, que en este caso es el recurso compartido de archivos de Azure de Hola que está montado en cada nodo de clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="158d9-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

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

<span data-ttu-id="158d9-159">Implementar aplicación hello con hello DC/OC CLI.</span><span class="sxs-lookup"><span data-stu-id="158d9-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="158d9-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="158d9-160">Next steps</span></span>

<span data-ttu-id="158d9-161">En este tutorial ha configurar toouse DC/OS tareas de registro de contenedor de Azure incluidos Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="158d9-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="158d9-162">Implementación de Azure Container Registry (en caso de ser necesaria)</span><span class="sxs-lookup"><span data-stu-id="158d9-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="158d9-163">Configuración de la autenticación de ACR en un clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="158d9-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="158d9-164">Cargar un toohello de imagen del registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="158d9-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="158d9-165">Ejecutar una imagen de contenedor de hello del registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="158d9-165">Run a container image from hello Azure Container Registry</span></span>
