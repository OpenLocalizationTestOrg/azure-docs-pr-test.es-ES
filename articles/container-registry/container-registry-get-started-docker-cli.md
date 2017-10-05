---
title: "Inserción de imagen de Docker en el registro privado de Azure | Microsoft Docs"
description: "Inserción y extracción de imágenes de Docker en un registro de contenedor privado de Azure mediante la CLI de Docker"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07d4d72e94eda02e8594dfddb0e911eb0e63012d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="9dd8d-103">Inserción de la primera imagen en un registro de contenedor privado de Docker mediante la CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="9dd8d-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="9dd8d-104">Un registro de contenedor de Azure almacena y administra imágenes privadas de contenedor de [Docker](http://hub.docker.com), de una forma similar a la que [Docker Hub](https://hub.docker.com/) almacena imágenes públicas.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="9dd8d-105">Use la [interfaz de la línea de comandos de Docker](https://docs.docker.com/engine/reference/commandline/cli/) (CLI de Docker) para [iniciar sesión](https://docs.docker.com/engine/reference/commandline/login/), [insertar](https://docs.docker.com/engine/reference/commandline/push/), [extraer](https://docs.docker.com/engine/reference/commandline/pull/) y realizar otras operaciones en el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="9dd8d-106">Para más información sobre el entorno y los conceptos, consulte [la información general](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9dd8d-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="9dd8d-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9dd8d-107">Prerequisites</span></span>
* <span data-ttu-id="9dd8d-108">**Registro de contenedor de Azure**: cree un registro de contenedor en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="9dd8d-109">Por ejemplo, use [Azure Portal](container-registry-get-started-portal.md) o la [CLI de Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9dd8d-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="9dd8d-110">**CLI de docker**: para configurar el equipo local como un host de Docker y tener acceso a los comandos de la CLI de Docker, instale [Docker Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="9dd8d-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="9dd8d-111">Inicio de sesión en un registro</span><span class="sxs-lookup"><span data-stu-id="9dd8d-111">Log in to a registry</span></span>
<span data-ttu-id="9dd8d-112">Ejecute `docker login` para iniciar sesión en el registro de contenedor con sus [credenciales de registro](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9dd8d-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="9dd8d-113">En el ejemplo siguiente se pasa el identificador y la contraseña de una [entidad de servicio](../active-directory/active-directory-application-objects.md) de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="9dd8d-114">Por ejemplo, puede que haya asignado una entidad de servicio al registro para ver un escenario de automatización.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="9dd8d-115">Asegúrese de especificar el nombre completo del registro (todo en minúsculas).</span><span class="sxs-lookup"><span data-stu-id="9dd8d-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="9dd8d-116">En este ejemplo, es `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="9dd8d-117">Pasos para extraer e insertar una imagen</span><span class="sxs-lookup"><span data-stu-id="9dd8d-117">Steps to pull and push an image</span></span>
<span data-ttu-id="9dd8d-118">En el ejemplo siguiente se descarga la imagen de Nginx desde el registro público de Docker Hub, se le asigna una etiqueta para el registro de contenedor de Azure privado, se le inserta en el registro y luego se extrae de nuevo.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="9dd8d-119">**1. Extraiga la imagen oficial de Docker para Nginx**</span><span class="sxs-lookup"><span data-stu-id="9dd8d-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="9dd8d-120">En primer lugar, extraiga la imagen pública de Nginx al equipo local.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="9dd8d-121">**2. Inicie el contenedor de Nginx**</span><span class="sxs-lookup"><span data-stu-id="9dd8d-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="9dd8d-122">El comando siguiente inicia el contenedor local de Nginx de forma interactiva en el puerto 8080, permitiéndole ver la salida de Nginx.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="9dd8d-123">Quita el contenedor en ejecución una vez detenido.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="9dd8d-124">Vaya a [http://localhost:8080](http://localhost:8080) para ver el contenedor en ejecución.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="9dd8d-125">Se muestra una pantalla similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-125">You see a screen similar to the following one.</span></span>

![Nginx en un equipo local](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="9dd8d-127">Para detener el contenedor en ejecución, pulse [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="9dd8d-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="9dd8d-128">**3. Cree un alias de la imagen en el registro**</span><span class="sxs-lookup"><span data-stu-id="9dd8d-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="9dd8d-129">El siguiente comando crea un alias de la imagen, con una ruta de acceso completa al registro.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="9dd8d-130">Este ejemplo especifica el espacio de nombres `samples` para evitar el desorden en la raíz del registro.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="9dd8d-131">**4. Inserte la imagen en el registro**</span><span class="sxs-lookup"><span data-stu-id="9dd8d-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="9dd8d-132">**5. Extraiga la imagen del registro**</span><span class="sxs-lookup"><span data-stu-id="9dd8d-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="9dd8d-133">**6. Inicie el contenedor de Nginx del registro**</span><span class="sxs-lookup"><span data-stu-id="9dd8d-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="9dd8d-134">Vaya a [http://localhost:8080](http://localhost:8080) para ver el contenedor en ejecución.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="9dd8d-135">Para detener el contenedor en ejecución, pulse [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="9dd8d-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="9dd8d-136">**7. (Opcional) Quite la imagen**</span><span class="sxs-lookup"><span data-stu-id="9dd8d-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="9dd8d-137">Límites simultáneos</span><span class="sxs-lookup"><span data-stu-id="9dd8d-137">Concurrent Limits</span></span>
<span data-ttu-id="9dd8d-138">En algunos escenarios, la ejecución de llamadas de forma simultánea podría producir errores.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="9dd8d-139">La tabla siguiente contiene los límites de llamadas simultáneas con las operaciones "Insertar" y "Extraer" en el registro de contenedor de Azure:</span><span class="sxs-lookup"><span data-stu-id="9dd8d-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="9dd8d-140">Operación</span><span class="sxs-lookup"><span data-stu-id="9dd8d-140">Operation</span></span>  | <span data-ttu-id="9dd8d-141">Límite</span><span class="sxs-lookup"><span data-stu-id="9dd8d-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="9dd8d-142">EXTRAER</span><span class="sxs-lookup"><span data-stu-id="9dd8d-142">PULL</span></span>       | <span data-ttu-id="9dd8d-143">Hasta 10 extracciones simultáneas por registro</span><span class="sxs-lookup"><span data-stu-id="9dd8d-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="9dd8d-144">INSERTAR</span><span class="sxs-lookup"><span data-stu-id="9dd8d-144">PUSH</span></span>       | <span data-ttu-id="9dd8d-145">Hasta 5 inserciones simultáneas por registro</span><span class="sxs-lookup"><span data-stu-id="9dd8d-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9dd8d-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9dd8d-146">Next steps</span></span>
<span data-ttu-id="9dd8d-147">Ahora que conoce los fundamentos, ya está listo para empezar a usar el registro.</span><span class="sxs-lookup"><span data-stu-id="9dd8d-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="9dd8d-148">Por ejemplo, empiece por implementar imágenes del contenedor en un clúster de [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="9dd8d-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
