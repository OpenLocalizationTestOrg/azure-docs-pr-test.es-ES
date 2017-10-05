---
title: Repositorios de Azure Container Registry | Microsoft Docs
description: "Uso de los repositorios de Azure Container Registry para imágenes de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="89ccc-103">Repositorios de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="89ccc-103">Azure container registry repositories</span></span>

<span data-ttu-id="89ccc-104">Azure Container Registry permite almacenar imágenes de contenedor en repositorios.</span><span class="sxs-lookup"><span data-stu-id="89ccc-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="89ccc-105">Mediante el almacenamiento de imágenes en repositorios, puede tener grupos de imágenes (o versión de imágenes) en entornos aislados.</span><span class="sxs-lookup"><span data-stu-id="89ccc-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="89ccc-106">Puede especificar estos repositorios al insertar imágenes en el registro.</span><span class="sxs-lookup"><span data-stu-id="89ccc-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="89ccc-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="89ccc-107">Prerequisites</span></span>
* <span data-ttu-id="89ccc-108">**Registro de contenedor de Azure**: cree un registro de contenedor en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="89ccc-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="89ccc-109">Por ejemplo, use [Azure Portal](container-registry-get-started-portal.md) o la [CLI de Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="89ccc-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="89ccc-110">**CLI de docker**: para configurar el equipo local como un host de Docker y tener acceso a los comandos de la CLI de Docker, instale [Docker Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="89ccc-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="89ccc-111">**Extraer una imagen**: extraiga una imagen desde el registro público de Docker Hub, etiquétela e insértela en el registro.</span><span class="sxs-lookup"><span data-stu-id="89ccc-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="89ccc-112">Para obtener instrucciones sobre cómo insertar y extraer imágenes, vea [Inserción de la primera imagen en un registro de contenedor privado de Docker mediante la CLI de Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="89ccc-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="89ccc-113">Visualización de repositorios en el portal</span><span class="sxs-lookup"><span data-stu-id="89ccc-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="89ccc-114">Una vez que haya insertado imágenes en el registro de contenedor, puede ver una lista de los repositorios que hospedan imágenes en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="89ccc-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="89ccc-115">Si ha seguido los pasos descritos en [Inserción de la primera imagen en un registro de contenedor privado de Docker mediante la CLI de Docker](container-registry-get-started-docker-cli.md), ahora debería tener una imagen de Nginx en el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="89ccc-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="89ccc-116">Como parte de las instrucciones, debe haber especificado un espacio de nombres para la imagen.</span><span class="sxs-lookup"><span data-stu-id="89ccc-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="89ccc-117">En el ejemplo siguiente, el comando inserta la imagen de NGinx en el repositorio de "ejemplos":</span><span class="sxs-lookup"><span data-stu-id="89ccc-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="89ccc-118">Azure Container Registry es compatible con los espacios de nombres del repositorio de varios niveles.</span><span class="sxs-lookup"><span data-stu-id="89ccc-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="89ccc-119">Esta característica le permite agrupar colecciones de imágenes relacionadas con una aplicación específica o una colección de aplicaciones con equipos operativos o de desarrollo específicos.</span><span class="sxs-lookup"><span data-stu-id="89ccc-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="89ccc-120">Para más información sobre los repositorios de registros de contenedor, consulte [Introducción a los registros de contenedores privados de Docker](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="89ccc-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="89ccc-121">Para ver los repositorios de registro de contenedor:</span><span class="sxs-lookup"><span data-stu-id="89ccc-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="89ccc-122">Iniciar sesión en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="89ccc-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="89ccc-123">En la hoja **Azure Container Registry**, seleccione el registro que desea inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="89ccc-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="89ccc-124">En la hoja de registro, haga clic en **Repositorios** para ver una lista de todos los repositorios y sus imágenes.</span><span class="sxs-lookup"><span data-stu-id="89ccc-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="89ccc-125">(Opcional) Seleccione una imagen específica para ver etiquetas.</span><span class="sxs-lookup"><span data-stu-id="89ccc-125">(Optional) Select a specific image to see tags</span></span>

![Repositorios del portal](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="89ccc-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89ccc-127">Next steps</span></span>
<span data-ttu-id="89ccc-128">Ahora que conoce los fundamentos, ya está listo para empezar a usar el registro.</span><span class="sxs-lookup"><span data-stu-id="89ccc-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="89ccc-129">Por ejemplo, empiece por implementar imágenes del contenedor en un clúster de [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="89ccc-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
