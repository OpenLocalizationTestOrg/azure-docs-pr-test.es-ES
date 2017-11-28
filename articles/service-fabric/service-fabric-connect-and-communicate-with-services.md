---
title: aaaConnect y comunicarse con los servicios de Azure Service Fabric | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooresolve, conectarse y comunicarse con servicios de Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="c6243-103">Conexión y comunicación con servicios en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c6243-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="c6243-104">En Service Fabric, un servicio se ejecuta en algún lugar en un clúster de Service Fabric que normalmente se distribuye entre varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c6243-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="c6243-105">Se puede mover desde un solo lugar tooanother, ya sea por el propietario del servicio hello, o automáticamente por Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c6243-105">It can be moved from one place tooanother, either by hello service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="c6243-106">Servicios no están vinculados estáticamente tooa una máquina determinada o la dirección.</span><span class="sxs-lookup"><span data-stu-id="c6243-106">Services are not statically tied tooa particular machine or address.</span></span>

<span data-ttu-id="c6243-107">Una aplicación de Service Fabric se compone, por lo general, de muchos servicios diferentes, donde cada uno de ellos realiza una tarea especializada.</span><span class="sxs-lookup"><span data-stu-id="c6243-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="c6243-108">Estos servicios pueden comunicarse entre sí tooform una función completa, por ejemplo, de diferentes partes de la representación de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c6243-108">These services may communicate with each other tooform a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="c6243-109">También hay aplicaciones que se conectan tooand comunican con los servicios de cliente.</span><span class="sxs-lookup"><span data-stu-id="c6243-109">There are also client applications that connect tooand communicate with services.</span></span> <span data-ttu-id="c6243-110">Este documento se describen cómo tooset la comunicación con y entre los servicios de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c6243-110">This document discusses how tooset up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="c6243-111">Este vídeo de Microsoft Virtual Academy también explica la comunicación del servicio: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="c6243-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="c6243-112">Traiga su propio protocolo</span><span class="sxs-lookup"><span data-stu-id="c6243-112">Bring your own protocol</span></span>
<span data-ttu-id="c6243-113">Service Fabric ayuda a administrar Hola del ciclo de vida de los servicios pero no efectúa ninguna decisión sobre lo que los servicios.</span><span class="sxs-lookup"><span data-stu-id="c6243-113">Service Fabric helps manage hello lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="c6243-114">Esto incluye la comunicación.</span><span class="sxs-lookup"><span data-stu-id="c6243-114">This includes communication.</span></span> <span data-ttu-id="c6243-115">Cuando se abre el servicio de Service Fabric, es decir, tooset de oportunidad de su servicio en un extremo para las solicitudes entrantes, mediante cualquier pila de comunicación o protocolo que desee.</span><span class="sxs-lookup"><span data-stu-id="c6243-115">When your service is opened by Service Fabric, that's your service's opportunity tooset up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="c6243-116">El servicio escuchará en una dirección **IP:port** normal mediante cualquier esquema de direccionamiento, como un URI.</span><span class="sxs-lookup"><span data-stu-id="c6243-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="c6243-117">Varias instancias de servicio o réplicas pueden compartir un proceso de host, en cuyo caso que se necesita toouse distintos puertos o usar un mecanismo de uso compartido de puertos, como controlador de núcleo de http.sys hello en Windows.</span><span class="sxs-lookup"><span data-stu-id="c6243-117">Multiple service instances or replicas may share a host process, in which case they will either need toouse different ports or use a port-sharing mechanism, such as hello http.sys kernel driver in Windows.</span></span> <span data-ttu-id="c6243-118">En ambos casos, cada instancia de servicio o réplica de un proceso de host debe ser direccionable de forma exclusiva.</span><span class="sxs-lookup"><span data-stu-id="c6243-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![puntos de conexión de servicio][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="c6243-120">Detección y resolución de servicios</span><span class="sxs-lookup"><span data-stu-id="c6243-120">Service discovery and resolution</span></span>
<span data-ttu-id="c6243-121">En un sistema distribuido, pueden mover los servicios de tooanother de una máquina con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="c6243-121">In a distributed system, services may move from one machine tooanother over time.</span></span> <span data-ttu-id="c6243-122">Esto puede ocurrir por diversos motivos, incluidos el equilibrio, las actualizaciones, las conmutaciones por error o el escalado de recursos. Esto significa cambian de direcciones de extremo de servicio como servicio Hola mueve toonodes con direcciones IP diferentes y puede abrir en puertos diferentes si el servicio de hello usa un puerto seleccionado dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="c6243-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as hello service moves toonodes with different IP addresses, and may open on different ports if hello service uses a dynamically selected port.</span></span>

![Distribución de servicios][7]

<span data-ttu-id="c6243-124">Tejido de servicio proporciona una detección y la resolución que se llamó al servicio Hola Naming Service.</span><span class="sxs-lookup"><span data-stu-id="c6243-124">Service Fabric provides a discovery and resolution service called hello Naming Service.</span></span> <span data-ttu-id="c6243-125">Hello Naming Service mantiene una tabla que asigna los toohello direcciones de extremo que escuchan en instancias de servicio con nombre.</span><span class="sxs-lookup"><span data-stu-id="c6243-125">hello Naming Service maintains a table that maps named service instances toohello endpoint addresses they listen on.</span></span> <span data-ttu-id="c6243-126">Todas las instancias de servicio con nombre en Service Fabric tienen nombres únicos como URI como, por ejemplo, `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="c6243-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="c6243-127">nombre de Hello del servicio de hello no cambia con vida Hola Hola, es solo direcciones de extremo de Hola que pueden cambiar cuando mueve servicios.</span><span class="sxs-lookup"><span data-stu-id="c6243-127">hello name of hello service does not change over hello lifetime of hello service, it's only hello endpoint addresses that can change when services move.</span></span> <span data-ttu-id="c6243-128">Esto es análogo toowebsites con direcciones URL constantes pero donde puede cambiar la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-128">This is analogous toowebsites that have constant URLs but where hello IP address may change.</span></span> <span data-ttu-id="c6243-129">Y tooDNS similar en web de hello, que se resuelve direcciones de tooIP de direcciones URL de sitios Web, Service Fabric tiene un registrador que se asigna la dirección del extremo de tootheir de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="c6243-129">And similar tooDNS on hello web, which resolves website URLs tooIP addresses, Service Fabric has a registrar that maps service names tootheir endpoint address.</span></span>

![puntos de conexión de servicio][2]

<span data-ttu-id="c6243-131">Resolver y conectar tooservices implica Hola siguiendo los pasos que se ejecute en un bucle:</span><span class="sxs-lookup"><span data-stu-id="c6243-131">Resolving and connecting tooservices involves hello following steps run in a loop:</span></span>

* <span data-ttu-id="c6243-132">**Resolver**: punto de conexión Hola Get que ha publicado un servicio de Hola Naming Service.</span><span class="sxs-lookup"><span data-stu-id="c6243-132">**Resolve**: Get hello endpoint that a service has published from hello Naming Service.</span></span>
* <span data-ttu-id="c6243-133">**Conectar**: conectar toohello servicio sobre cualquier protocolo que se usa en ese punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="c6243-133">**Connect**: Connect toohello service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="c6243-134">**Vuelva a intentar**: un intento de conexión puede producir un error de una serie de motivos, por ejemplo, si el servicio de Hola se mueve desde la dirección de extremo de hello última hora Hola se resolvió.</span><span class="sxs-lookup"><span data-stu-id="c6243-134">**Retry**: A connection attempt may fail for any number of reasons, for example if hello service has moved since hello last time hello endpoint address was resolved.</span></span> <span data-ttu-id="c6243-135">En ese caso, Hola anterior resolución y conectar pasos deben toobe vuelve a intentar y este ciclo se repite hasta que la conexión de Hola se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="c6243-135">In that case, hello preceding resolve and connect steps need toobe retried, and this cycle is repeated until hello connection succeeds.</span></span>

## <a name="connecting-tooother-services"></a><span data-ttu-id="c6243-136">Conectar servicios tooother</span><span class="sxs-lookup"><span data-stu-id="c6243-136">Connecting tooother services</span></span>
<span data-ttu-id="c6243-137">Servicios que se conectan tooeach sí dentro de un clúster por lo general puede acceder directamente a los puntos de conexión de Hola de otros servicios porque los nodos de hello en un clúster están en hello misma red local.</span><span class="sxs-lookup"><span data-stu-id="c6243-137">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="c6243-138">toomake es más fácil tooconnect entre servicios, Service Fabric proporciona servicios adicionales que usan Hola Naming Service.</span><span class="sxs-lookup"><span data-stu-id="c6243-138">toomake is easier tooconnect between services, Service Fabric provides additional services that use hello Naming Service.</span></span> <span data-ttu-id="c6243-139">Un servicio DNS y un servicio de proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="c6243-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="c6243-140">Servicio DNS</span><span class="sxs-lookup"><span data-stu-id="c6243-140">DNS service</span></span>
<span data-ttu-id="c6243-141">Dado que muchos servicios, especialmente en los servicios en contenedores, pueden tener un nombre de dirección URL existente, tooresolve capaz de estos mediante Hola protocolo DNS estándar (en lugar de protocolo del servicio de nomenclatura de hello) es muy prácticos, especialmente en aplicaciones "Levantar y mover" escenarios.</span><span class="sxs-lookup"><span data-stu-id="c6243-141">Since many services, especially containerized services, can have an existing URL name, being able tooresolve these using hello standard DNS protocol (rather than hello Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="c6243-142">Esto es exactamente qué servicio DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-142">This is exactly what hello DNS service does.</span></span> <span data-ttu-id="c6243-143">Permite toomap DNS nombres tooa nombre del servicio y, por tanto, resolver direcciones IP del extremo.</span><span class="sxs-lookup"><span data-stu-id="c6243-143">It enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="c6243-144">Como se muestra en hello siguiente diagrama, Hola servicio DNS, en ejecución en el clúster de Service Fabric hello, asigna nombres de tooservice de nombres DNS que, a continuación, se resuelven utilizando Hola Naming Service tooreturn Hola extremo direcciones tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="c6243-144">As shown in hello following diagram, hello DNS service, running in hello Service Fabric cluster, maps DNS names tooservice names which are then resolved by hello Naming Service tooreturn hello endpoint addresses tooconnect to.</span></span> <span data-ttu-id="c6243-145">nombre DNS de Hello para el servicio de Hola se proporciona en tiempo de Hola de creación.</span><span class="sxs-lookup"><span data-stu-id="c6243-145">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![puntos de conexión de servicio][9]

<span data-ttu-id="c6243-147">Para obtener más detalles sobre cómo ver hello toouse servicio DNS [servicio DNS en Azure Service Fabric](service-fabric-dnsservice.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="c6243-147">For more details on how toouse hello DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="c6243-148">Servicio de proxy inverso</span><span class="sxs-lookup"><span data-stu-id="c6243-148">Reverse proxy service</span></span>
<span data-ttu-id="c6243-149">servicios en clúster de Hola que expone extremos HTTP incluidos HTTPS de direcciones de proxy inverso de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-149">hello reverse proxy addresses services in hello cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="c6243-150">proxy inverso Hola simplifica considerablemente la llamada a otros servicios y sus métodos debido a un determinado formato de URI e identificadores resolver hello, conectar, Hola a pasos de reintento necesarios para toocommunicate de un servicio con el uso de otro servicio de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="c6243-150">hello reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles hello resolve, connect, retry steps required for one service toocommunicate with another using hello Naming Serivce.</span></span> <span data-ttu-id="c6243-151">En otras palabras, se oculta Hola servicio de escribir el nombre del usuario al llamar a otros servicios haciendo esto tan sencillo como llamar a una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="c6243-151">In other words, it hides hello Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![puntos de conexión de servicio][10]

<span data-ttu-id="c6243-153">Para obtener más detalles sobre cómo toouse Hola invertir el servicio de proxy, consulte [proxy en Azure Service Fabric inverso](service-fabric-reverseproxy.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="c6243-153">For more details on how toouse hello reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="c6243-154">Conexiones desde clientes externos</span><span class="sxs-lookup"><span data-stu-id="c6243-154">Connections from external clients</span></span>
<span data-ttu-id="c6243-155">Servicios que se conectan tooeach sí dentro de un clúster por lo general puede acceder directamente a los puntos de conexión de Hola de otros servicios porque los nodos de hello en un clúster están en hello misma red local.</span><span class="sxs-lookup"><span data-stu-id="c6243-155">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="c6243-156">Sin embargo, en algunos entornos, un clúster puede estar detrás de un equilibrador de carga que enruta el tráfico de entrada externo a través de un conjunto limitado de puertos.</span><span class="sxs-lookup"><span data-stu-id="c6243-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="c6243-157">En estos casos, los servicios todavía pueden comunicarse entre sí y resolver direcciones mediante Hola Naming Service, pero realizar pasos adicionales deben ser tomada tooallow los clientes externos tooconnect tooservices.</span><span class="sxs-lookup"><span data-stu-id="c6243-157">In these cases, services can still communicate with each other and resolve addresses using hello Naming Service, but extra steps must be taken tooallow external clients tooconnect tooservices.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="c6243-158">Service Fabric en Azure</span><span class="sxs-lookup"><span data-stu-id="c6243-158">Service Fabric in Azure</span></span>
<span data-ttu-id="c6243-159">Un clúster de Service Fabric en Azure se coloca detrás de un equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6243-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="c6243-160">Todos los clústeres de toohello de tráfico externo deben pasar a través del equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-160">All external traffic toohello cluster must pass through hello load balancer.</span></span> <span data-ttu-id="c6243-161">Hello equilibrador de carga automáticamente reenviará el tráfico entrante en un tooa determinado puerto aleatorio *nodo* cuya Hola abrir el mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="c6243-161">hello load balancer will automatically forward traffic inbound on a given port tooa random *node* that has hello same port open.</span></span> <span data-ttu-id="c6243-162">Hello equilibrador de carga de Azure solo conoce puertos abiertos en hello *nodos*, no conozca puertos abiertos individuo *services*.</span><span class="sxs-lookup"><span data-stu-id="c6243-162">hello Azure Load Balancer only knows about ports open on hello *nodes*, it does not know about ports open by individual *services*.</span></span>

![Topología de equilibrador de carga de Azure y Service Fabric][3]

<span data-ttu-id="c6243-164">Por ejemplo, en orden tooaccept externo el tráfico en el puerto **80**, debe configurarse Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="c6243-164">For example, in order tooaccept external traffic on port **80**, hello following things must be configured:</span></span>

1. <span data-ttu-id="c6243-165">Escriba un servicio que escuche en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="c6243-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="c6243-166">Configurar el puerto 80 en ServiceManifest.xml del servicio de Hola y abrir un agente de escucha en el servicio de hello, por ejemplo, un servidor web hospedado por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="c6243-166">Configure port 80 in hello service's ServiceManifest.xml and open a listener in hello service, for example, a self-hosted web server.</span></span>

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. <span data-ttu-id="c6243-167">Crear un clúster de Service Fabric en Azure y especifique el puerto **80** como un puerto de extremo personalizado para el tipo de nodo de Hola que va a hospedar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for hello node type that will host hello service.</span></span> <span data-ttu-id="c6243-168">Si tiene más de un tipo de nodo, puede configurar un *restricción de emplazamiento* en hello tooensure de servicio sólo se ejecuta en el tipo de nodo de Hola que tiene abierto el puerto de extremo personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-168">If you have more than one node type, you can set up a *placement constraint* on hello service tooensure it only runs on hello node type that has hello custom endpoint port opened.</span></span>

    ![Apertura de un puerto en un tipo de nodo][4]
3. <span data-ttu-id="c6243-170">Una vez que se haya creado el clúster de hello, configure Hola equilibrador de carga de Azure en el tráfico de tooforward de grupo de recursos del clúster de hello en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="c6243-170">Once hello cluster has been created, configure hello Azure Load Balancer in hello cluster's Resource Group tooforward traffic on port 80.</span></span> <span data-ttu-id="c6243-171">Al crear un clúster a través de hello portal de Azure, esto se configura automáticamente para cada puerto de extremo personalizado que se configuró.</span><span class="sxs-lookup"><span data-stu-id="c6243-171">When creating a cluster through hello Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Reenviar el tráfico en hello equilibrador de carga de Azure][5]
4. <span data-ttu-id="c6243-173">Hola utiliza el equilibrador de carga Azure un toodetermine sondeo si o no toosend tráfico tooa de nodo concreto.</span><span class="sxs-lookup"><span data-stu-id="c6243-173">hello Azure Load Balancer uses a probe toodetermine whether or not toosend traffic tooa particular node.</span></span> <span data-ttu-id="c6243-174">Hola sondeo comprueba periódicamente un punto de conexión en cada toodetermine de nodo o no está respondiendo nodo Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-174">hello probe periodically checks an endpoint on each node toodetermine whether or not hello node is responding.</span></span> <span data-ttu-id="c6243-175">Si el sondeo de hello no tooreceive una respuesta después de un número determinado de veces, equilibrador de carga de hello deja de enviar nodo toothat de tráfico.</span><span class="sxs-lookup"><span data-stu-id="c6243-175">If hello probe fails tooreceive a response after a configured number of times, hello load balancer stops sending traffic toothat node.</span></span> <span data-ttu-id="c6243-176">Al crear un clúster a través de hello portal de Azure, un sondeo se configura automáticamente para cada puerto de extremo personalizado que se configuró.</span><span class="sxs-lookup"><span data-stu-id="c6243-176">When creating a cluster through hello Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Reenviar el tráfico en hello equilibrador de carga de Azure][8]

<span data-ttu-id="c6243-178">Es importante tooremember que hello equilibrador de carga de Azure y sondeo Hola solo conocen hello *nodos*, no Hola *servicios* ejecutan en nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-178">It's important tooremember that hello Azure Load Balancer and hello probe only know about hello *nodes*, not hello *services* running on hello nodes.</span></span> <span data-ttu-id="c6243-179">Hola equilibrador de carga de Azure siempre enviará tráfico toonodes que respondan toohello sondeo, por lo que debe tener cuidado tooensure servicios están disponibles en los nodos de Hola que se pueda toorespond toohello sondeo.</span><span class="sxs-lookup"><span data-stu-id="c6243-179">hello Azure Load Balancer will always send traffic toonodes that respond toohello probe, so care must be taken tooensure services are available on hello nodes that are able toorespond toohello probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="c6243-180">Reliable Services: opciones de API de comunicación integradas</span><span class="sxs-lookup"><span data-stu-id="c6243-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="c6243-181">Hola servicios confiables framework incluye varias opciones de comunicación pregenerado.</span><span class="sxs-lookup"><span data-stu-id="c6243-181">hello Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="c6243-182">Decisión de Hello sobre los cuales uno adaptará mejor a los depende de elección de Hola de hello programación modelo, marco de comunicación de Hola y Hola lenguaje de programación que los servicios se escriben en.</span><span class="sxs-lookup"><span data-stu-id="c6243-182">hello decision about which one will work best for you depends on hello choice of hello programming model, hello communication framework, and hello programming language that your services are written in.</span></span>

* <span data-ttu-id="c6243-183">**Ningún protocolo específico:** si no tiene una opción determinada del marco de comunicación, pero desea tooget algo activos y en funcionamiento rápidamente, Hola opción ideal para usted es [comunicación remota de servicio](service-fabric-reliable-services-communication-remoting.md), lo que permite llamadas a procedimiento remoto fuertemente tipado para servicios de confianza y actores confiable.</span><span class="sxs-lookup"><span data-stu-id="c6243-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want tooget something up and running quickly, then hello ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="c6243-184">Esto es más fácil de hello y tooget de forma más rápida a trabajar con comunicación del servicio.</span><span class="sxs-lookup"><span data-stu-id="c6243-184">This is hello easiest and fastest way tooget started with service communication.</span></span> <span data-ttu-id="c6243-185">La comunicación remota de servicio controla la resolución de direcciones, la conexión, los reintentos y el control de errores del servicio.</span><span class="sxs-lookup"><span data-stu-id="c6243-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="c6243-186">Esto está disponible para aplicaciones de C# y Java.</span><span class="sxs-lookup"><span data-stu-id="c6243-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="c6243-187">**HTTP**: para una comunicación independiente del lenguaje, HTTP proporciona una opción estándar con las herramientas y los servidores HTTP disponibles en muchos lenguajes diferentes, compatibles todos ellos con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c6243-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="c6243-188">Los servicios pueden usar cualquier pila HTTP disponible, incluida la [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) para aplicaciones de C#.</span><span class="sxs-lookup"><span data-stu-id="c6243-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="c6243-189">Los clientes escritos en C# pueden aprovechar hello `ICommunicationClient` y `ServicePartitionClient` clases, mientras que para Java, usar hello `CommunicationClient` y `FabricServicePartitionClient` clases, [para la resolución de servicio, las conexiones HTTP y bucles de reintento](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="c6243-189">Clients written in C# can leverage hello `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use hello `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="c6243-190">**WCF**: Si tienes código existente que usa WCF como el marco de comunicación, puede usar hello `WcfCommunicationListener` para el lado del servidor de Hola y `WcfCommunicationClient` y `ServicePartitionClient` clases para cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6243-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use hello `WcfCommunicationListener` for hello server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for hello client.</span></span> <span data-ttu-id="c6243-191">Pero esto solo está disponible para las aplicaciones de C# en clústeres basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="c6243-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="c6243-192">Para obtener más información, consulte el artículo [implementación basada en WCF de pila de comunicación de hello](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="c6243-192">For more details, see this article about [WCF-based implementation of hello communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="c6243-193">Uso de protocolos personalizados y otros marcos de comunicación</span><span class="sxs-lookup"><span data-stu-id="c6243-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="c6243-194">Los servicios pueden usar cualquier protocolo o marco de comunicación, ya sea un protocolo binario personalizado sobre sockets de TCP o eventos de streaming a través de [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) o [IoT Hub de Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="c6243-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="c6243-195">Service Fabric proporciona comunicación las API que se puede conectar la pila de comunicación en, mientras todos los Hola trabajar toodiscover y conectar se abstrae del usuario.</span><span class="sxs-lookup"><span data-stu-id="c6243-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all hello work toodiscover and connect is abstracted from you.</span></span> <span data-ttu-id="c6243-196">Consulte este artículo sobre hello [modelo de comunicación de servicio confiable](service-fabric-reliable-services-communication.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="c6243-196">See this article about hello [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6243-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6243-197">Next steps</span></span>
<span data-ttu-id="c6243-198">Aprender más acerca de conceptos de Hola y de API disponibles en hello [modelo de comunicación de servicios de confianza](service-fabric-reliable-services-communication.md), a continuación, empezar a trabajar rápidamente con [comunicación remota de servicio](service-fabric-reliable-services-communication-remoting.md) o visite toolearn detallada de cómo toowrite un agente de escucha de comunicación con [API Web con OWIN autohospedaje](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="c6243-198">Learn more about hello concepts and APIs available in hello [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth toolearn how toowrite a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
