---
title: repositorios de registro del contenedor de aaaAzure | Documentos de Microsoft
description: "¿Cómo toouse repositorios de registro de contenedor de Azure para las imágenes de Docker"
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
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="8d1fd-103">Repositorios de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="8d1fd-103">Azure container registry repositories</span></span>

<span data-ttu-id="8d1fd-104">Registro de contenedor de Azure permite imágenes del contenedor toostore en repositorios.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="8d1fd-105">Mediante el almacenamiento de imágenes en repositorios, puede tener grupos de imágenes (o versión de imágenes) en entornos aislados.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="8d1fd-106">Puede especificar estos repositorios cuando realice una inserción del registro de tooyour de imágenes.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8d1fd-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8d1fd-107">Prerequisites</span></span>
* <span data-ttu-id="8d1fd-108">**Registro de contenedor de Azure**: cree un registro de contenedor en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="8d1fd-109">Por ejemplo, usar hello [portal de Azure](container-registry-get-started-portal.md) o hello [CLI de Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8d1fd-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="8d1fd-110">**CLI de docker** -tooset el equipo local como un host y el acceso Hola CLI de Docker comandos de Docker, instalar [motor de Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="8d1fd-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="8d1fd-111">**Una imagen de extracción** : extraer una imagen de registro de Docker Hub público hello, etiquetarlo y empújelo tooyour registro.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="8d1fd-112">Para obtener instrucciones sobre cómo insertar y extraer imágenes, vea [registro privada de inserción Docker imágenes tooAzure](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8d1fd-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="8d1fd-113">Ver los repositorios en hello Portal</span><span class="sxs-lookup"><span data-stu-id="8d1fd-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="8d1fd-114">Una vez que haya insertado el registro de contenedor de tooyour de imágenes, puede ver una lista de repositorios de hello hospedaje imágenes Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="8d1fd-115">Si ha seguido los pasos de Hola Hola [registro privada de Docker Push imágenes tooAzure](container-registry-get-started-docker-cli.md) artículo, ahora debería tener una imagen de Nginx en el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="8d1fd-116">Como parte de las instrucciones de hello, debe especificar un espacio de nombres de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="8d1fd-117">En el ejemplo de Hola siguiente, el comando de hello inserta repositorio de hello NGinx imágenes toohello "ejemplos":</span><span class="sxs-lookup"><span data-stu-id="8d1fd-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="8d1fd-118">Azure Container Registry es compatible con los espacios de nombres del repositorio de varios niveles.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="8d1fd-119">Esta característica permite toogroup las colecciones de aplicación específico de imágenes tooa relacionados o una colección de desarrollo de aplicaciones toospecific o los equipos operativos.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="8d1fd-120">tooread más información acerca de los repositorios de registros de contenedor, consulte [registros de contenedor de privado Docker en Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8d1fd-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="8d1fd-121">repositorios de tooview Hola contenedor del registro:</span><span class="sxs-lookup"><span data-stu-id="8d1fd-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="8d1fd-122">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8d1fd-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="8d1fd-123">En hello **registro de contenedor de Azure** hoja, registro de hello seleccione desea tooinspect</span><span class="sxs-lookup"><span data-stu-id="8d1fd-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="8d1fd-124">En la hoja de registro de hello, haga clic en **repositorios** toosee una lista de todos los repositorios de Hola y sus imágenes</span><span class="sxs-lookup"><span data-stu-id="8d1fd-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="8d1fd-125">(Opcional) Seleccione las etiquetas de una imagen específica toosee</span><span class="sxs-lookup"><span data-stu-id="8d1fd-125">(Optional) Select a specific image toosee tags</span></span>

![Repositorios de portal de Hola](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="8d1fd-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8d1fd-127">Next steps</span></span>
<span data-ttu-id="8d1fd-128">Ahora que conoce los fundamentos de hello, ya está listo toostart mediante el registro.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="8d1fd-129">Por ejemplo, iniciar la implementación de contenedor imágenes tooan [servicio de contenedor de Azure](https://azure.microsoft.com/documentation/services/container-service/) clúster.</span><span class="sxs-lookup"><span data-stu-id="8d1fd-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
