---
title: "Equilibrio de carga de contenedores en un clúster DC/OS de Azure | Microsoft Docs"
description: "Equilibrio de carga en varios contenedores en un clúster DC/OS de Azure Container Service."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, microservicios, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 78725c9d23e13d307821a188028ef573d1def038
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="97ce3-104">Equilibrio de carga de contenedores en un clúster DC/OS de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="97ce3-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="97ce3-105">En este artículo, exploramos cómo crear un equilibrador de carga interno en una instancia de Azure Container Service administrada por DC/OS mediante Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="97ce3-105">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="97ce3-106">Esta configuración le permite escalar aplicaciones horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="97ce3-106">This configuration enables you to scale your applications horizontally.</span></span> <span data-ttu-id="97ce3-107">También le permite aprovechar sacar provecho de los clústeres de agente públicos y privados mediante la colocación de los equilibradores de carga en el clúster público y los contenedores de su aplicación en el clúster privado.</span><span class="sxs-lookup"><span data-stu-id="97ce3-107">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span> <span data-ttu-id="97ce3-108">En este tutorial, hizo lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="97ce3-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="97ce3-109">Configurar un equilibrador de carga de Marathon</span><span class="sxs-lookup"><span data-stu-id="97ce3-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="97ce3-110">Implementación de una aplicación con el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="97ce3-110">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="97ce3-111">Configurar Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="97ce3-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="97ce3-112">Necesita un clúster de ACS con DC/OS para completar los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="97ce3-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="97ce3-113">Si es necesario, este [script de ejemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) puede crear uno.</span><span class="sxs-lookup"><span data-stu-id="97ce3-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="97ce3-114">Para realizar este tutorial es necesaria la versión 2.0.4 o superior de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="97ce3-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="97ce3-115">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="97ce3-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="97ce3-116">Si necesita actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="97ce3-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="97ce3-117">Introducción al equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="97ce3-117">Load balancing overview</span></span>

<span data-ttu-id="97ce3-118">Hay dos capas de equilibrio de carga en un clúster DC/OS de Azure Container Service :</span><span class="sxs-lookup"><span data-stu-id="97ce3-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="97ce3-119">**Azure Load Balancer** proporciona puntos de entrada públicos (los que llegarán a los usuarios finales).</span><span class="sxs-lookup"><span data-stu-id="97ce3-119">**Azure Load Balancer** provides public entry points (the ones that end users access).</span></span> <span data-ttu-id="97ce3-120">Azure Load Balancer lo proporciona automáticamente Azure Container Service y, de forma predeterminada, se configura para exponer los puertos 80, 443 y 8080.</span><span class="sxs-lookup"><span data-stu-id="97ce3-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>

<span data-ttu-id="97ce3-121">**Marathon Load Balancer (marathon-lb)** enruta las solicitudes entrantes a instancias de contenedor que sirven a esas solicitudes.</span><span class="sxs-lookup"><span data-stu-id="97ce3-121">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span></span> <span data-ttu-id="97ce3-122">Marathon-lb se adapta dinámicamente a medida que escalamos los contenedores que proporcionan el servicio web.</span><span class="sxs-lookup"><span data-stu-id="97ce3-122">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span></span> <span data-ttu-id="97ce3-123">De manera predeterminada no se proporciona este equilibrador de carga en Azure Container Service, pero se instala fácilmente.</span><span class="sxs-lookup"><span data-stu-id="97ce3-123">This load balancer is not provided by default in your Container Service, but it is easy to install.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="97ce3-124">Configuración de un equilibrador de carga de Marathon</span><span class="sxs-lookup"><span data-stu-id="97ce3-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="97ce3-125">El equilibrador de carga de Marathon se reconfigura dinámicamente basándose en los contenedores que ha implementado.</span><span class="sxs-lookup"><span data-stu-id="97ce3-125">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="97ce3-126">También es resistente a la pérdida de contenedores o agentes; en caso de que ocurra, Apache Mesos reinicia el contenedor en otro lugar y marathon-lb se adapta.</span><span class="sxs-lookup"><span data-stu-id="97ce3-126">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="97ce3-127">Ejecute el siguiente comando para instalar el equilibrador de carga de Marathon en el clúster del agente público.</span><span class="sxs-lookup"><span data-stu-id="97ce3-127">Run the following command to install the marathon load balancer on the public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="97ce3-128">Implementación de una aplicación de carga equilibrada</span><span class="sxs-lookup"><span data-stu-id="97ce3-128">Deploy load balanced application</span></span>

<span data-ttu-id="97ce3-129">Ahora que tenemos el paquete de marathon-lb, podemos implementar el contenedor de aplicaciones cuya carga se desea equilibrar.</span><span class="sxs-lookup"><span data-stu-id="97ce3-129">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> 

<span data-ttu-id="97ce3-130">En primer lugar, obtenga el FQDN de los agentes expuestos públicamente.</span><span class="sxs-lookup"><span data-stu-id="97ce3-130">First, get the FQDN of the publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="97ce3-131">A continuación, cree un archivo denominado *hello-web.json* y cópielo en el contenido siguiente.</span><span class="sxs-lookup"><span data-stu-id="97ce3-131">Next, create a file named *hello-web.json* and copy in the following contents.</span></span> <span data-ttu-id="97ce3-132">La etiqueta `HAPROXY_0_VHOST` debe actualizarse con el FQDN de los agentes de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="97ce3-132">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="97ce3-133">Utilice la CLI de DC/OS para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="97ce3-133">Use the DC/OS CLI to run the application.</span></span> <span data-ttu-id="97ce3-134">De forma predeterminada, Marathon implementa la aplicación en el clúster privado.</span><span class="sxs-lookup"><span data-stu-id="97ce3-134">By default Marathon deploys the the applicaton to the private cluster.</span></span> <span data-ttu-id="97ce3-135">Esto significa que la implementación anterior solo es accesible a través del equilibrador de carga, lo que suele ser el comportamiento deseado.</span><span class="sxs-lookup"><span data-stu-id="97ce3-135">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="97ce3-136">Una vez que se ha implementado la aplicación, busque el FQDN del clúster de agente para ver la aplicación de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="97ce3-136">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span></span>

![Imagen de la aplicación de carga equilibrada](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="97ce3-138">Configuración de Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="97ce3-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="97ce3-139">De forma predeterminada, Azure Load Balancer expone los puertos 80, 8080 y 443.</span><span class="sxs-lookup"><span data-stu-id="97ce3-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="97ce3-140">Si está utilizando uno de estos tres puertos (como ocurre en el ejemplo anterior), no hay nada que debe hacer.</span><span class="sxs-lookup"><span data-stu-id="97ce3-140">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="97ce3-141">Debe ser capaz de alcanzar el agente del nombre de dominio completo del equilibrador de carga; cada vez que actualice, alcanzará uno de los tres servidores web con el mecanismo round robin.</span><span class="sxs-lookup"><span data-stu-id="97ce3-141">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="97ce3-142">Si utiliza otro puerto, deberá agregar una regla de operación round robin y realizar un sondeo en el equilibrador de carga para ver cuál es el puerto utilizado.</span><span class="sxs-lookup"><span data-stu-id="97ce3-142">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="97ce3-143">Este procedimiento se puede realizar desde la [CLI de Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), con los comandos `azure network lb rule create` y `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="97ce3-143">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97ce3-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97ce3-144">Next steps</span></span>

<span data-ttu-id="97ce3-145">En este tutorial, ha aprendido acerca de equilibrio de carga en ACS con los equilibradores de carga de Azure y Marathon, incluidas las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="97ce3-145">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="97ce3-146">Configurar un equilibrador de carga de Marathon</span><span class="sxs-lookup"><span data-stu-id="97ce3-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="97ce3-147">Implementación de una aplicación con el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="97ce3-147">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="97ce3-148">Configurar Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="97ce3-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="97ce3-149">Avance al tutorial siguiente para obtener información sobre la integración de Azure Storage con DC/OS en Azure.</span><span class="sxs-lookup"><span data-stu-id="97ce3-149">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97ce3-150">Montaje del recurso compartido de archivos de Azure en un clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="97ce3-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)