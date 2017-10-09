---
title: proxy inverso de aaaAzure Service Fabric | Documentos de Microsoft
description: "Utiliza a un proxy inverso de Service Fabric para toomicroservices de comunicación desde el interior y exterior clúster Hola."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="981c2-103">Proxy inverso en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="981c2-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="981c2-104">proxy inverso de Hola que está integrado en Azure Service Fabric direcciones microservicios en clúster de Service Fabric Hola que expone los extremos HTTP.</span><span class="sxs-lookup"><span data-stu-id="981c2-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="981c2-105">Modelo de comunicación de microservicios</span><span class="sxs-lookup"><span data-stu-id="981c2-105">Microservices communication model</span></span>
<span data-ttu-id="981c2-106">Microservicios en Service Fabric suele ejecutan en un subconjunto de máquinas virtuales en clúster de Hola y pueden pasar tooanother de una máquina virtual por distintas razones.</span><span class="sxs-lookup"><span data-stu-id="981c2-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="981c2-107">Por lo tanto, los puntos de conexión de Hola para microservicios pueden cambiar dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="981c2-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="981c2-108">Hola patrón típico toocommunicate toohello microservicio es siguiente Hola resolver bucle:</span><span class="sxs-lookup"><span data-stu-id="981c2-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="981c2-109">Resolver la ubicación del servicio Hola inicialmente a través del servicio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="981c2-110">Conectar el servicio toohello.</span><span class="sxs-lookup"><span data-stu-id="981c2-110">Connect toohello service.</span></span>
3. <span data-ttu-id="981c2-111">Determinar la causa de Hola de errores de conexión y resolver la ubicación del servicio Hola de nuevo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="981c2-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="981c2-112">Este proceso implica generalmente bibliotecas de comunicación de cliente en un bucle de reintento que implementa directivas de resolución e inténtelo de nuevo del servicio de Hola de ajuste.</span><span class="sxs-lookup"><span data-stu-id="981c2-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="981c2-113">Para más información, consulte [Conexión y comunicación con los servicios](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="981c2-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="981c2-114">Comunicarse con el proxy inverso Hola</span><span class="sxs-lookup"><span data-stu-id="981c2-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="981c2-115">proxy inverso de Hello en el tejido de servicio se ejecuta en todos los nodos Hola Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="981c2-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="981c2-116">Realiza el proceso de resolución de servicio completo de hello en nombre del cliente y, a continuación, reenvía la solicitud de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="981c2-117">Por lo tanto, los clientes que se ejecutan en el clúster de hello pueden usar cualquier servicio de destino de cliente HTTP comunicación bibliotecas tootalk toohello mediante el uso de proxy inverso de Hola que se ejecuta localmente en Hola mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="981c2-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![Comunicación interna][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="981c2-119">Alcanzar microservicios de clúster de hello exterior</span><span class="sxs-lookup"><span data-stu-id="981c2-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="981c2-120">modelo de comunicación externa Hola predeterminado para microservicios es un modelo de participación en donde no se puede tener acceso a cada servicio directamente desde los clientes externos.</span><span class="sxs-lookup"><span data-stu-id="981c2-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="981c2-121">[El equilibrador de carga Azure](../load-balancer/load-balancer-overview.md), que es un límite de red entre microservicios y los clientes externos, realiza la traducción de direcciones de red y externo reenvía solicitudes de puntos de conexión de toointernal IP: Port.</span><span class="sxs-lookup"><span data-stu-id="981c2-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="981c2-122">toomake clientes de tooexternal directamente accesibles de punto de conexión de microservicio, primero debe configurar tooforward tráfico tooeach puerto que Hola servicio utiliza el equilibrador de carga en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="981c2-123">Además, la mayoría microservicios, especialmente con estado microservicios, no en vivo en todos los nodos del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="981c2-124">Hola microservicios pueden mover entre los nodos de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="981c2-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="981c2-125">En tales casos, equilibrador de carga no se puede determinar eficazmente ubicación Hola del nodo de destino de Hola de hello réplicas toowhich debe reenviar el tráfico.</span><span class="sxs-lookup"><span data-stu-id="981c2-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="981c2-126">Microservicios a través de proxy inverso de Hola de clúster de hello fuera de alcance</span><span class="sxs-lookup"><span data-stu-id="981c2-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="981c2-127">En lugar de configurar el puerto Hola de un servicio individual en el equilibrador de carga, puede configurar solo Hola puerto de proxy inverso de hello en el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="981c2-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="981c2-128">Esta configuración permite a los clientes fuera del clúster de hello tener acceso a servicios en clúster de hello mediante proxy inverso de hello sin ninguna configuración adicional.</span><span class="sxs-lookup"><span data-stu-id="981c2-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![Comunicación externa][0]

> [!WARNING]
> <span data-ttu-id="981c2-130">Cuando se configura el puerto de proxy inverso de hello en equilibrador de carga, son direccionables desde fuera de clúster de hello microservicios todos los clúster de Hola que exponen un extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="981c2-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="981c2-131">Formato URI para tener acceso a servicios mediante el uso de proxy inverso de Hola</span><span class="sxs-lookup"><span data-stu-id="981c2-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="981c2-132">usos de proxy inverso de Hola que se debería reenviar una uniforme de recursos específico (URI) de identificador formato tooidentify Hola partición toowhich Hola entrantes solicitud de servicio:</span><span class="sxs-lookup"><span data-stu-id="981c2-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="981c2-133">**http:** proxy inverso de Hola puede ser configurado tooaccept HTTP o el tráfico HTTPS.</span><span class="sxs-lookup"><span data-stu-id="981c2-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="981c2-134">Para el reenvío de HTTPS, consulte demasiado[conectar el servicio seguro tooa con proxy inverso de hello](service-fabric-reverseproxy-configure-secure-communication.md) una vez que haya toolisten el programa de instalación de proxy inverso en HTTPS.</span><span class="sxs-lookup"><span data-stu-id="981c2-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="981c2-135">**Nombre de dominio completo (FQDN) de clúster | dirección IP interna:** para los clientes externos, puede configurar el proxy inverso de Hola para que sea accesible a través del dominio del clúster hello, como mycluster.eastus.cloudapp.azure.com. De forma predeterminada, proxy inverso de Hola se ejecuta en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="981c2-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="981c2-136">Para el tráfico interno, puede tener acceso proxy inverso de hello en el host local o en cualquier dirección IP de nodo interno, por ejemplo, 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="981c2-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="981c2-137">**Puerto:** se trata de puerto de hello, como 19081, que se ha especificado para el proxy inverso Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="981c2-138">**ServiceInstanceName:** trata Hola completo nombre de instancia de servicio de hello implementada que se está intentando tooreach sin Hola "fabric: /" esquema.</span><span class="sxs-lookup"><span data-stu-id="981c2-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="981c2-139">Por ejemplo, tooreach hello *fabric: / myapp/myservice/* servicio, usaría *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="981c2-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="981c2-140">nombre de instancia de servicio de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="981c2-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="981c2-141">Utilizando un distinguen mayúsculas de minúsculas para el nombre de instancia de servicio de hello en dirección URL de hello hace Hola solicitudes toofail con 404 (no encontrado).</span><span class="sxs-lookup"><span data-stu-id="981c2-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="981c2-142">**Ruta de acceso de sufijo:** es Hola real ruta de acceso URL, como *myapi/valores/agregar/3*, para servicio de Hola que desee tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="981c2-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="981c2-143">**PartitionKey:** para un servicio con particiones, esta es la clave de partición calculada de Hola de partición de Hola que desea tooreach.</span><span class="sxs-lookup"><span data-stu-id="981c2-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="981c2-144">Tenga en cuenta que esto es *no* Hola GUID de Id. de partición.</span><span class="sxs-lookup"><span data-stu-id="981c2-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="981c2-145">Este parámetro no es necesario para los servicios que utilizan el esquema de partición de singleton de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="981c2-146">**PartitionKind:** se trata de esquema de partición de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="981c2-147">El valor puede ser Int64Range o Con nombre.</span><span class="sxs-lookup"><span data-stu-id="981c2-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="981c2-148">Este parámetro no es necesario para los servicios que utilizan el esquema de partición de singleton de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="981c2-149">**ListenerName** los extremos de Hola de servicio de hello tienen formato de Hola {"Extremos": {"Listener1": "Endpoint1", "Listener2": "Endpoint2"...}}.</span><span class="sxs-lookup"><span data-stu-id="981c2-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="981c2-150">Cuando el servicio de hello expone varios puntos de conexión, se identifica el punto de conexión de hello esa solicitud de cliente de Hola se debería reenviar a.</span><span class="sxs-lookup"><span data-stu-id="981c2-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="981c2-151">Esto se puede omitir si el servicio de hello tiene sólo un agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="981c2-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="981c2-152">**TargetReplicaSelector** especifica cómo se debe seleccionar instancia o la réplica de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="981c2-153">Cuando el servicio de destino de hello está activo, hello TargetReplicaSelector puede ser uno de los siguientes Hola: 'PrimaryReplica', 'RandomSecondaryReplica' o 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="981c2-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="981c2-154">Si no se especifica este parámetro, valor predeterminado de hello es 'PrimaryReplica'.</span><span class="sxs-lookup"><span data-stu-id="981c2-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="981c2-155">Cuando el servicio de destino de hello no tiene estado, proxy inverso toma una instancia de solicitud hello tooforward de partición de servicio de Hola a aleatorio.</span><span class="sxs-lookup"><span data-stu-id="981c2-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="981c2-156">**Tiempo de espera:** Esto especifica el tiempo de espera de Hola para solicitud de hello HTTP creado por toohello servicio de proxy inverso de hello en nombre de la solicitud de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="981c2-157">valor de Hello predeterminado es 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="981c2-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="981c2-158">Se trata de un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="981c2-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="981c2-159">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="981c2-159">Example usage</span></span>
<span data-ttu-id="981c2-160">Por ejemplo, vamos a echar hello *fabric: / MyApp/MyService* servicio que se abre un agente de escucha HTTP en hello después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="981c2-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="981c2-161">Siguientes son recursos de hello para el servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="981c2-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="981c2-162">Si servicio de hello utiliza singleton Hola esquema de partición, Hola *PartitionKey* y *PartitionKind* parámetros de cadena de consulta no son necesarios, y puede tener acceso al servicio de hello mediante el uso de la puerta de enlace de hello como:</span><span class="sxs-lookup"><span data-stu-id="981c2-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="981c2-163">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="981c2-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="981c2-164">Internamente: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="981c2-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="981c2-165">Si el servicio de Hola usa Hola Int64 uniforme esquema de partición, Hola *PartitionKey* y *PartitionKind* parámetros de cadena de consulta deben ser tooreach usa una partición de servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="981c2-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="981c2-166">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="981c2-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="981c2-167">Internamente: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="981c2-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="981c2-168">recursos de hello tooreach que expone el servicio de hello, basta con colocar la ruta de acceso de recursos de Hola después de nombre de servicio de hello en dirección URL de hello:</span><span class="sxs-lookup"><span data-stu-id="981c2-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="981c2-169">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="981c2-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="981c2-170">Internamente: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="981c2-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="981c2-171">puerta de enlace de Hello, a continuación, reenvía la dirección URL del servicio estas solicitudes toohello:</span><span class="sxs-lookup"><span data-stu-id="981c2-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="981c2-172">Control especial de los servicios de uso compartido de puertos</span><span class="sxs-lookup"><span data-stu-id="981c2-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="981c2-173">La puerta de enlace de aplicaciones Azure intenta tooresolve un servicio nuevo de direcciones y vuelva a intentar la solicitud de hello cuando un servicio no se puede obtener acceso.</span><span class="sxs-lookup"><span data-stu-id="981c2-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="981c2-174">Se trata de una de las ventajas principal de puerta de enlace de aplicación porque el código de cliente no necesita tooimplement su propia resolución de servicio y resolver el bucle.</span><span class="sxs-lookup"><span data-stu-id="981c2-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="981c2-175">Por lo general, cuando no se puede alcanzar un servicio, instancia de servicio de Hola o réplica ha movido tooa otro nodo como parte de su ciclo de vida normal.</span><span class="sxs-lookup"><span data-stu-id="981c2-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="981c2-176">Cuando esto sucede, puerta de enlace de aplicaciones puede recibir una conexión de red error que indica que un punto de conexión es que no abierto más tiempo en hello originalmente resolver direcciones.</span><span class="sxs-lookup"><span data-stu-id="981c2-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="981c2-177">Sin embargo, las instancias del servicio o las réplicas pueden compartir un proceso de host y un puerto cuando un servidor web basado en http.sys las hospeda; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="981c2-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="981c2-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="981c2-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="981c2-179">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="981c2-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="981c2-180">Katana</span><span class="sxs-lookup"><span data-stu-id="981c2-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="981c2-181">En esta situación, es probable que el servidor web Hola está disponible en el proceso de host de Hola y responde toorequests pero Hola resolver la instancia del servicio o réplica ya no está disponible en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="981c2-182">En este caso, la puerta de enlace de hello recibirá una respuesta HTTP 404 de servidor web de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="981c2-183">Este tipo de respuesta tiene dos lecturas diferentes:</span><span class="sxs-lookup"><span data-stu-id="981c2-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="981c2-184">Caja #1: la dirección de servicio de hello es correcta, pero el recurso Hola Hola usuario solicitado no existe.</span><span class="sxs-lookup"><span data-stu-id="981c2-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="981c2-185">Caso #2: la dirección de servicio de hello es incorrecto y recurso de Hola Hola el usuario solicitó puede encontrarse en otro nodo.</span><span class="sxs-lookup"><span data-stu-id="981c2-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="981c2-186">Hola primer caso es un error 404 de HTTP normal, que se considera un error de usuario.</span><span class="sxs-lookup"><span data-stu-id="981c2-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="981c2-187">Sin embargo, en el segundo caso hello, usuario Hola ha solicitado un recurso que existen.</span><span class="sxs-lookup"><span data-stu-id="981c2-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="981c2-188">Puerta de enlace de aplicaciones era toolocate que se ha movido porque Hola propio servicio.</span><span class="sxs-lookup"><span data-stu-id="981c2-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="981c2-189">Aplicación puerta de enlace necesidades tooresolve Hola dirección nuevo y solicitud de Hola de reintento.</span><span class="sxs-lookup"><span data-stu-id="981c2-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="981c2-190">Puerta de enlace de aplicaciones, por tanto, necesita un toodistinguish forma entre estos dos casos.</span><span class="sxs-lookup"><span data-stu-id="981c2-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="981c2-191">toomake que existe una distinción, una sugerencia de servidor hello es necesaria.</span><span class="sxs-lookup"><span data-stu-id="981c2-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="981c2-192">De forma predeterminada, puerta de enlace de aplicaciones se da por supuesto caso #2 y trata tooresolve y emitir solicitudes de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="981c2-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="981c2-193">tooindicate caso &#1; tooApplication puerta de enlace, el servicio de hello debería devolver Hola siguiente encabezado de respuesta HTTP:</span><span class="sxs-lookup"><span data-stu-id="981c2-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="981c2-194">Este encabezado de respuesta HTTP indica una situación de HTTP 404 normal en qué Hola recurso solicitado no existe y puerta de enlace de aplicaciones no intentará volver a dirección de servicio de tooresolve Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="981c2-195">Instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="981c2-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="981c2-196">Habilitar proxy inverso mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="981c2-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="981c2-197">Portal de Azure proporciona a un proxy inverso de tooenable opción al crear un nuevo clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="981c2-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="981c2-198">En **clúster crear Service Fabric**, paso 2: configuración del clúster, configuración de tipo de nodo, seleccione también Hola casilla "Habilitar proxy inverso".</span><span class="sxs-lookup"><span data-stu-id="981c2-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="981c2-199">Para configurar el proxy inverso segura, se puede especificar certificado SSL en el paso 3: seguridad, establecer la configuración de seguridad de clúster, seleccione Hola casilla demasiado "Incluyen un certificado SSL para el proxy inverso" y escriba los detalles del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="981c2-200">Habilitar proxy inverso mediante plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="981c2-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="981c2-201">Puede usar hello [plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable Hola proxy inverso de Service Fabric para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="981c2-202">Consulte demasiado[Proxy inverso de HTTPS configurar en un clúster segura](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) ejemplos de plantilla para el Administrador de recursos de Azure tooconfigure proxy inverso seguro con un certificado y el control de sustitución del certificado.</span><span class="sxs-lookup"><span data-stu-id="981c2-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="981c2-203">En primer lugar, obtendrá plantilla hello para el clúster de Hola que desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="981c2-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="981c2-204">Puede usar plantillas de ejemplo de Hola o crear una plantilla personalizada que el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="981c2-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="981c2-205">A continuación, puede habilitar a proxy inverso de hello mediante Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="981c2-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="981c2-206">Definir un puerto de proxy inverso de Hola Hola [sección parámetros](../azure-resource-manager/resource-group-authoring-templates.md) de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="981c2-207">Especifique el puerto de Hola para cada uno de los objetos de nodetype Hola Hola **clúster** [sección de recursos de tipo](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="981c2-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="981c2-208">puerto de Hola se identifica mediante el nombre del parámetro hello, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="981c2-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="981c2-209">Hola tooaddress proxy inverso de hello exterior clúster de Azure, configurar reglas de equilibrador de carga de Azure de hello para el puerto de Hola que especificó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="981c2-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="981c2-210">tooconfigure certificados SSL en el puerto de hello para el proxy inverso de hello, agregar Hola certificado toohello ***reverseProxyCertificate*** propiedad Hola **clúster** [sección de tipo de recurso](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="981c2-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="981c2-211">Compatibilidad con un certificado de proxy inverso que es diferente del certificado de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="981c2-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="981c2-212">Si el certificado de proxy inverso de hello es distinto del certificado de Hola que protege el clúster de hello, a continuación, Hola especificado anteriormente certificado debe instalarse en la máquina virtual de Hola y agrega la lista de control de acceso (ACL) de toohello para que puedan Service Fabric obtener acceso a él.</span><span class="sxs-lookup"><span data-stu-id="981c2-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="981c2-213">Esto puede hacerse en hello **virtualMachineScaleSets** [sección de recursos de tipo](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="981c2-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="981c2-214">Para la instalación, agregue ese osProfile toohello de certificado.</span><span class="sxs-lookup"><span data-stu-id="981c2-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="981c2-215">sección de extensión de Hola de plantilla de hello puede actualizar el certificado de Hola Hola ACL.</span><span class="sxs-lookup"><span data-stu-id="981c2-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="981c2-216">Cuando se usan certificados que son diferentes de hello clúster certificado tooenable Hola proxy inverso en un clúster existente, instalar certificado de proxy inverso de Hola y actualizar Hola ACL en clúster de hello antes de habilitar el proxy inverso Hola.</span><span class="sxs-lookup"><span data-stu-id="981c2-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="981c2-217">Hola completa [plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) implementación mediante la configuración de hello mencionadas anteriormente antes de iniciar un proxy inverso de implementación tooenable hello en los pasos 1 a 4.</span><span class="sxs-lookup"><span data-stu-id="981c2-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="981c2-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="981c2-218">Next steps</span></span>
* <span data-ttu-id="981c2-219">Vea un ejemplo de comunicación HTTP entre los servicios de un [proyecto de ejemplo en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="981c2-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="981c2-220">Reenvío de servicio de toosecure HTTP con proxy inverso de Hola</span><span class="sxs-lookup"><span data-stu-id="981c2-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="981c2-221">Llamadas a procedimiento remoto con la comunicación remota de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="981c2-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="981c2-222">API web que usa OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="981c2-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="981c2-223">Comunicación WCF con la utilización de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="981c2-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="981c2-224">Para opciones adicionales de la configuración del proxy inverso, consulte la sección de ApplicationGateway/Http en [Personalización de la configuración del clúster de Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="981c2-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
