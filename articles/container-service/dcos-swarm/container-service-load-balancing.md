---
title: "contenedores de saldo de aaaLoad en clúster de Azure DC/OS | Documentos de Microsoft"
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
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="45e60-104">Equilibrio de carga de contenedores en un clúster DC/OS de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="45e60-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="45e60-105">En este artículo, exploraremos cómo toocreate un equilibrador de carga interno en un controlador de dominio/OS administra el servicio de contenedor de Azure mediante maratón LB.</span><span class="sxs-lookup"><span data-stu-id="45e60-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="45e60-106">Esta configuración permite que se tooscale sus aplicaciones horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="45e60-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="45e60-107">También permite tootake ventaja de clústeres de hello agente públicas y privadas mediante la colocación de los equilibradores de carga en los clústeres pública de Hola y los contenedores de la aplicación en clúster privada Hola.</span><span class="sxs-lookup"><span data-stu-id="45e60-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="45e60-108">En este tutorial, hizo lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="45e60-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45e60-109">Configurar un equilibrador de carga de Marathon</span><span class="sxs-lookup"><span data-stu-id="45e60-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="45e60-110">Implementar una aplicación con el equilibrador de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="45e60-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="45e60-111">Configurar Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="45e60-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="45e60-112">Necesita un controlador de dominio ACS/OS hello toocomplete de clúster de los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="45e60-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="45e60-113">Si es necesario, este [script de ejemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) puede crear uno.</span><span class="sxs-lookup"><span data-stu-id="45e60-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="45e60-114">Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="45e60-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="45e60-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="45e60-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="45e60-116">Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="45e60-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="45e60-117">Introducción al equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="45e60-117">Load balancing overview</span></span>

<span data-ttu-id="45e60-118">Hay dos capas de equilibrio de carga en un clúster DC/OS de Azure Container Service :</span><span class="sxs-lookup"><span data-stu-id="45e60-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="45e60-119">**El equilibrador de carga Azure** proporciona puntos de entrada públicos (Hola acceder los que los usuarios finales).</span><span class="sxs-lookup"><span data-stu-id="45e60-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="45e60-120">Una carga Equilibrada de Azure se proporciona automáticamente mediante el servicio de contenedor de Azure y es, de forma predeterminada, tooexpose configurado puerto 8080, 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="45e60-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="45e60-121">**Hola equilibrador de carga de maratón (maratón lb)** instancias de toocontainer de solicitudes que dan servicio a estas solicitudes de entrada de las rutas.</span><span class="sxs-lookup"><span data-stu-id="45e60-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="45e60-122">A medida que se escalan contenedores Hola proporcionar nuestro servicio web, se adapta dinámicamente Hola maratón-lb.</span><span class="sxs-lookup"><span data-stu-id="45e60-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="45e60-123">Este equilibrador de carga no se proporciona de forma predeterminada en el servicio de contenedor, pero resulta fácil tooinstall.</span><span class="sxs-lookup"><span data-stu-id="45e60-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="45e60-124">Configuración de un equilibrador de carga de Marathon</span><span class="sxs-lookup"><span data-stu-id="45e60-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="45e60-125">Equilibrador de carga de maratón reconfigura dinámicamente basándose en los contenedores de Hola que se han implementado.</span><span class="sxs-lookup"><span data-stu-id="45e60-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="45e60-126">También es resistente toohello pérdida de un contenedor o un agente - si esto ocurre, Apache Mesos reinicia el contenedor de hello en otra parte y se adapta maratón lb.</span><span class="sxs-lookup"><span data-stu-id="45e60-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="45e60-127">Ejecute hello después de equilibrador de carga de comando tooinstall Hola maratón en clúster del agente de hello pública.</span><span class="sxs-lookup"><span data-stu-id="45e60-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="45e60-128">Implementación de una aplicación de carga equilibrada</span><span class="sxs-lookup"><span data-stu-id="45e60-128">Deploy load balanced application</span></span>

<span data-ttu-id="45e60-129">Ahora que tenemos el paquete de maratón lb hello, podemos implementar un contenedor de la aplicación que se desea equilibrar tooload.</span><span class="sxs-lookup"><span data-stu-id="45e60-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="45e60-130">En primer lugar, obtenga Hola FQDN de los agentes de hello expuesto públicamente.</span><span class="sxs-lookup"><span data-stu-id="45e60-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="45e60-131">A continuación, cree un archivo denominado *web.json hello* y copia en hello siguiendo el contenido.</span><span class="sxs-lookup"><span data-stu-id="45e60-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="45e60-132">Hola `HAPROXY_0_VHOST` etiqueta necesita toobe actualizado con hello FQDN de Hola DC/agentes del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="45e60-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

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

<span data-ttu-id="45e60-133">Usar Hola DC/OS CLI toorun Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="45e60-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="45e60-134">De forma predeterminada maratón implementa Hola Hola aplicación toohello privada del clúster.</span><span class="sxs-lookup"><span data-stu-id="45e60-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="45e60-135">Esto significa que Hola por encima de la implementación solo es accesible a través de un equilibrador de carga, que normalmente es el comportamiento deseado de Hola.</span><span class="sxs-lookup"><span data-stu-id="45e60-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="45e60-136">Una vez que se ha implementado la aplicación hello, examinar toohello FQDN de aplicación con equilibrio de carga de hello agent clúster tooview.</span><span class="sxs-lookup"><span data-stu-id="45e60-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Imagen de la aplicación de carga equilibrada](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="45e60-138">Configuración de Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="45e60-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="45e60-139">De forma predeterminada, Azure Load Balancer expone los puertos 80, 8080 y 443.</span><span class="sxs-lookup"><span data-stu-id="45e60-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="45e60-140">Si usa uno de estos tres puertos (tal como lo hacemos en hello ejemplo anterior), no hay nada que necesita toodo.</span><span class="sxs-lookup"><span data-stu-id="45e60-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="45e60-141">Debe ser capaz de toohit el agente de FQDN del equilibrador de carga, y cada vez que actualice, podrá alcance uno de los servidores web de tres en un modo round-robin.</span><span class="sxs-lookup"><span data-stu-id="45e60-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="45e60-142">Si utiliza un puerto diferente, debe tooadd round robin regla y un sondeo del equilibrador de carga de hello para el puerto de Hola que usó.</span><span class="sxs-lookup"><span data-stu-id="45e60-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="45e60-143">Puede hacerlo desde hello [CLI de Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), con los comandos de hello `azure network lb rule create` y `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="45e60-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45e60-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45e60-144">Next steps</span></span>

<span data-ttu-id="45e60-145">En este tutorial, ha aprendido acerca de equilibrio de carga en ACS con maratón hello y carga de Azure equilibradores incluidos Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="45e60-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45e60-146">Configurar un equilibrador de carga de Marathon</span><span class="sxs-lookup"><span data-stu-id="45e60-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="45e60-147">Implementar una aplicación con el equilibrador de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="45e60-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="45e60-148">Configurar Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="45e60-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="45e60-149">Avanzar toohello toolearn de tutorial siguiente sobre la integración de almacenamiento de Azure con controlador de dominio/OS en Azure.</span><span class="sxs-lookup"><span data-stu-id="45e60-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="45e60-150">Montaje del recurso compartido de archivos de Azure en un clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="45e60-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)