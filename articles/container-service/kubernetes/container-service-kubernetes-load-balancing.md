---
title: aaaLoad equilibrar Kubernetes contenedores en Azure | Documentos de Microsoft
description: "Conéctese externamente y equilibre la carga entre varios contenedores en un clúster de Kubernetes en Azure Container Service."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, microservicios, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="7748a-104">Equilibrio de carga de contenedores en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7748a-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="7748a-105">En este artículo se detalla el equilibrio de carga en un clúster de Kubernetes en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="7748a-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="7748a-106">Equilibrio de carga proporciona una dirección IP accesible desde el exterior para el servicio de Hola y distribuye el tráfico de red entre pod de Hola que se ejecuta en máquinas virtuales de agente.</span><span class="sxs-lookup"><span data-stu-id="7748a-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="7748a-107">Puede configurar un toouse de servicio de Kubernetes [equilibrador de carga Azure](../../load-balancer/load-balancer-overview.md) toomanage tráfico de red (TCP) externo.</span><span class="sxs-lookup"><span data-stu-id="7748a-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="7748a-108">Con la configuración adicional, son posibles el equilibrio de carga y el enrutamiento del tráfico HTTP o HTTPS, así como escenarios más avanzados.</span><span class="sxs-lookup"><span data-stu-id="7748a-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7748a-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7748a-109">Prerequisites</span></span>
* <span data-ttu-id="7748a-110">[Implementar un clúster de Kubernetes](container-service-kubernetes-walkthrough.md) en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7748a-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="7748a-111">[Conectar el cliente](../container-service-connect.md) tooyour clúster</span><span class="sxs-lookup"><span data-stu-id="7748a-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="7748a-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="7748a-112">Azure load balancer</span></span>

<span data-ttu-id="7748a-113">De forma predeterminada, un clúster de Kubernetes implementado en el servicio de contenedor de Azure incluye un equilibrador de carga de Azure orientado a Internet para el agente de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7748a-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="7748a-114">(Un recurso de equilibrador de carga independiente está configurado para master Hola máquinas virtuales). Azure Load Balancer es un equilibrador de carga de nivel 4.</span><span class="sxs-lookup"><span data-stu-id="7748a-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="7748a-115">Actualmente, equilibrador de carga de hello solo admite el tráfico TCP en Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7748a-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="7748a-116">Al crear un servicio de Kubernetes, puede configurar automáticamente hello Azure tooallow acceso toohello servicio del equilibrador de.</span><span class="sxs-lookup"><span data-stu-id="7748a-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="7748a-117">equilibrador de carga de hello tooconfigure, conjunto Hola servicio `type` demasiado`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="7748a-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="7748a-118">equilibrador de carga de Hola crea una regla toomap una dirección IP pública y número de puerto de entrada servicio tráfico toohello las direcciones IP privadas y los números de puerto de pod hello en el agente de VM (y viceversa para el tráfico de respuesta).</span><span class="sxs-lookup"><span data-stu-id="7748a-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="7748a-119">Éstos son algunos ejemplos de dos que muestra cómo tooset Hola servicio Kubernetes `type` demasiado`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="7748a-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="7748a-120">(Después de tratar de obtener ejemplos de hello, eliminar las implementaciones de hello aunque ya no los necesite.)</span><span class="sxs-lookup"><span data-stu-id="7748a-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="7748a-121">Ejemplo: Hola de uso `kubectl expose` comando</span><span class="sxs-lookup"><span data-stu-id="7748a-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="7748a-122">Hola [Kubernetes tutorial](container-service-kubernetes-walkthrough.md) incluye un ejemplo de cómo un servicio con hello tooexpose `kubectl expose` comando y su `--type=LoadBalancer` marca.</span><span class="sxs-lookup"><span data-stu-id="7748a-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="7748a-123">Estos son los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7748a-123">Here are hello steps :</span></span>

1. <span data-ttu-id="7748a-124">Inicie una nueva implementación de contenedor.</span><span class="sxs-lookup"><span data-stu-id="7748a-124">Start a new container deployment.</span></span> <span data-ttu-id="7748a-125">Hola por ejemplo, el siguiente comando inicia una nueva implementación llama `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="7748a-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="7748a-126">implementación de Hello consta de tres contenedores basados en imagen de Docker de hello para el servidor de web Nginx Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="7748a-127">Compruebe que se están ejecutando los contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-127">Verify that hello containers are running.</span></span> <span data-ttu-id="7748a-128">Por ejemplo, si realiza una consulta para los contenedores de hello con `kubectl get pods`, ve resultados similares toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="7748a-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Obtención de contenedores de Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="7748a-130">tooconfigure Hola carga equilibrador tooaccept tráfico externo toohello implementación, ejecute `kubectl expose` con `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="7748a-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="7748a-131">Hello siguiente comando expone hello Nginx servidor en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="7748a-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="7748a-132">Tipo `kubectl get svc` toosee estado de hello de servicios de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="7748a-133">Mientras el equilibrador de carga de hello configura reglas de hello, Hola `EXTERNAL-IP` de hello servicio aparece como `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="7748a-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="7748a-134">Después de unos minutos, se configura la dirección IP externa de hello:</span><span class="sxs-lookup"><span data-stu-id="7748a-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurar Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="7748a-136">Compruebe que puede tener acceso a servicio de hello en la dirección IP externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="7748a-137">Por ejemplo, abra una dirección IP de toohello de explorador web que se muestra.</span><span class="sxs-lookup"><span data-stu-id="7748a-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="7748a-138">Explorador de Hello muestra servidor web hello Nginx que ejecute en uno de los contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="7748a-139">O bien, hello ejecución `curl` o `wget` comando.</span><span class="sxs-lookup"><span data-stu-id="7748a-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="7748a-140">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7748a-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="7748a-141">Debería mostrarse una salida similar a esta:</span><span class="sxs-lookup"><span data-stu-id="7748a-141">You should see output similar to:</span></span>

    ![Acceder a Nginx con curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="7748a-143">configuración de hello toosee hello Azure del equilibrador de carga, vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7748a-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="7748a-144">Busque el grupo de recursos de hello para el clúster de servicio de contenedor y seleccione el equilibrador de carga de hello para el agente de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7748a-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="7748a-145">Su nombre debe ser Hola igual que el servicio de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="7748a-146">(No elija equilibrador de carga de Hola de nodos maestros hello, Hola uno cuyo nombre incluya **lb master**.)</span><span class="sxs-lookup"><span data-stu-id="7748a-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![Equilibrador de carga en el grupo de recursos](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="7748a-148">toosee Hola detalles de configuración de equilibrador de carga de hello, haga clic en **reglas de equilibrio de carga** y el nombre de Hola de regla de Hola que configuró.</span><span class="sxs-lookup"><span data-stu-id="7748a-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Reglas de equilibrador de carga](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="7748a-150">Ejemplo: Especificar `type: LoadBalancer` en el archivo de configuración de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="7748a-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="7748a-151">Si se implementa una aplicación de contenedor de Kubernetes desde un YAML o JSON [archivo de configuración de servicio](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), especifique un equilibrador de carga externo mediante la adición de hello siguiendo la especificación del servicio toohello línea:</span><span class="sxs-lookup"><span data-stu-id="7748a-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="7748a-152">pasos siguientes Hello utilizan hello Kubernetes [ejemplo de libro de visitas](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="7748a-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="7748a-153">Este ejemplo es una aplicación web de varios niveles basada en imágenes de Redis y Docker PHP.</span><span class="sxs-lookup"><span data-stu-id="7748a-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="7748a-154">Puede especificar en el archivo de configuración de servicio de hello que ese servidor PHP de front-end de hello usa el equilibrador de carga de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="7748a-155">Descargar archivo hello `guestbook-all-in-one.yaml` de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="7748a-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="7748a-156">Busque hello `spec` para hello `frontend` servicio.</span><span class="sxs-lookup"><span data-stu-id="7748a-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="7748a-157">Quite el comentario de línea de hello `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="7748a-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![Equilibrador de carga en configuración del servicio](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="7748a-159">Guardar archivo hello e implementar la aplicación hello ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7748a-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="7748a-160">Tipo `kubectl get svc` toosee estado de hello de servicios de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="7748a-161">Mientras el equilibrador de carga de hello configura reglas de hello, Hola `EXTERNAL-IP` de hello `frontend` servicio aparece como `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="7748a-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="7748a-162">Después de unos minutos, se configura la dirección IP externa de hello:</span><span class="sxs-lookup"><span data-stu-id="7748a-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurar Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="7748a-164">Compruebe que puede tener acceso a servicio de hello en la dirección IP externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="7748a-165">Por ejemplo, puede abrir una dirección IP externa de toohello de explorador de web del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Acceder al libro de visitas externamente](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="7748a-167">Puede agregar entradas del libro de visitas.</span><span class="sxs-lookup"><span data-stu-id="7748a-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="7748a-168">configuración de hello toosee hello Azure del equilibrador de carga, buscar recursos de equilibrador de carga de Hola para clúster Hola Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7748a-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7748a-169">Vea Hola los pasos de ejemplo de Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="7748a-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="7748a-170">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="7748a-170">Considerations</span></span>

* <span data-ttu-id="7748a-171">Creación de regla de equilibrador de carga de Hola se realiza de forma asincrónica y la información sobre equilibrador de hello aprovisionado se publica en el servicio de hello `status.loadBalancer` campo.</span><span class="sxs-lookup"><span data-stu-id="7748a-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="7748a-172">Todos los servicios se asignan automáticamente su propia dirección IP virtual en el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="7748a-173">Si lo desea equilibrador de carga de hello tooreach mediante un nombre DNS, trabajar con su toocreate de proveedor de servicio de dominio un nombre DNS para la dirección IP de la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="7748a-174">Tráfico HTTP o HTTPS</span><span class="sxs-lookup"><span data-stu-id="7748a-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="7748a-175">saldo de tooload HTTP o HTTPS tráfico toocontainer aplicaciones web y administrar los certificados de seguridad de la capa de transporte (TLS), puede usar hello Kubernetes [entrada](https://kubernetes.io/docs/user-guide/ingress/) recursos.</span><span class="sxs-lookup"><span data-stu-id="7748a-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="7748a-176">Una entrada es una colección de reglas que permiten las conexiones entrantes en servicios de cluster Server de tooreach Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="7748a-177">Para una toowork de recursos de entrada, hello Kubernetes deben tener un [controlador de entrada](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) ejecutando.</span><span class="sxs-lookup"><span data-stu-id="7748a-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="7748a-178">Azure Container Service no implementa un controlador Ingress de Kubernetes automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7748a-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="7748a-179">Hay varias implementaciones de controlador disponibles.</span><span class="sxs-lookup"><span data-stu-id="7748a-179">Several controller implementations are available.</span></span> <span data-ttu-id="7748a-180">Actualmente, Hola [controlador de entrada de Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) se recomienda tooconfigure reglas de entrada y equilibrio de carga de tráfico HTTP y HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7748a-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="7748a-181">Para obtener más información, vea hello [documentación del controlador de entrada de Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="7748a-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7748a-182">Al utilizar Hola controlador Nginx entrada en servicio de contenedor de Azure, debe exponer como un servicio con la implementación de controladores de hello `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="7748a-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="7748a-183">Esto configura el controlador toohello de tráfico de tooroute de equilibrador de hello carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="7748a-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="7748a-184">Para obtener más información, vea la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="7748a-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7748a-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7748a-185">Next steps</span></span>

* <span data-ttu-id="7748a-186">Vea hello [Kubernetes LoadBalancer documentación](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="7748a-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="7748a-187">Obtener más información sobre los controladores [Ingress de Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="7748a-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="7748a-188">Consultar [ejemplos de Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="7748a-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

