---
title: "clúster de Azure DC/OS aaaMonitor - Dynatrace | Documentos de Microsoft"
description: "Supervisión de un clúster de Azure Container Service DC/OS con Dynatrace. Implementar hello Dynatrace OneAgent mediante el panel de Hola DC/OS."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Contenedores, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="03e4c-105">Supervisión de un clúster DC/OS de Azure Container Service con Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="03e4c-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="03e4c-106">En este artículo, le mostraremos cómo hello toodeploy [Dynatrace](https://www.dynatrace.com/) Hola a OneAgent toomonitor todos los nodos de agente en el clúster de servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="03e4c-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="03e4c-107">Necesita una cuenta con Dynatrace SaaS/Managed para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="03e4c-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="03e4c-108">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="03e4c-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="03e4c-109">Dynatrace es una solución de supervisión nativa en la nube para entornos de clúster y contenedor muy dinámicos.</span><span class="sxs-lookup"><span data-stu-id="03e4c-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="03e4c-110">Le permite toobetter optimizar las implementaciones de contenedor y las asignaciones de memoria mediante datos de uso en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="03e4c-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="03e4c-111">Permite indicar automáticamente los problemas de infraestructura y aplicación proporcionando una línea de base automatizada, la correlación de problemas y la detección de la causa raíz.</span><span class="sxs-lookup"><span data-stu-id="03e4c-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="03e4c-112">Hola siguiente figura se muestra hello Dynatrace UI:</span><span class="sxs-lookup"><span data-stu-id="03e4c-112">hello following figure shows hello Dynatrace UI:</span></span>

![Interfaz de usuario de Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="03e4c-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="03e4c-114">Prerequisites</span></span> 
<span data-ttu-id="03e4c-115">[Implementar](container-service-deployment.md) y [conectar](./../container-service-connect.md) clúster tooa configurado mediante el servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="03e4c-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="03e4c-116">Explorar hello [interfaz de usuario de maratón](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="03e4c-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="03e4c-117">Vaya demasiado[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset una cuenta de Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="03e4c-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="03e4c-118">Configuración de una implementación de Dynatrace con Marathon</span><span class="sxs-lookup"><span data-stu-id="03e4c-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="03e4c-119">Estos pasos le mostrarán cómo tooconfigure e implementar aplicaciones de Dynatrace tooyour clúster con maratón.</span><span class="sxs-lookup"><span data-stu-id="03e4c-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="03e4c-120">Acceda a la interfaz de usuario de DC/OS mediante [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="03e4c-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="03e4c-121">Una vez en hello interfaz de usuario del controlador de dominio/OS, navegue toohello **universo** ficha y, a continuación, busque **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="03e4c-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace en Universe (Universo) en DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="03e4c-123">configuración de hello toocomplete, necesita una cuenta de Dynatrace SaaS o una cuenta de prueba gratuita.</span><span class="sxs-lookup"><span data-stu-id="03e4c-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="03e4c-124">Una vez que ha iniciado sesión en el panel de Dynatrace hello, seleccione **Dynatrace implementar**.</span><span class="sxs-lookup"><span data-stu-id="03e4c-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Integración de PaaS de configuración de Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="03e4c-126">En la página de hello, seleccione **configurar la integración de PaaS**.</span><span class="sxs-lookup"><span data-stu-id="03e4c-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Token de la API de Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="03e4c-128">Escriba el símbolo (token) de API en hello Dynatrace OneAgent configuración dentro de Hola DC/OS universo.</span><span class="sxs-lookup"><span data-stu-id="03e4c-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![Configuración de Dynatrace OneAgent Hola universo de DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="03e4c-130">Establecer instancias de hello toohello número de nodos piensa toorun.</span><span class="sxs-lookup"><span data-stu-id="03e4c-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="03e4c-131">Establece a un número mayor también funciona, pero el controlador de dominio/OS seguirá intentando toofind nuevas instancias hasta que realmente se alcanza ese número.</span><span class="sxs-lookup"><span data-stu-id="03e4c-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="03e4c-132">Si lo prefiere, también puede establecer este valor tooa como 1000000.</span><span class="sxs-lookup"><span data-stu-id="03e4c-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="03e4c-133">En este caso, cada vez que se agrega un nuevo nodo clúster toohello, Dynatrace implementa automáticamente un agente toothat nuevo nodo, a un precio de Hola de DC/OS probar constantemente instancias adicionales de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="03e4c-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Configuración de Dynatrace Hola DC/universo de SO-instancias](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="03e4c-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03e4c-135">Next steps</span></span>

<span data-ttu-id="03e4c-136">Una vez haya instalado el paquete de hello, desplácese atrás toohello Dynatrace panel.</span><span class="sxs-lookup"><span data-stu-id="03e4c-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="03e4c-137">Puede explorar las métricas de uso distintos de Hola para contenedores de hello en el clúster.</span><span class="sxs-lookup"><span data-stu-id="03e4c-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
