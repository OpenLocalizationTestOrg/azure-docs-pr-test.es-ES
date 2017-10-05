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
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="1b27d-103">Repositorios de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="1b27d-103">Azure container registry repositories</span></span>

<span data-ttu-id="1b27d-104">Los registros de contenedor de Azure son compatibles con un gran número de servicios y orquestadores.</span><span class="sxs-lookup"><span data-stu-id="1b27d-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="1b27d-105">Para que sea más fácil realizar el seguimiento de los servicios y los agentes de origen desde los que se usa ACR, hemos empezado con el campo de encabezado de Docker del archivo Docker.config.</span><span class="sxs-lookup"><span data-stu-id="1b27d-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="1b27d-106">Visualización de repositorios en el portal</span><span class="sxs-lookup"><span data-stu-id="1b27d-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="1b27d-107">Los encabezados de ACR tienen el formato:</span><span class="sxs-lookup"><span data-stu-id="1b27d-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="1b27d-108">cloud: Azure, Azure Stack u otras nubes de Azure específicas del gobierno o el país.</span><span class="sxs-lookup"><span data-stu-id="1b27d-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="1b27d-109">Aunque las nubes de gobierno y Azure Stack no se admiten actualmente, este parámetro permite la compatibilidad en el futuro.</span><span class="sxs-lookup"><span data-stu-id="1b27d-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="1b27d-110">service: nombre del servicio.</span><span class="sxs-lookup"><span data-stu-id="1b27d-110">Service: name of the service.</span></span>
* <span data-ttu-id="1b27d-111">optionalservicename: parámetro opcional para los servicios con subservicios o para especificar una SKU (por ejemplo, las aplicaciones web se corresponden con Azure/app-service/web-apps).</span><span class="sxs-lookup"><span data-stu-id="1b27d-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="1b27d-112">Se recomienda que los orquestadores y los servicios asociados usen valores de encabezado específicos para ayudar a con la telemetría.</span><span class="sxs-lookup"><span data-stu-id="1b27d-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="1b27d-113">Si quieren, los usuarios también pueden modificar el valor pasado al encabezado.</span><span class="sxs-lookup"><span data-stu-id="1b27d-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="1b27d-114">A continuación se encuentran los valores que queremos que usen los asociados de ACR para rellenar el campo "X-Meta-Source-Client":</span><span class="sxs-lookup"><span data-stu-id="1b27d-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="1b27d-115">Nombre de servicio</span><span class="sxs-lookup"><span data-stu-id="1b27d-115">Service Name</span></span>              | <span data-ttu-id="1b27d-116">Encabezado</span><span class="sxs-lookup"><span data-stu-id="1b27d-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="1b27d-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="1b27d-117">Azure Container Service</span></span>   | <span data-ttu-id="1b27d-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="1b27d-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="1b27d-119">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="1b27d-119">App Service - Web Apps</span></span>    | <span data-ttu-id="1b27d-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="1b27d-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="1b27d-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1b27d-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="1b27d-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="1b27d-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="1b27d-123">Batch</span><span class="sxs-lookup"><span data-stu-id="1b27d-123">Batch</span></span>                     | <span data-ttu-id="1b27d-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="1b27d-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="1b27d-125">Cloud Console</span><span class="sxs-lookup"><span data-stu-id="1b27d-125">Cloud Console</span></span>             | <span data-ttu-id="1b27d-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="1b27d-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="1b27d-127">Functions</span><span class="sxs-lookup"><span data-stu-id="1b27d-127">Functions</span></span>                 | <span data-ttu-id="1b27d-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="1b27d-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="1b27d-129">Internet of Things - Hub</span><span class="sxs-lookup"><span data-stu-id="1b27d-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="1b27d-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="1b27d-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="1b27d-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b27d-131">HDInsight</span></span>                 | <span data-ttu-id="1b27d-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="1b27d-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="1b27d-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="1b27d-133">Jenkins</span></span>                   | <span data-ttu-id="1b27d-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="1b27d-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="1b27d-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1b27d-135">Machine Learning</span></span>          | <span data-ttu-id="1b27d-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="1b27d-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="1b27d-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1b27d-137">Service Fabric</span></span>            | <span data-ttu-id="1b27d-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="1b27d-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="1b27d-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="1b27d-139">VSTS</span></span>                      | <span data-ttu-id="1b27d-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="1b27d-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="1b27d-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b27d-141">Next steps</span></span>
[<span data-ttu-id="1b27d-142">Más información sobre los registros, y los servicios y orquestadores compatibles</span><span class="sxs-lookup"><span data-stu-id="1b27d-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
