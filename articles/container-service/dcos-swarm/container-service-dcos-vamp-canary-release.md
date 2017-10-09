---
title: "versión de aaaCanary con Vamp en clúster de Azure DC/OS | Documentos de Microsoft"
description: "Cómo toouse Vamp toocanary servicios de lanzamiento y aplicar el filtrado en un clúster de servicio de contenedor de Azure DC/OS inteligente del tráfico"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="034fa-103">Lanzamiento controlado de microservicios con Vamp en un clúster de DC/OS de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="034fa-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="034fa-104">En este tutorial, se configura Vamp en Azure Container Service con un clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="034fa-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="034fa-105">Publicamos canary servicio de demostración de hello Vamp "sava" y, a continuación, resolver una incompatibilidad de servicio de hello con Firefox aplicando el filtrado de tráfico inteligente.</span><span class="sxs-lookup"><span data-stu-id="034fa-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="034fa-106">En este tutorial Vamp se ejecuta en un clúster de DC/OS, pero también se puede utilizar Vamp con Kubernetes como orchestrator Hola.</span><span class="sxs-lookup"><span data-stu-id="034fa-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="034fa-107">Acerca de los lanzamientos controlados y Vamp</span><span class="sxs-lookup"><span data-stu-id="034fa-107">About canary releases and Vamp</span></span>


<span data-ttu-id="034fa-108">El [lanzamiento controlado](https://martinfowler.com/bliki/CanaryRelease.html) es una estrategia de implementación inteligente adoptada por organizaciones innovadoras como Netflix, Facebook y Spotify.</span><span class="sxs-lookup"><span data-stu-id="034fa-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="034fa-109">Es un método que tiene sentido, ya que reduce los problemas, incluye redes de seguridad y aumenta la innovación.</span><span class="sxs-lookup"><span data-stu-id="034fa-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="034fa-110">¿Y por qué no se usa en todas las compañías?</span><span class="sxs-lookup"><span data-stu-id="034fa-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="034fa-111">Extender una tooinclude de canalización de CI/CD estrategias canary agrega complejidad y requiere devops amplios conocimientos y experiencia.</span><span class="sxs-lookup"><span data-stu-id="034fa-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="034fa-112">Que es suficiente tooblock pequeñas empresas y las empresas similares antes de que incluso empezar a trabajar.</span><span class="sxs-lookup"><span data-stu-id="034fa-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="034fa-113">[Vamp](http://vamp.io/) es un sistema de código abierto diseñado tooease esta transición y poner canary liberando características tooyour preferido contenedor programador.</span><span class="sxs-lookup"><span data-stu-id="034fa-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="034fa-114">La funcionalidad controlada de Vamp va más allá de las implementaciones basadas en porcentajes.</span><span class="sxs-lookup"><span data-stu-id="034fa-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="034fa-115">El tráfico se puede filtrar y dividir en una amplia variedad de condiciones, por ejemplo tootarget determinados usuarios, intervalos de IP o dispositivos.</span><span class="sxs-lookup"><span data-stu-id="034fa-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="034fa-116">Vamp realiza un seguimiento y un análisis de las métricas de rendimiento, lo que permite una automatización basada en datos reales.</span><span class="sxs-lookup"><span data-stu-id="034fa-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="034fa-117">Puede configurar la reversión automática en caso de error o escalar variantes de servicios individuales en función de la carga o la latencia.</span><span class="sxs-lookup"><span data-stu-id="034fa-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="034fa-118">Configuración de Azure Container Service con DC/OS</span><span class="sxs-lookup"><span data-stu-id="034fa-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="034fa-119">[Implemente un clúster de DC/OS](container-service-deployment.md) con un maestro y dos agentes de tamaño predeterminado.</span><span class="sxs-lookup"><span data-stu-id="034fa-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="034fa-120">[Crear un túnel SSH](../container-service-connect.md) clúster de tooconnect toohello DC/OS.</span><span class="sxs-lookup"><span data-stu-id="034fa-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="034fa-121">En este artículo se da por supuesto que tunelizar toohello clúster en el puerto local 80.</span><span class="sxs-lookup"><span data-stu-id="034fa-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="034fa-122">Configuración de Vamp</span><span class="sxs-lookup"><span data-stu-id="034fa-122">Set up Vamp</span></span>

<span data-ttu-id="034fa-123">Ahora que tiene un clúster de DC/OS ejecución, puede instalar Vamp desde Hola interfaz de usuario del controlador de dominio/OS (http://localhost: 80).</span><span class="sxs-lookup"><span data-stu-id="034fa-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![Interfaz de usuario de DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="034fa-125">La instalación se lleva a cabo en dos fases:</span><span class="sxs-lookup"><span data-stu-id="034fa-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="034fa-126">**Implemente Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="034fa-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="034fa-127">A continuación, **implementar Vamp** mediante la instalación de paquete de universo de hello Vamp DC/OS.</span><span class="sxs-lookup"><span data-stu-id="034fa-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="034fa-128">Implementación de Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="034fa-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="034fa-129">Vamp necesita Elasticsearch para recopilar y agregar métricas.</span><span class="sxs-lookup"><span data-stu-id="034fa-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="034fa-130">Puede usar hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy una pila Vamp Elasticsearch compatible.</span><span class="sxs-lookup"><span data-stu-id="034fa-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="034fa-131">Hola de interfaz de usuario del controlador de dominio/OS, vaya demasiado**servicios** y haga clic en **implementar servicio**.</span><span class="sxs-lookup"><span data-stu-id="034fa-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="034fa-132">Seleccione **modo JSON** de hello **implementar nuevo servicio** emergente.</span><span class="sxs-lookup"><span data-stu-id="034fa-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![Selección del modo JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="034fa-134">Pegue en hello después de JSON.</span><span class="sxs-lookup"><span data-stu-id="034fa-134">Paste in hello following JSON.</span></span> <span data-ttu-id="034fa-135">Esta configuración ejecuta el contenedor de hello con 1 GB de RAM y una comprobación básica del estado en el puerto de hello Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="034fa-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="034fa-136">Haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="034fa-136">Click **Deploy**.</span></span>

  <span data-ttu-id="034fa-137">Controlador de dominio/OS implementa contenedor de hello Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="034fa-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="034fa-138">Puede realizar el seguimiento del progreso en hello **servicios** página.</span><span class="sxs-lookup"><span data-stu-id="034fa-138">You can track progress on hello **Services** page.</span></span>  

  ![Implementación de Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="034fa-140">Implementación de Vamp</span><span class="sxs-lookup"><span data-stu-id="034fa-140">Deploy Vamp</span></span>

<span data-ttu-id="034fa-141">Una vez Elasticsearch notifica como **ejecuta**, puede agregar paquete de universo de DC/OS Vamp Hola.</span><span class="sxs-lookup"><span data-stu-id="034fa-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="034fa-142">Vaya demasiado**universo** y busque **vamp**.</span><span class="sxs-lookup"><span data-stu-id="034fa-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="034fa-143">![Vamp en el universo de DC/OS](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="034fa-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="034fa-144">Haga clic en **instalar** toohello siguiente vamp paquete y elija **instalación avanzada**.</span><span class="sxs-lookup"><span data-stu-id="034fa-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="034fa-145">Desplácese hacia abajo y escriba Hola después elasticsearch url: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="034fa-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Escriba la dirección URL de Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="034fa-147">Haga clic en **revise e instale**, a continuación, haga clic en **instalar** implementación de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="034fa-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="034fa-148">DC/OS implementa todos los componentes de Vamp necesarios.</span><span class="sxs-lookup"><span data-stu-id="034fa-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="034fa-149">Puede realizar el seguimiento del progreso en hello **servicios** página.</span><span class="sxs-lookup"><span data-stu-id="034fa-149">You can track progress on hello **Services** page.</span></span>
  
  ![Implementación de Vamp como paquete de universo](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="034fa-151">Una vez completada la implementación, puede tener acceso a hello Vamp interfaz de usuario:</span><span class="sxs-lookup"><span data-stu-id="034fa-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![Servicio de Vamp en DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interfaz de usuario de Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="034fa-154">Implementación de su primer servicio</span><span class="sxs-lookup"><span data-stu-id="034fa-154">Deploy your first service</span></span>

<span data-ttu-id="034fa-155">Ahora que Vamp está en funcionamiento, implemente un servicio desde un plano.</span><span class="sxs-lookup"><span data-stu-id="034fa-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="034fa-156">En su forma más simple, un [Vamp plano](http://vamp.io/documentation/using-vamp/blueprints/) describe Hola extremos (puertas de enlace), clústeres y toodeploy de servicios.</span><span class="sxs-lookup"><span data-stu-id="034fa-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="034fa-157">Vamp usa clústeres toogroup diferentes variaciones de hello mismo servicio en grupos lógicos para liberar canary o A realizar pruebas A/b.</span><span class="sxs-lookup"><span data-stu-id="034fa-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="034fa-158">Este escenario usa una aplicación monolítica de ejemplo denominada [**sava**](https://github.com/magneticio/sava), que se encuentra en la versión 1.0.</span><span class="sxs-lookup"><span data-stu-id="034fa-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="034fa-159">monolito Hola se empaqueta en un contenedor de Docker, que se encuentra en Docker Hub en magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="034fa-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="034fa-160">aplicación Hello normalmente se ejecuta en el puerto 8080, pero desea tooexpose en puerto 9050 en este caso.</span><span class="sxs-lookup"><span data-stu-id="034fa-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="034fa-161">Implementar la aplicación hello a través de Vamp con un esquema simple.</span><span class="sxs-lookup"><span data-stu-id="034fa-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="034fa-162">Vaya demasiado**implementaciones**.</span><span class="sxs-lookup"><span data-stu-id="034fa-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="034fa-163">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="034fa-163">Click **Add**.</span></span>

3. <span data-ttu-id="034fa-164">Pegar en hello después plano YAML.</span><span class="sxs-lookup"><span data-stu-id="034fa-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="034fa-165">Este plano contiene un clúster con solo una variante de servicio, que se cambia en un paso posterior:</span><span class="sxs-lookup"><span data-stu-id="034fa-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="034fa-166">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="034fa-166">Click **Save**.</span></span> <span data-ttu-id="034fa-167">Vamp inicia la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="034fa-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="034fa-168">aparece la implementación de Hello en hello **implementaciones** página.</span><span class="sxs-lookup"><span data-stu-id="034fa-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="034fa-169">Haga clic en hello implementación toomonitor su estado.</span><span class="sxs-lookup"><span data-stu-id="034fa-169">Click hello deployment toomonitor its status.</span></span>

![Interfaz de usuario de Vamp: implementar sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Servicio sava en la interfaz de usuario de Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="034fa-172">Se crean dos puertas de enlace, que se muestran en hello **puertas de enlace** página:</span><span class="sxs-lookup"><span data-stu-id="034fa-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="034fa-173">un hello tooaccess de extremo estable ejecutando el servicio (puerto 9050)</span><span class="sxs-lookup"><span data-stu-id="034fa-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="034fa-174">una puerta de enlace interna administrada por Vamp (información sobre esta puerta de enlace más adelante).</span><span class="sxs-lookup"><span data-stu-id="034fa-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Interfaz de usuario de Vamp: puertas de enlace de sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="034fa-176">Ahora ha implementado el servicio de Hello sava, pero no puede acceder externamente puesto Hola equilibrador de carga Azure desconoce tooforward tráfico tooit todavía.</span><span class="sxs-lookup"><span data-stu-id="034fa-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="034fa-177">servicio de hello tooaccess, Hola de actualización de configuración de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="034fa-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="034fa-178">Actualizar configuración de red de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="034fa-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="034fa-179">Vamp implementa el servicio de sava de hello en nodos de agente de Hola DC/OS, exponer un extremo en el puerto 9050 estable.</span><span class="sxs-lookup"><span data-stu-id="034fa-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="034fa-180">servicio de hello tooaccess del clúster de DC/OS Hola exterior, realizar las Hola siguiente configuración de red de Azure toohello de cambios en la implementación de clúster:</span><span class="sxs-lookup"><span data-stu-id="034fa-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="034fa-181">**Configurar Hola equilibrador de carga Azure** para los agentes de hello (Hola recurso denominado **dcos-agent-lb-xxxx**) con un sondeo de estado y un tráfico de tooforward de regla en instancias de puerto 9050 toohello sava.</span><span class="sxs-lookup"><span data-stu-id="034fa-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="034fa-182">**Grupo de seguridad de red de actualizaciones hello** para agentes pública hello (Hola recurso denominado **XXXX agente público nsg XXXX**) tooallow tráfico en el puerto 9050.</span><span class="sxs-lookup"><span data-stu-id="034fa-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="034fa-183">Para obtener pasos detallados toocomplete estas tareas con hello Azure portal, vea [habilitar la aplicación de servicio de contenedor de Azure de acceso público tooan](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="034fa-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="034fa-184">Especifique el puerto 9050 en todas las configuraciones de puerto.</span><span class="sxs-lookup"><span data-stu-id="034fa-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="034fa-185">Una vez que todo se ha creado, vaya toohello **Introducción** hoja del equilibrador de carga de agente de Hola DC/OS (Hola recurso denominado **dcos-agent-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="034fa-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="034fa-186">Buscar hello **dirección IP pública**y utilice Hola dirección tooaccess sava de puerto 9050.</span><span class="sxs-lookup"><span data-stu-id="034fa-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Azure Portal: obtener la dirección IP pública](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="034fa-189">Ejecución de un lanzamiento controlado</span><span class="sxs-lookup"><span data-stu-id="034fa-189">Run a canary release</span></span>

<span data-ttu-id="034fa-190">Suponga que tiene una nueva versión de esta aplicación que desea que la versión toocanary en producción.</span><span class="sxs-lookup"><span data-stu-id="034fa-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="034fa-191">Tiene que incluir en contenedores como magneticio/sava:1.1.0 y toogo listo.</span><span class="sxs-lookup"><span data-stu-id="034fa-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="034fa-192">Vamp le permite agregar fácilmente nuevos toohello de servicios ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="034fa-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="034fa-193">Estos servicios "combinados" se implementan junto con los servicios existentes en clúster de Hola Hola y le asigna un peso de 0%.</span><span class="sxs-lookup"><span data-stu-id="034fa-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="034fa-194">Tráfico no es servicio de tooa enrutado recién combinado hasta ajustar una distribución del tráfico Hola.</span><span class="sxs-lookup"><span data-stu-id="034fa-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="034fa-195">control deslizante de peso de Hola Hola Vamp interfaz de usuario proporciona un control total sobre la distribución de hello, lo que permite ajustes incrementales (versión canary) o una reversión de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="034fa-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="034fa-196">Combinación de una nueva variante de servicio</span><span class="sxs-lookup"><span data-stu-id="034fa-196">Merge a new service variant</span></span>

<span data-ttu-id="034fa-197">toomerge Hola nuevo sava 1.1 servicio con hello ejecutando implementación:</span><span class="sxs-lookup"><span data-stu-id="034fa-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="034fa-198">Hola Vamp interfaz de usuario, haga clic en **planos**.</span><span class="sxs-lookup"><span data-stu-id="034fa-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="034fa-199">Haga clic en **agregar** y pegar en hello después plano YAML: esta guía describe un nuevo toodeploy variante (sava: 1.1.0) de servicio en clúster existente de hello (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="034fa-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="034fa-200">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="034fa-200">Click **Save**.</span></span> <span data-ttu-id="034fa-201">plano técnico Hola se almacena y aparece en hello **planos** página.</span><span class="sxs-lookup"><span data-stu-id="034fa-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="034fa-202">Menú de acción de hello abierto en el plano de Hola sava: 1.1 y haga clic en **Merge para**.</span><span class="sxs-lookup"><span data-stu-id="034fa-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Interfaz de usuario de Vamp: planos](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="034fa-204">Seleccione hello **sava** implementación y haga clic en **mezcla**.</span><span class="sxs-lookup"><span data-stu-id="034fa-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![Interfaz de usuario de vamp - combinar plano toodeployment](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="034fa-206">Vamp implementa Hola nueva sava: 1.1.0 variante de un servicio se describe en el plano de hello junto con sava: 1.0.0 Hola **sava_cluster** de hello ejecutando la implementación.</span><span class="sxs-lookup"><span data-stu-id="034fa-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![Interfaz de usuario de Vamp: implementación de sava actualizada](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="034fa-208">Hola **sava/sava_cluster/webport** (punto de conexión de clúster de hello) de la puerta de enlace también se actualiza, agregar una ruta toohello recién implementado sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="034fa-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="034fa-209">En este momento, no el tráfico se enruta a continuación (hello **peso** se establece too0%).</span><span class="sxs-lookup"><span data-stu-id="034fa-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![Interfaz de usuario de Vamp: puerta de enlace de clúster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="034fa-211">Lanzamiento controlado</span><span class="sxs-lookup"><span data-stu-id="034fa-211">Canary release</span></span>

<span data-ttu-id="034fa-212">Con ambas versiones de sava implementado en hello mismo clúster, ajuste la distribución de Hola de tráfico entre ellas moviendo hello **peso** control deslizante.</span><span class="sxs-lookup"><span data-stu-id="034fa-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="034fa-213">Haga clic en ![Vamp una interfaz de usuario: editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) siguiente demasiado**peso**.</span><span class="sxs-lookup"><span data-stu-id="034fa-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="034fa-214">Establecer Hola peso distribución too50%/50% y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="034fa-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![Interfaz de usuario de Vamp: control deslizante de peso de puerta de enlace](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="034fa-216">Retroceda tooyour explorador y actualizar página de hello sava varias veces.</span><span class="sxs-lookup"><span data-stu-id="034fa-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="034fa-217">aplicación Hola sava cambia entre una página sava: 1.0 y una página sava: 1.1.</span><span class="sxs-lookup"><span data-stu-id="034fa-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![Alternar entre los servicios sava1.0 y sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="034fa-219">Este alternancia de página Hola funciona mejor con Hola "Incógnito" o "Anónimo" modo de su explorador debido a Hola almacenamiento en caché de activos estáticos.</span><span class="sxs-lookup"><span data-stu-id="034fa-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="034fa-220">Filtrado del tráfico</span><span class="sxs-lookup"><span data-stu-id="034fa-220">Filter traffic</span></span>

<span data-ttu-id="034fa-221">Suponga que, después de la implementación, detecta una incompatibilidad en sava:1.1.0 que causa problemas de visualización en los exploradores Firefox.</span><span class="sxs-lookup"><span data-stu-id="034fa-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="034fa-222">Puede establecer Vamp toofilter el tráfico entrante y dirigir que toohello conocida estable sava: 1.0.0 hacer copia de todos los usuarios de Firefox.</span><span class="sxs-lookup"><span data-stu-id="034fa-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="034fa-223">Este filtro al instante resuelve Hola interrupciones para los usuarios de Firefox, mientras los demás continúa tooenjoy ventajas de Hola de hello había mejorado sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="034fa-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="034fa-224">Vamp utiliza **condiciones** toofilter el tráfico entre las rutas en una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="034fa-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="034fa-225">El tráfico en primer lugar se filtra y dirige correspondiente toohello condiciones aplicadas tooeach ruta.</span><span class="sxs-lookup"><span data-stu-id="034fa-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="034fa-226">Todo el tráfico restante se distribuye según la configuración de peso de puerta de enlace de toohello.</span><span class="sxs-lookup"><span data-stu-id="034fa-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="034fa-227">Puede crear una condición toofilter todos los usuarios de Firefox y dirigirlas toohello sava: 1.0.0 anterior:</span><span class="sxs-lookup"><span data-stu-id="034fa-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="034fa-228">En hello sava/sava_cluster/webport **puertas de enlace** página, haga clic en ![Vamp una interfaz de usuario: editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd una **condición** toohello ruta sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="034fa-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="034fa-229">Escriba la condición de hello **usuario-agente == Firefox** y haga clic en ![Vamp una interfaz de usuario: Guardar](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="034fa-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="034fa-230">Vamp agrega la condición de hello con la seguridad predeterminada de 0%.</span><span class="sxs-lookup"><span data-stu-id="034fa-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="034fa-231">toostart filtrando el tráfico, deberá intensidad de condición de tooadjust Hola.</span><span class="sxs-lookup"><span data-stu-id="034fa-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="034fa-232">Haga clic en ![Vamp una interfaz de usuario: editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **intensidad** aplica toohello condición.</span><span class="sxs-lookup"><span data-stu-id="034fa-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="034fa-233">Conjunto hello **intensidad** too100% y haga clic en ![Vamp una interfaz de usuario: Guardar](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span><span class="sxs-lookup"><span data-stu-id="034fa-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="034fa-234">Vamp ahora envía todo el tráfico coincidente Hola condición (todos los usuarios de Firefox) toosava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="034fa-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![Vamp la interfaz de usuario: aplicar la condición toogateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="034fa-236">Por último, ajustar toosend de peso de puerta de enlace de hello todas las restantes tráfico (todos los usuarios de Firefox no) toohello nueva sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="034fa-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="034fa-237">Haga clic en ![Vamp una interfaz de usuario: editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) siguiente demasiado**peso** y establecer la distribución de pesos de Hola por lo que es de 100% toohello dirigido ruta sava/sava_cluster/sava:1.1.0/webport.</span><span class="sxs-lookup"><span data-stu-id="034fa-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="034fa-238">Todo el tráfico que no se filtran por la condición de hello ahora es dirigido toohello nueva sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="034fa-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="034fa-239">filtro de hello toosee en acción, abra dos distintos exploradores (uno Firefox y un otro explorador) y obtenga acceso a hello sava de ambos.</span><span class="sxs-lookup"><span data-stu-id="034fa-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="034fa-240">Todas las solicitudes de Firefox se envían toosava:1.0.0, mientras que todos los demás exploradores son toosava:1.1.0 dirigido.</span><span class="sxs-lookup"><span data-stu-id="034fa-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![Interfaz de usuario de Vamp: filtrar el tráfico](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="034fa-242">Resumen</span><span class="sxs-lookup"><span data-stu-id="034fa-242">Summing up</span></span>

<span data-ttu-id="034fa-243">Este artículo es una tooVamp introducción rápida en un clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="034fa-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="034fa-244">Para empezar, copiadas Vamp hasta y ejecuta en el servicio de contenedor de Azure DC/OS clúster, implementar un servicio con un plano Vamp y accedió a él en el punto de conexión de hello expone (puerta de enlace).</span><span class="sxs-lookup"><span data-stu-id="034fa-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="034fa-245">Hemos tratado también algunas características eficaces de Vamp: combinar una toohello variant de servicio nueva ejecución de implementación y presentación de forma incremental y, a continuación, filtrar tráfico tooresolve una incompatibilidad conocida.</span><span class="sxs-lookup"><span data-stu-id="034fa-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="034fa-246">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="034fa-246">Next steps</span></span>

* <span data-ttu-id="034fa-247">Obtenga información acerca de cómo administrar las acciones de Vamp a través de hello [Vamp API de REST](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="034fa-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="034fa-248">Cree scripts de automatización de Vamp en Node.js y ejecútelos como [flujos de trabajo de Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="034fa-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="034fa-249">Consulte más [tutoriales sobre VAMP](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="034fa-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

