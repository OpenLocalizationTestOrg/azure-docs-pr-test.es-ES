---
title: aaaCreate el primer contenedor de instancias de contenedor de Azure | Documentos de Azure
description: Implemente y empiece a usar Azure Container Instances
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="a84f4-103">Creación del primer contenedor en Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="a84f4-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="a84f4-104">Instancias de contenedor Azure resulta fácil toocreate y administrar contenedores en Azure.</span><span class="sxs-lookup"><span data-stu-id="a84f4-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="a84f4-105">En este tutorial, creará un contenedor de Azure y exponerlo toohello internet con una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="a84f4-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="a84f4-106">Esta operación se completa en un solo comando.</span><span class="sxs-lookup"><span data-stu-id="a84f4-106">This operation is completed in a single command.</span></span> <span data-ttu-id="a84f4-107">En pocos segundos, verá lo siguiente en el explorador:</span><span class="sxs-lookup"><span data-stu-id="a84f4-107">Within just a few seconds, you will see this in your browser:</span></span>

![Aplicación implementada mediante Azure Container Instances vista en el explorador][aci-app-browser]

<span data-ttu-id="a84f4-109">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="a84f4-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a84f4-110">Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.12 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="a84f4-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="a84f4-111">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="a84f4-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a84f4-112">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a84f4-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="a84f4-113">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a84f4-113">Create a resource group</span></span>

<span data-ttu-id="a84f4-114">Azure Container Instances son recursos de Azure y se deben colocar en un grupo de recursos de Azure, una colección lógica en la que se implementan y administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a84f4-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="a84f4-115">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a84f4-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="a84f4-116">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="a84f4-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="a84f4-117">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="a84f4-117">Create a container</span></span>

<span data-ttu-id="a84f4-118">Para crear un contenedor debe especificar un nombre, una imagen de Docker y un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a84f4-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="a84f4-119">Puede exponer opcionalmente Hola contenedor toohello internet con una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="a84f4-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="a84f4-120">En este caso, se va a usar un contenedor que hospeda una aplicación web muy simple escrita en [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a84f4-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="a84f4-121">Dentro de unos segundos, debería obtener una solicitud de tooyour de respuesta.</span><span class="sxs-lookup"><span data-stu-id="a84f4-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="a84f4-122">Inicialmente, el contenedor de hello estará en un **crear** estado, pero debe comenzar en cuestión de segundos.</span><span class="sxs-lookup"><span data-stu-id="a84f4-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="a84f4-123">Puede comprobar el estado de hello mediante hello `show` comando:</span><span class="sxs-lookup"><span data-stu-id="a84f4-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="a84f4-124">En parte inferior de Hola de salida de hello, verá el estado de aprovisionamiento del contenedor de Hola y su dirección IP:</span><span class="sxs-lookup"><span data-stu-id="a84f4-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="a84f4-125">Una vez que el contenedor de hello mueve toohello **correcto** estado, puede llegar a él en el Explorador de hello mediante la dirección IP Hola proporcionada.</span><span class="sxs-lookup"><span data-stu-id="a84f4-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![Aplicación implementada mediante Azure Container Instances vista en el explorador][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="a84f4-127">Extraer registros de contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="a84f4-127">Pull hello container logs</span></span>

<span data-ttu-id="a84f4-128">Puede extraer registros Hola del contenedor de hello creada con hello `logs` comando:</span><span class="sxs-lookup"><span data-stu-id="a84f4-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="a84f4-129">Salida:</span><span class="sxs-lookup"><span data-stu-id="a84f4-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="a84f4-130">Eliminar el contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="a84f4-130">Delete hello container</span></span>

<span data-ttu-id="a84f4-131">Cuando haya terminado con el contenedor de hello, puede quitarlo mediante hello `delete` comando:</span><span class="sxs-lookup"><span data-stu-id="a84f4-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a84f4-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a84f4-132">Next steps</span></span>

<span data-ttu-id="a84f4-133">Todo de hello el código de contenedor de hello utilizado en esta guía de inicio rápido está disponible [en GitHub][app-github-repo], junto con su Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="a84f4-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="a84f4-134">Si desea que tootry creación usted mismo y su implementación tooAzure instancias de contenedor con hello del registro de contenedor de Azure, continuar con tutorial de toohello instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="a84f4-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a84f4-135">Tutoriales de Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="a84f4-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png