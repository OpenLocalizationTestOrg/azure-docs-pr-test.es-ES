---
title: aaaPush Docker imagen tooprivate del registro de Azure | Documentos de Microsoft
description: "Inserción y extracción de Docker del registro del contenedor privado de tooa de imágenes en Azure con hello CLI de Docker"
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
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="ec548-103">Insertar el primera imagen tooa privada Docker contenedor registro mediante Hola CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="ec548-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="ec548-104">Un registro de contenedor de Azure almacena y administra privado [Docker](http://hub.docker.com) imágenes del contenedor, toohello similar forma [Docker Hub](https://hub.docker.com/) almacena imágenes públicas de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec548-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="ec548-105">Usar hello [interfaz de línea de comandos de Docker](https://docs.docker.com/engine/reference/commandline/cli/) (CLI de Docker) para [inicio de sesión](https://docs.docker.com/engine/reference/commandline/login/), [inserción](https://docs.docker.com/engine/reference/commandline/push/), [extracción](https://docs.docker.com/engine/reference/commandline/pull/)y otras operaciones en el contenedor registro.</span><span class="sxs-lookup"><span data-stu-id="ec548-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="ec548-106">Para obtener más datos y conceptos, vea [Hola información general](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ec548-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="ec548-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ec548-107">Prerequisites</span></span>
* <span data-ttu-id="ec548-108">**Registro de contenedor de Azure**: cree un registro de contenedor en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ec548-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="ec548-109">Por ejemplo, usar hello [portal de Azure](container-registry-get-started-portal.md) o hello [CLI de Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ec548-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="ec548-110">**CLI de docker** -tooset el equipo local como un host y el acceso Hola CLI de Docker comandos de Docker, instalar [motor de Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="ec548-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="ec548-111">Inicie sesión en el registro de tooa</span><span class="sxs-lookup"><span data-stu-id="ec548-111">Log in tooa registry</span></span>
<span data-ttu-id="ec548-112">Ejecutar `docker login` toolog en tooyour del registro de contenedor con su [las credenciales del registro](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ec548-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="ec548-113">Hello en el ejemplo siguiente se pasa Hola ID y la contraseña de Azure Active Directory [entidad de servicio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="ec548-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="ec548-114">Por ejemplo, que puede que haya asignado un registro de tooyour principal de servicio para un escenario de automatización.</span><span class="sxs-lookup"><span data-stu-id="ec548-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="ec548-115">Asegúrese de nombre de registro completo de hello toospecify seguro (en minúsculas).</span><span class="sxs-lookup"><span data-stu-id="ec548-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="ec548-116">En este ejemplo, es `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="ec548-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="ec548-117">Pasos toopull e inserte una imagen</span><span class="sxs-lookup"><span data-stu-id="ec548-117">Steps toopull and push an image</span></span>
<span data-ttu-id="ec548-118">Hola seguir ejemplo descargas Hola Nginx imagen desde el registro de Docker Hub público hello, etiquetas para el registro de contenedor de Azure privada, lo inserta en el registro de tooyour, a continuación, se extrae de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ec548-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="ec548-119">**1. Extraiga la imagen oficial de hello Docker para Nginx**</span><span class="sxs-lookup"><span data-stu-id="ec548-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="ec548-120">Primera extracción Hola pública Nginx imagen tooyour equipo local.</span><span class="sxs-lookup"><span data-stu-id="ec548-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="ec548-121">**2. Inicie el contenedor de hello Nginx**</span><span class="sxs-lookup"><span data-stu-id="ec548-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="ec548-122">Hello comando siguiente inicia contenedor Nginx local de hello interactivamente en el puerto 8080, permitiéndole salida toosee desde Nginx.</span><span class="sxs-lookup"><span data-stu-id="ec548-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="ec548-123">Quita Hola ejecución una vez detenido el contenedor.</span><span class="sxs-lookup"><span data-stu-id="ec548-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="ec548-124">Examinar demasiado[http://localhost: 8080](http://localhost:8080) hello tooview ejecutando el contenedor.</span><span class="sxs-lookup"><span data-stu-id="ec548-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="ec548-125">Verá un toohello similar de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="ec548-125">You see a screen similar toohello following one.</span></span>

![Nginx en un equipo local](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="ec548-127">toostop Hola contenedor en ejecución, pulse [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="ec548-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="ec548-128">**3. Crear un alias de imagen de hello en el registro**</span><span class="sxs-lookup"><span data-stu-id="ec548-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="ec548-129">Hello siguiente comando crea un alias de imagen de hello, con un registro de tooyour de ruta de acceso completa.</span><span class="sxs-lookup"><span data-stu-id="ec548-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="ec548-130">Este ejemplo especifica hello `samples` desorden de tooavoid de espacio de nombres en la raíz de hello del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="ec548-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="ec548-131">**4. Registro de inserción Hola imágenes tooyour**</span><span class="sxs-lookup"><span data-stu-id="ec548-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="ec548-132">**5. Imagen de Hola de extracción desde el registro**</span><span class="sxs-lookup"><span data-stu-id="ec548-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="ec548-133">**6. Inicie el contenedor de Nginx de Hola desde el registro**</span><span class="sxs-lookup"><span data-stu-id="ec548-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="ec548-134">Examinar demasiado[http://localhost: 8080](http://localhost:8080) hello tooview ejecutando el contenedor.</span><span class="sxs-lookup"><span data-stu-id="ec548-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="ec548-135">toostop Hola contenedor en ejecución, pulse [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="ec548-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="ec548-136">**7. (Opcional) Quitar imagen Hola**</span><span class="sxs-lookup"><span data-stu-id="ec548-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="ec548-137">Límites simultáneos</span><span class="sxs-lookup"><span data-stu-id="ec548-137">Concurrent Limits</span></span>
<span data-ttu-id="ec548-138">En algunos escenarios, la ejecución de llamadas de forma simultánea podría producir errores.</span><span class="sxs-lookup"><span data-stu-id="ec548-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="ec548-139">Hello en la tabla siguiente contiene los límites de Hola de llamadas concurrentes con operaciones de "Inserción" y "Pull" en el registro de contenedor de Azure:</span><span class="sxs-lookup"><span data-stu-id="ec548-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="ec548-140">Operación</span><span class="sxs-lookup"><span data-stu-id="ec548-140">Operation</span></span>  | <span data-ttu-id="ec548-141">Límite</span><span class="sxs-lookup"><span data-stu-id="ec548-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="ec548-142">EXTRAER</span><span class="sxs-lookup"><span data-stu-id="ec548-142">PULL</span></span>       | <span data-ttu-id="ec548-143">Seguridad too10 simultáneas extrae por registro</span><span class="sxs-lookup"><span data-stu-id="ec548-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="ec548-144">INSERTAR</span><span class="sxs-lookup"><span data-stu-id="ec548-144">PUSH</span></span>       | <span data-ttu-id="ec548-145">Seguridad too5 simultáneas inserta por registro</span><span class="sxs-lookup"><span data-stu-id="ec548-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ec548-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ec548-146">Next steps</span></span>
<span data-ttu-id="ec548-147">Ahora que conoce los fundamentos de hello, ya está listo toostart mediante el registro.</span><span class="sxs-lookup"><span data-stu-id="ec548-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="ec548-148">Por ejemplo, iniciar la implementación de contenedor imágenes tooan [servicio de contenedor de Azure](https://azure.microsoft.com/documentation/services/container-service/) clúster.</span><span class="sxs-lookup"><span data-stu-id="ec548-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
