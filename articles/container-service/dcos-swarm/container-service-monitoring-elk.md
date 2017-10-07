---
title: "un clúster de Azure DC/OS - pila ELK aaaMonitor | Documentos de Microsoft"
description: "Supervisión de un clúster de DC/OS en un clúster de Azure Container Service con ELK (Elasticsearch, Logstash y Kibana)."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Contenedores, DC/OS, supervisión, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="0d9c5-104">Supervisión de un clúster de Azure Container Service con ELK</span><span class="sxs-lookup"><span data-stu-id="0d9c5-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="0d9c5-105">En este artículo, se muestra cómo la pila toodeploy Hola ELK (Elasticsearch, Logstash, Kibana) en un clúster de DC/OS en el servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0d9c5-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0d9c5-106">Prerequisites</span></span>
<span data-ttu-id="0d9c5-107">[Implemente](container-service-deployment.md) y [conecte](../container-service-connect.md) un clúster de DC/OS configurado por Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="0d9c5-108">Explorar el panel de controlador de dominio/OS hello y servicios de maratón [aquí](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="0d9c5-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="0d9c5-109">Instalar hello [equilibrador de carga de maratón](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="0d9c5-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="0d9c5-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="0d9c5-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="0d9c5-111">Pila ELK es una combinación de Elasticsearch, Logstash, y Kibana que proporciona una pila de tooend final que puede toomonitor usado y analizar los registros en el clúster.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="0d9c5-112">Configurar la pila ELK hello en un clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="0d9c5-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="0d9c5-113">Obtener acceso a la interfaz de usuario del controlador de dominio/OS a través de [http://localhost: 80 /](http://localhost:80/) una vez en hello navegar de interfaz de usuario del controlador de dominio/OS demasiado**universo**.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="0d9c5-114">Buscar e instalar Elasticsearch, Logstash y Kibana con hello universo de DC/OS y, en ese orden específico.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="0d9c5-115">Se puede obtener más información acerca de la configuración si va toohello **instalación avanzada** vínculo.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="0d9c5-119">Una vez Hola contenedores ELK y están activos y en funcionamiento, debe tooenable Kibana toobe tiene acceso a través de maratón LB.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="0d9c5-120">Navegue demasiado **servicios** > **kibana**y haga clic en **editar** tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="0d9c5-122">Alternar demasiado**modo JSON** y desplácese hacia abajo de la sección de etiquetas toohello.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="0d9c5-123">Necesita tooadd un `"HAPROXY_GROUP": "external"` entrada aquí tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="0d9c5-124">Una vez que haga clic en **Deploy changes** (Implementar cambios), se reinicia el contenedor.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="0d9c5-126">Si desea que tooverify que Kibana está registrado como un servicio en el panel HAPROXY hello, deberá tooopen puerto 9090 en clúster de agente de hello tal y como HAPROXY se ejecuta en el puerto 9090.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="0d9c5-127">De forma predeterminada, se abre los puertos 80, 8080 y Hola a 443 en el clúster de agente de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="0d9c5-128">Instrucciones tooopen un puerto y proporcionar evaluar público se proporcionan [aquí](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="0d9c5-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="0d9c5-129">tooaccess Hola panel HAPROXY, interfaz de administración abierto Hola maratón LB en: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="0d9c5-130">Una vez que navegue toohello URL, debería ver el panel de hello HAPROXY tal y como se muestra a continuación y debería ver una entrada de servicio de Kibana.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="0d9c5-132">panel de tooaccess hello Kibana, que se implementa en el puerto 5601, deberá tooopen puerto 5601.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="0d9c5-133">Siga las instrucciones que encontrará [aquí](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="0d9c5-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="0d9c5-134">A continuación, abra el panel de Kibana hello en: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="0d9c5-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d9c5-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0d9c5-135">Next steps</span></span>

* <span data-ttu-id="0d9c5-136">Con respecto al reenvío y configuración de registros de aplicaciones y sistemas, consulte [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Administración de registros en DC/OS con ELK).</span><span class="sxs-lookup"><span data-stu-id="0d9c5-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="0d9c5-137">Consulte los registros de toofilter, [filtrar registros con ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="0d9c5-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

