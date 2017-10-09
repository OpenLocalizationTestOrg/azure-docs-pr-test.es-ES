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
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="56d85-103">Repositorios de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="56d85-103">Azure container registry repositories</span></span>

<span data-ttu-id="56d85-104">Los registros de contenedor de Azure son compatibles con un gran número de servicios y orquestadores.</span><span class="sxs-lookup"><span data-stu-id="56d85-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="56d85-105">toomake, servicios de código fuente de hello tootrack más fáciles y los agentes desde la que se usa el ACR, hemos comenzamos utilizando el campo de encabezado de Docker de hello en el archivo de hello Docker.config.</span><span class="sxs-lookup"><span data-stu-id="56d85-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="56d85-106">Ver los repositorios en hello Portal</span><span class="sxs-lookup"><span data-stu-id="56d85-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="56d85-107">encabezados ACR Hola tener el formato de hello:</span><span class="sxs-lookup"><span data-stu-id="56d85-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="56d85-108">cloud: Azure, Azure Stack u otras nubes de Azure específicas del gobierno o el país.</span><span class="sxs-lookup"><span data-stu-id="56d85-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="56d85-109">Aunque las nubes de gobierno y Azure Stack no se admiten actualmente, este parámetro permite la compatibilidad en el futuro.</span><span class="sxs-lookup"><span data-stu-id="56d85-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="56d85-110">Servicio: el nombre del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="56d85-110">Service: name of hello service.</span></span>
* <span data-ttu-id="56d85-111">Optionalservicename: el parámetro opcional para los servicios con subservicios o toospecify una SKU (ex: aplicaciones web se corresponden con/app-servicio/aplicaciones web de Azure).</span><span class="sxs-lookup"><span data-stu-id="56d85-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="56d85-112">Orchestrators y servicios asociados son toouse recomienda toohelp de valores de encabezado específico con nuestro la telemetría.</span><span class="sxs-lookup"><span data-stu-id="56d85-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="56d85-113">Los usuarios también pueden modificar valor Hola pasada toohello encabezado si así lo desean.</span><span class="sxs-lookup"><span data-stu-id="56d85-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="56d85-114">valores de Hello queremos ACR socios toouse toopopulate Hola "X-Meta-cliente de origen" campo son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="56d85-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="56d85-115">Nombre de servicio</span><span class="sxs-lookup"><span data-stu-id="56d85-115">Service Name</span></span>              | <span data-ttu-id="56d85-116">Encabezado</span><span class="sxs-lookup"><span data-stu-id="56d85-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="56d85-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="56d85-117">Azure Container Service</span></span>   | <span data-ttu-id="56d85-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="56d85-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="56d85-119">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="56d85-119">App Service - Web Apps</span></span>    | <span data-ttu-id="56d85-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="56d85-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="56d85-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="56d85-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="56d85-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="56d85-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="56d85-123">Batch</span><span class="sxs-lookup"><span data-stu-id="56d85-123">Batch</span></span>                     | <span data-ttu-id="56d85-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="56d85-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="56d85-125">Cloud Console</span><span class="sxs-lookup"><span data-stu-id="56d85-125">Cloud Console</span></span>             | <span data-ttu-id="56d85-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="56d85-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="56d85-127">Functions</span><span class="sxs-lookup"><span data-stu-id="56d85-127">Functions</span></span>                 | <span data-ttu-id="56d85-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="56d85-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="56d85-129">Internet of Things - Hub</span><span class="sxs-lookup"><span data-stu-id="56d85-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="56d85-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="56d85-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="56d85-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="56d85-131">HDInsight</span></span>                 | <span data-ttu-id="56d85-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="56d85-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="56d85-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="56d85-133">Jenkins</span></span>                   | <span data-ttu-id="56d85-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="56d85-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="56d85-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="56d85-135">Machine Learning</span></span>          | <span data-ttu-id="56d85-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="56d85-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="56d85-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="56d85-137">Service Fabric</span></span>            | <span data-ttu-id="56d85-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="56d85-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="56d85-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="56d85-139">VSTS</span></span>                      | <span data-ttu-id="56d85-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="56d85-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="56d85-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56d85-141">Next steps</span></span>
[<span data-ttu-id="56d85-142">Obtener más información sobre los registros y Hola admite servicios y orchestrators</span><span class="sxs-lookup"><span data-stu-id="56d85-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
