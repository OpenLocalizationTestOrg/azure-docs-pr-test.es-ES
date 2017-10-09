---
title: "clúster de aaaMonitor un servicio de contenedor de Azure con Sysdig | Documentos de Microsoft"
description: "Supervise un clúster del servicio de contenedores de Azure con Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="52c8e-104">Supervisión de un clúster del servicio de contenedores de Azure con Sysdig</span><span class="sxs-lookup"><span data-stu-id="52c8e-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="52c8e-105">En este artículo, se implementará nodos de agente de Sysdig agentes tooall hello en el clúster de servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="52c8e-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="52c8e-106">Necesita una cuenta con Sysdig para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="52c8e-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="52c8e-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="52c8e-107">Prerequisites</span></span>
<span data-ttu-id="52c8e-108">[Implemente](container-service-deployment.md) y [conecte](../container-service-connect.md) un clúster configurado por Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="52c8e-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="52c8e-109">Explorar hello [interfaz de usuario de maratón](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="52c8e-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="52c8e-110">Vaya demasiado[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset una cuenta de Sysdig en la nube.</span><span class="sxs-lookup"><span data-stu-id="52c8e-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="52c8e-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="52c8e-111">Sysdig</span></span>
<span data-ttu-id="52c8e-112">Sysdig es un servicio de supervisión que le permite toomonitor los contenedores dentro de su clúster.</span><span class="sxs-lookup"><span data-stu-id="52c8e-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="52c8e-113">Sysdig se conoce toohelp a solucionar el problema, pero también tiene las métricas de supervisión básicas de CPU, red, memoria y E/S.</span><span class="sxs-lookup"><span data-stu-id="52c8e-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="52c8e-114">Resulta fácil toosee qué contenedores se comportan Sysdig hello más difíciles o básicamente mediante Hola mayoría de CPU y memoria.</span><span class="sxs-lookup"><span data-stu-id="52c8e-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="52c8e-115">Esta vista está en la sección "Introducción", que se encuentra actualmente en versión beta de Hola.</span><span class="sxs-lookup"><span data-stu-id="52c8e-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![Interfaz de usuario de Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="52c8e-117">Configuración de una implementación de Sysdig con Marathon</span><span class="sxs-lookup"><span data-stu-id="52c8e-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="52c8e-118">Estos pasos le mostrarán cómo tooconfigure e implementar aplicaciones de Sysdig tooyour clúster con maratón.</span><span class="sxs-lookup"><span data-stu-id="52c8e-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="52c8e-119">Obtener acceso a la interfaz de usuario del controlador de dominio/OS a través de [http://localhost: 80 /](http://localhost:80/) una vez en Hola DC/OS UI vaya toohello "Universo", que se encuentra en hello inferior izquierdo y, a continuación, busque "Sysdig."</span><span class="sxs-lookup"><span data-stu-id="52c8e-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![Sysdig en Universe en DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="52c8e-121">En la nube ahora configuración hello toocomplete necesita un Sysdig cuenta o una cuenta de prueba gratuita.</span><span class="sxs-lookup"><span data-stu-id="52c8e-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="52c8e-122">Una vez que ha iniciado sesión en el sitio Web de toohello Sysdig en la nube, haga clic en su nombre de usuario y, en la página de hello verá la "clave de acceso".</span><span class="sxs-lookup"><span data-stu-id="52c8e-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Clave de API de Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="52c8e-124">A continuación, escriba su clave de acceso en configuración de Sysdig de hello en hello universo de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="52c8e-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Configuración de Sysdig Hola universo de DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="52c8e-126">Ahora establezca Hola instancias too10000000 por lo que cada vez que se agrega un nuevo nodo de clúster toohello Sysdig implementará automáticamente un agente toothat nuevo nodo.</span><span class="sxs-lookup"><span data-stu-id="52c8e-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="52c8e-127">Se trata de un toomake solución provisional seguro que sysdig implementará a tooall nuevos agentes en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="52c8e-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Configuración de Sysdig Hola DC/universo de SO-instancias](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="52c8e-129">Una vez haya instalado el paquete de hello desplácese atrás toohello Sysdig UI y podrá métricas de uso diferentes de tooexplore capaz de Hola para contenedores de hello en el clúster.</span><span class="sxs-lookup"><span data-stu-id="52c8e-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="52c8e-130">También puede paneles específicos de Mesos y Marathon a través del [nuevo Asistente de panel](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="52c8e-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
