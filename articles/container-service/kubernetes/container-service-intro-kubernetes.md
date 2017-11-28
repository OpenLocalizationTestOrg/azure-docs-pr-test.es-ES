---
title: aaaIntroduction tooAzure servicio de contenedor para Kubernetes | Documentos de Microsoft
description: Servicio de contenedor de Azure para Kubernetes resulta sencillo toodeploy y administrar aplicaciones basadas en el contenedor en Azure.
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, Docker, Containers, microservicios, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="bd857-104">Introducción tooAzure servicio de contenedor para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bd857-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="bd857-105">Servicio de contenedor de Azure para Kubernetes resulta sencillo toocreate, configurar y administrar un clúster de máquinas virtuales que forman las aplicaciones preconfiguradas toorun en contenedores.</span><span class="sxs-lookup"><span data-stu-id="bd857-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="bd857-106">Esto permite toouse sus conocimientos, o dibujar en un cuerpo elevado y creciente de conocimientos de la Comunidad, toodeploy y administrar aplicaciones basadas en el contenedor en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bd857-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="bd857-107">Mediante el servicio de contenedor de Azure, puede aprovechar las ventajas del programa Hola a características de nivel empresarial de Azure, manteniendo la portabilidad de aplicación a través de Kubernetes y Hola formato de imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="bd857-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="bd857-108">Uso de Azure Container Service para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bd857-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="bd857-109">Nuestro objetivo con el servicio de contenedor de Azure es tooprovide un entorno de hospedaje de contenedor mediante el uso de herramientas de código abierto y tecnologías que son populares entre los clientes hoy en día.</span><span class="sxs-lookup"><span data-stu-id="bd857-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="bd857-110">toothis final, se exponen los puntos de conexión de la API de Kubernetes estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="bd857-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="bd857-111">Mediante el uso de estos puntos de conexión estándar, puede aprovechar cualquier software que es capaz de comunicarse tooa Kubernetes clúster.</span><span class="sxs-lookup"><span data-stu-id="bd857-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="bd857-112">Por ejemplo, puede elegir [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) o [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="bd857-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="bd857-113">Creación de un clúster de Docker mediante Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="bd857-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="bd857-114">toobegin con el servicio de contenedor de Azure, implementar un clúster de servicio de contenedor de Azure con hello [CLI de Azure 2.0](container-service-kubernetes-walkthrough.md) o a través del portal de hello (Hola búsqueda Marketplace para **servicio de contenedor de Azure**).</span><span class="sxs-lookup"><span data-stu-id="bd857-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="bd857-115">Si es un usuario avanzado que necesita más control sobre las plantillas de Azure Resource Manager de hello, puede usar código abierto de hello [motor acs](https://github.com/Azure/acs-engine) proyecto toobuild sus propio Kubernetes personalizados de clúster e implementarla a través de Hola `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="bd857-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="bd857-116">Uso de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bd857-116">Using Kubernetes</span></span>
<span data-ttu-id="bd857-117">Kubernetes automatiza la implementación, el escalado y la administración de aplicaciones en contenedor.</span><span class="sxs-lookup"><span data-stu-id="bd857-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="bd857-118">Tiene un amplio conjunto de características que incluyen:</span><span class="sxs-lookup"><span data-stu-id="bd857-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="bd857-119">Empaquetamiento automático en contenedores</span><span class="sxs-lookup"><span data-stu-id="bd857-119">Automatic binpacking</span></span>
* <span data-ttu-id="bd857-120">Recuperación automática</span><span class="sxs-lookup"><span data-stu-id="bd857-120">Self-healing</span></span>
* <span data-ttu-id="bd857-121">Escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="bd857-121">Horizontal scaling</span></span>
* <span data-ttu-id="bd857-122">Detección de servicio y equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="bd857-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="bd857-123">Lanzamientos y reversiones automatizados</span><span class="sxs-lookup"><span data-stu-id="bd857-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="bd857-124">Administración de configuración y secretos</span><span class="sxs-lookup"><span data-stu-id="bd857-124">Secret and configuration management</span></span>
* <span data-ttu-id="bd857-125">Orquestación de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bd857-125">Storage orchestration</span></span>
* <span data-ttu-id="bd857-126">Ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="bd857-126">Batch execution</span></span>

<span data-ttu-id="bd857-127">Diagrama de la arquitectura de Kubernetes implementado a través de Azure Container Service:</span><span class="sxs-lookup"><span data-stu-id="bd857-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Servicio de contenedor de Azure había configurado toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="bd857-129">Vídeos</span><span class="sxs-lookup"><span data-stu-id="bd857-129">Videos</span></span>

<span data-ttu-id="bd857-130">Compatibilidad con Kubernetes de Azure Container Services (Azure, viernes, enero de 2017):</span><span class="sxs-lookup"><span data-stu-id="bd857-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="bd857-131">Herramientas para desarrollar e implementar aplicaciones en Kubernetes (Azure OpenDev, junio de 2017):</span><span class="sxs-lookup"><span data-stu-id="bd857-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="bd857-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd857-132">Next steps</span></span>

<span data-ttu-id="bd857-133">Explorar hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin explorar el servicio de contenedor de Azure hoy en día.</span><span class="sxs-lookup"><span data-stu-id="bd857-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
