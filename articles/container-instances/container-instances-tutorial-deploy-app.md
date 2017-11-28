---
title: "tutorial de instancias de contenedor de aaaAzure - implementar aplicación | Documentos de Microsoft"
description: "Tutorial de Azure Container Instances: implementación de aplicación"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="b5d87-103">Implementar un contenedor de instancias de contenedor tooAzure</span><span class="sxs-lookup"><span data-stu-id="b5d87-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="b5d87-104">Se trata de hello última de un tutorial de tres partes.</span><span class="sxs-lookup"><span data-stu-id="b5d87-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="b5d87-105">En las secciones anteriores, [una imagen de contenedor se creó](container-instances-tutorial-prepare-app.md) y [inserta tooan del registro de contenedor de Azure](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="b5d87-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="b5d87-106">En esta sección, se finaliza el tutorial de hello mediante la implementación de contenedor de hello tooAzure instancias de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b5d87-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="b5d87-107">Los pasos completados incluyen:</span><span class="sxs-lookup"><span data-stu-id="b5d87-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5d87-108">Definición de un grupo de contenedores mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b5d87-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="b5d87-109">Implementar grupo de contenedor de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b5d87-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="b5d87-110">Visualización de los registros de contenedores</span><span class="sxs-lookup"><span data-stu-id="b5d87-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="b5d87-111">Implementar contenedor de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b5d87-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="b5d87-112">Hola CLI de Azure permite la implementación de un contenedor de tooAzure instancias de contenedor en un solo comando.</span><span class="sxs-lookup"><span data-stu-id="b5d87-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="b5d87-113">Puesto que se hospeda la imagen de contenedor de hello en Hola privada del registro de contenedor de Azure, debe incluir hello las credenciales necesarias tooaccess lo.</span><span class="sxs-lookup"><span data-stu-id="b5d87-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="b5d87-114">En caso de ser necesario, puede consultarlas tal como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="b5d87-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="b5d87-115">Servidor de inicio de sesión en el registro de contenedor (actualice con su nombre de registro):</span><span class="sxs-lookup"><span data-stu-id="b5d87-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="b5d87-116">Contraseña del registro de contenedor:</span><span class="sxs-lookup"><span data-stu-id="b5d87-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="b5d87-117">toodeploy la imagen de contenedor del registro de contenedor de hello con un recurso de solicitud de 1 núcleo de CPU y 1GB de memoria, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="b5d87-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="b5d87-118">En cuestión de segundos, recibirá una respuesta inicial de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b5d87-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="b5d87-119">estado de hello tooview de implementación de hello, use:</span><span class="sxs-lookup"><span data-stu-id="b5d87-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="b5d87-120">Podemos seguir ejecutando este comando hasta que se cambia el estado de Hola de *pendiente* demasiado*ejecutando*.</span><span class="sxs-lookup"><span data-stu-id="b5d87-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="b5d87-121">Después, ya se puede continuar.</span><span class="sxs-lookup"><span data-stu-id="b5d87-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="b5d87-122">Ver los registros de aplicación y el contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="b5d87-122">View hello application and container logs</span></span>

<span data-ttu-id="b5d87-123">Cuando se complete correctamente la implementación de hello, abra la dirección IP del explorador toohello que se muestra en la salida de hello de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b5d87-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Aplicación de Hello world en el Explorador de Hola][aci-app-browser]

<span data-ttu-id="b5d87-125">También puede ver la salida de registro de hello de contenedor de hello:</span><span class="sxs-lookup"><span data-stu-id="b5d87-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="b5d87-126">Salida:</span><span class="sxs-lookup"><span data-stu-id="b5d87-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="b5d87-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5d87-127">Next steps</span></span>

<span data-ttu-id="b5d87-128">En este tutorial, ha completado proceso hello de la implementación de su tooAzure contenedores instancias de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b5d87-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="b5d87-129">se completaron Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b5d87-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5d87-130">Implementación de contenedor de Hola desde el registro de contenedor de Azure con el Hola Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b5d87-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="b5d87-131">Ver aplicación hello en el Explorador de Hola</span><span class="sxs-lookup"><span data-stu-id="b5d87-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="b5d87-132">Visualización de registros de contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="b5d87-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
