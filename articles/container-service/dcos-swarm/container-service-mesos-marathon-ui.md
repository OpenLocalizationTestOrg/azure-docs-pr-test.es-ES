---
title: "clúster de Azure DC/OS aaaManage con interfaz de usuario de maratón | Documentos de Microsoft"
description: "Implementar el servicio de Cluster Server de contenedores tooan servicio de contenedor de Azure mediante el uso de la interfaz de usuario de web de maratón Hola."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="91fc7-104">Administrar un clúster de servicio de contenedor de Azure DC/OS a través de la interfaz de usuario de web de maratón Hola</span><span class="sxs-lookup"><span data-stu-id="91fc7-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="91fc7-105">Controlador de dominio/OS proporciona un entorno para implementar y ampliar las cargas de trabajo en clúster, mientras la abstracción de hardware subyacente Hola.</span><span class="sxs-lookup"><span data-stu-id="91fc7-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="91fc7-106">Por encima de DC/OS hay un marco que administra la programación y ejecución de cargas de trabajo de proceso.</span><span class="sxs-lookup"><span data-stu-id="91fc7-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="91fc7-107">Mientras los marcos están disponibles para muchas cargas de trabajo populares, este documento describe cómo tooget introducción sobre cómo implementar contenedores con maratón.</span><span class="sxs-lookup"><span data-stu-id="91fc7-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="91fc7-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="91fc7-108">Prerequisites</span></span>
<span data-ttu-id="91fc7-109">Antes de trabajar con estos ejemplos, necesita un clúster de DC/OS configurado en el servicio Contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="91fc7-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="91fc7-110">También necesita clúster de toothis de conectividad remota de toohave.</span><span class="sxs-lookup"><span data-stu-id="91fc7-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="91fc7-111">Para obtener más información sobre estos elementos, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="91fc7-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="91fc7-112">Implementación de un clúster del servicio Contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="91fc7-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="91fc7-113">Conectar el clúster del servicio de contenedor de Azure tooan</span><span class="sxs-lookup"><span data-stu-id="91fc7-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="91fc7-114">En este artículo se da por supuesto que está realizando un túnel clúster de DC/OS toohello a través de su puerto local 80.</span><span class="sxs-lookup"><span data-stu-id="91fc7-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="91fc7-115">Explorar Hola interfaz de usuario del controlador de dominio/OS</span><span class="sxs-lookup"><span data-stu-id="91fc7-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="91fc7-116">Con un túnel de Shell seguro (SSH) [establece](../container-service-connect.md), examinar toohttp://localhost/.</span><span class="sxs-lookup"><span data-stu-id="91fc7-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="91fc7-117">Esto carga la interfaz de usuario de web de Hola DC/OS y muestra información sobre el clúster de hello, como los recursos usados, activos agentes y servicios en ejecución.</span><span class="sxs-lookup"><span data-stu-id="91fc7-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![Interfaz de usuario de DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="91fc7-119">Explorar Hola maratón UI</span><span class="sxs-lookup"><span data-stu-id="91fc7-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="91fc7-120">Hola toosee maratón de interfaz de usuario, busque toohttp://localhost/marathon.</span><span class="sxs-lookup"><span data-stu-id="91fc7-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="91fc7-121">Desde esta pantalla, puede iniciar un nuevo contenedor u otra aplicación en clúster del servicio de contenedor de Azure DC/OS Hola.</span><span class="sxs-lookup"><span data-stu-id="91fc7-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="91fc7-122">También puede ver información acerca de cómo ejecutar contenedores y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="91fc7-122">You can also see information about running containers and applications.</span></span>  

![Interfaz de usuario de Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="91fc7-124">Implementación de un contenedor con formato Docker</span><span class="sxs-lookup"><span data-stu-id="91fc7-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="91fc7-125">toodeploy un nuevo contenedor mediante el uso de maratón, haga clic en **crear aplicación**y escriba Hola siguiente información en las fichas del formulario hello:</span><span class="sxs-lookup"><span data-stu-id="91fc7-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="91fc7-126">Campo</span><span class="sxs-lookup"><span data-stu-id="91fc7-126">Field</span></span> | <span data-ttu-id="91fc7-127">Valor</span><span class="sxs-lookup"><span data-stu-id="91fc7-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="91fc7-128">ID</span><span class="sxs-lookup"><span data-stu-id="91fc7-128">ID</span></span> |<span data-ttu-id="91fc7-129">nginx</span><span class="sxs-lookup"><span data-stu-id="91fc7-129">nginx</span></span> |
| <span data-ttu-id="91fc7-130">Memoria</span><span class="sxs-lookup"><span data-stu-id="91fc7-130">Memory</span></span> | <span data-ttu-id="91fc7-131">32</span><span class="sxs-lookup"><span data-stu-id="91fc7-131">32</span></span> |
| <span data-ttu-id="91fc7-132">Imagen</span><span class="sxs-lookup"><span data-stu-id="91fc7-132">Image</span></span> |<span data-ttu-id="91fc7-133">nginx</span><span class="sxs-lookup"><span data-stu-id="91fc7-133">nginx</span></span> |
| <span data-ttu-id="91fc7-134">Red</span><span class="sxs-lookup"><span data-stu-id="91fc7-134">Network</span></span> |<span data-ttu-id="91fc7-135">Bridged</span><span class="sxs-lookup"><span data-stu-id="91fc7-135">Bridged</span></span> |
| <span data-ttu-id="91fc7-136">Puerto de host</span><span class="sxs-lookup"><span data-stu-id="91fc7-136">Host Port</span></span> |<span data-ttu-id="91fc7-137">80</span><span class="sxs-lookup"><span data-stu-id="91fc7-137">80</span></span> |
| <span data-ttu-id="91fc7-138">Protocol</span><span class="sxs-lookup"><span data-stu-id="91fc7-138">Protocol</span></span> |<span data-ttu-id="91fc7-139">TCP</span><span class="sxs-lookup"><span data-stu-id="91fc7-139">TCP</span></span> |

![Nueva interfaz de usuario de la aplicación: General](./media/container-service-mesos-marathon-ui/dcos4.png)

![Nueva interfaz de usuario de la aplicación: Contenedor de Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Nueva interfaz de usuario de la aplicación: Detección de servicios y puertos](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="91fc7-143">Si desea toostatically mapa Hola contenedor tooa puerto en el agente de hello, deberá toouse modo de JSON.</span><span class="sxs-lookup"><span data-stu-id="91fc7-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="91fc7-144">toodo cambiar por lo tanto, Asistente para la nueva aplicación Hola demasiado**JSON modo** mediante el uso de alternancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="91fc7-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="91fc7-145">A continuación, escriba Hola después de la configuración en hello `portMappings` sección de definición de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="91fc7-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="91fc7-146">Este ejemplo enlaza el puerto 80 de hello contenedor tooport 80 del agente de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="91fc7-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="91fc7-147">Puede volver a cambiar el modo JSON del Asistente después de realizar este cambio.</span><span class="sxs-lookup"><span data-stu-id="91fc7-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Nueva interfaz de usuario de la aplicación: Ejemplo con el puerto 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="91fc7-149">Si desea que las comprobaciones de mantenimiento tooenable, establezca una ruta de acceso en hello **comprobaciones de mantenimiento** ficha.</span><span class="sxs-lookup"><span data-stu-id="91fc7-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![Interfaz de usuario para nueva aplicación: comprobaciones de estado](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="91fc7-151">clúster de DC/OS Hola se implementa con conjunto de agentes públicos y privados.</span><span class="sxs-lookup"><span data-stu-id="91fc7-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="91fc7-152">Para hello toobe tooaccess capaz de las aplicaciones de clúster de hello Internet, deberá a agente pública de toodeploy Hola aplicaciones tooa.</span><span class="sxs-lookup"><span data-stu-id="91fc7-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="91fc7-153">toodo por lo tanto, seleccione hello **opcional** ficha del Asistente para nueva aplicación de Hola y escriba **slave_public** para hello **aceptado recursos Roles**.</span><span class="sxs-lookup"><span data-stu-id="91fc7-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="91fc7-154">Haga clic en **Create Application** (Crear aplicación).</span><span class="sxs-lookup"><span data-stu-id="91fc7-154">Then click **Create Application**.</span></span>

![Nueva interfaz de usuario de la aplicación: Configuración del agente público](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="91fc7-156">En página principal de maratón de hello, podrá ver el estado de implementación de hello para el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="91fc7-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="91fc7-157">Inicialmente verá un estado **Deploying** (Implementando).</span><span class="sxs-lookup"><span data-stu-id="91fc7-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="91fc7-158">Después de una implementación correcta, Hola cambios de estado demasiado**ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="91fc7-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Página principal de la interfaz de usuario de Marathon: Estado de la implementación del contenedor](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="91fc7-160">Cuando se cambia (http://localhost/) de la interfaz de usuario de la web de DC/OS toohello atrás, verá que se está ejecutando una tarea (en este caso, un contenedor con Docker formato) en clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="91fc7-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![Interfaz de usuario, tarea que se ejecuta en el clúster de hello web de DC/OS](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="91fc7-162">nodo del clúster hello toosee Hola tarea se ejecuta en, haga clic en hello **nodos** ficha.</span><span class="sxs-lookup"><span data-stu-id="91fc7-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![Interfaz de usuario web de DC/OS: nodo de clúster de la tarea](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="91fc7-164">Alcanzar contenedor Hola</span><span class="sxs-lookup"><span data-stu-id="91fc7-164">Reach hello container</span></span>

<span data-ttu-id="91fc7-165">En este ejemplo, se ejecuta la aplicación de hello en un nodo de agente pública.</span><span class="sxs-lookup"><span data-stu-id="91fc7-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="91fc7-166">Alcanzar la aplicación hello de hello internet examinando toohello agente FQDN del clúster de hello: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, donde:</span><span class="sxs-lookup"><span data-stu-id="91fc7-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="91fc7-167">**DNSPREFIX** es Hola prefijo DNS que proporcionó al implementar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="91fc7-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="91fc7-168">**REGIÓN** es región hello en el que se encuentra el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="91fc7-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![Nginx de Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="91fc7-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91fc7-170">Next steps</span></span>
* [<span data-ttu-id="91fc7-171">Trabajar con el controlador de dominio/OS y Hola maratón API</span><span class="sxs-lookup"><span data-stu-id="91fc7-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="91fc7-172">Profundización en el servicio de contenedor de Azure con Mesos Hola</span><span class="sxs-lookup"><span data-stu-id="91fc7-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
