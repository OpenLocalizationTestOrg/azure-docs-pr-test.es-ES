---
title: "Comunicación de servicio con ASP.NET Core | Microsoft Docs"
description: Aprenda a usar ASP.NET Core en Reliable Services con y sin estado.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 8ac4d409f7363e8b4ae98be659a627ac8db8d787
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="7f73e-103">ASP.NET Core en Reliable Services de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7f73e-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="7f73e-104">ASP.NET Core es un nuevo marco de código abierto multiplataforma para crear aplicaciones conectadas a Internet modernas y basadas en la nube, como aplicaciones web, aplicaciones de IoT y back-ends móviles.</span><span class="sxs-lookup"><span data-stu-id="7f73e-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="7f73e-105">Este artículo es una guía en profundidad sobre cómo hospedar servicios de ASP.NET Core en Reliable Services de Service Fabric mediante el conjunto de paquetes NuGet **Microsoft.ServiceFabric.AspNetCore.***.</span><span class="sxs-lookup"><span data-stu-id="7f73e-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="7f73e-106">Para ver un tutorial introductorio sobre ASP.NET Core en Service Fabric e instrucciones para configurar el entorno de desarrollo, consulte [Creación de un front-end de servicio web para una aplicación mediante ASP.NET Core](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="7f73e-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="7f73e-107">En el resto de este artículo se da por supuesto que ya conoce ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7f73e-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="7f73e-108">Si no es así, se recomienda leer los [fundamentos de ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="7f73e-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="7f73e-109">ASP.NET Core en el entorno de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7f73e-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="7f73e-110">Aunque las aplicaciones de ASP.NET Core se pueden ejecutar en .NET Core o en la versión completa de .NET Framework, actualmente los servicios de Service Fabric solo se pueden ejecutar en esta última.</span><span class="sxs-lookup"><span data-stu-id="7f73e-110">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="7f73e-111">Esto significa que, cuando se crea un servicio de Service Fabric de ASP.NET Core, todavía debe tener como destino la versión completa de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="7f73e-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="7f73e-112">ASP.NET Core se puede utilizar de dos maneras diferentes en Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="7f73e-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="7f73e-113">**Implementado como archivo ejecutable invitado**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="7f73e-114">Se usa principalmente para ejecutar aplicaciones ASP.NET Core existentes en Service Fabric sin realizar ningún cambio en el código.</span><span class="sxs-lookup"><span data-stu-id="7f73e-114">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="7f73e-115">**Ejecutado dentro de una instancia de Reliable Services**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="7f73e-116">Permite una mejor integración con el entorno de ejecución de Service Fabric y permite servicios ASP.NET Core con estado.</span><span class="sxs-lookup"><span data-stu-id="7f73e-116">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="7f73e-117">En el resto de este artículo se explica cómo usar ASP.NET Core dentro de una instancia de Reliable Services mediante los componentes de integración de ASP.NET Core que se incluyen con el SDK de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7f73e-117">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="7f73e-118">Hospedaje de servicios de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7f73e-118">Service Fabric service hosting</span></span>

<span data-ttu-id="7f73e-119">En Service Fabric, una o varias instancias o réplicas del servicio se ejecutan en un *proceso de host de servicio* (un archivo ejecutable que ejecuta el código del servicio).</span><span class="sxs-lookup"><span data-stu-id="7f73e-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="7f73e-120">Aunque, como autor del servicio, usted es el propietario del proceso de host de servicio, Service Fabric lo activa y supervisa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7f73e-120">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="7f73e-121">Tradicionalmente, ASP.NET (hasta MVC 5) ha estado estrechamente unido a IIS a través de System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="7f73e-121">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="7f73e-122">ASP.NET Core proporciona una separación entre el servidor web y la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7f73e-122">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="7f73e-123">Esto permite que las aplicaciones web sean portátiles entre diferentes servidores web y también que los servidores web se *hospeden a sí mismos*, lo que significa que puede iniciar un servidor web en su propio proceso, al contrario que un proceso que pertenece a software de servidor web dedicado, como IIS.</span><span class="sxs-lookup"><span data-stu-id="7f73e-123">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="7f73e-124">Para combinar un servicio de Service Fabric y ASP.NET, ya sea como ejecutable invitado o en una instancia de Reliable Services, debe ser capaz de iniciar ASP.NET dentro de su proceso de host de servicio.</span><span class="sxs-lookup"><span data-stu-id="7f73e-124">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="7f73e-125">El autohospedaje de ASP.NET Core lo permite.</span><span class="sxs-lookup"><span data-stu-id="7f73e-125">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="7f73e-126">Hospedaje de ASP.NET Core en una instancia de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7f73e-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="7f73e-127">Por lo general, las aplicaciones ASP.NET Core autohospedadas crean un elemento WebHost en el punto de entrada de una aplicación, como el método `static void Main()` en `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="7f73e-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="7f73e-128">En este caso, el ciclo de vida de WebHost está ligado al del proceso.</span><span class="sxs-lookup"><span data-stu-id="7f73e-128">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![Hospedaje de ASP.NET Core en un proceso][0]

<span data-ttu-id="7f73e-130">Sin embargo, el punto de entrada de la aplicación no es el lugar adecuado para crear un elemento WebHost en una instancia de Reliable Services, porque el punto de entrada de la aplicación solo se usa para registrar un tipo de servicio con el sistema en tiempo de ejecución de Service Fabric, para que pueda crear instancias de ese tipo de servicio.</span><span class="sxs-lookup"><span data-stu-id="7f73e-130">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="7f73e-131">El elemento WebHost debe crearse en una instancia de Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="7f73e-131">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="7f73e-132">Dentro del proceso de host de servicio, las instancias o réplicas de servicio pueden pasar por varios ciclos de vida.</span><span class="sxs-lookup"><span data-stu-id="7f73e-132">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="7f73e-133">Una instancia de Reliable Services se representa mediante la clase de servicio derivada de `StatelessService` o `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="7f73e-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="7f73e-134">La pila de comunicación de un servicio se encuentra en una implementación `ICommunicationListener` en la clase de servicio.</span><span class="sxs-lookup"><span data-stu-id="7f73e-134">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="7f73e-135">Los paquetes NuGet `Microsoft.ServiceFabric.Services.AspNetCore.*` contienen implementaciones de `ICommunicationListener` que inician y administran el elemento WebHost de ASP.NET Core para Kestrel o WebListener en una instancia de Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="7f73e-135">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Hospedaje de ASP.NET Core en una instancia de Reliable Services][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="7f73e-137">ICommunicationListeners en ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7f73e-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="7f73e-138">Las implementaciones de `ICommunicationListener` para Kestrel y WebListener en los paquetes NuGet `Microsoft.ServiceFabric.Services.AspNetCore.*` tienen patrones de uso parecidos pero realizan acciones ligeramente diferentes, específicas de cada servidor web.</span><span class="sxs-lookup"><span data-stu-id="7f73e-138">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="7f73e-139">Ambos agentes de escucha de comunicación proporcionan un constructor que acepta los argumentos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7f73e-139">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="7f73e-140">**`ServiceContext serviceContext`**: el objeto `ServiceContext` que contiene información sobre el servicio en ejecución.</span><span class="sxs-lookup"><span data-stu-id="7f73e-140">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="7f73e-141">**`string endpointName`**: el nombre de una configuración `Endpoint` en ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="7f73e-141">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="7f73e-142">Es en este aspecto en lo que se diferencian principalmente ambos agentes de escucha de comunicación: WebListener **requiere** una configuración `Endpoint`, pero Kestrel no.</span><span class="sxs-lookup"><span data-stu-id="7f73e-142">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="7f73e-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: expresión lambda que se implementa para crear y devolver `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="7f73e-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="7f73e-144">Esto permite configurar `IWebHost` tal como lo haría normalmente en una aplicación de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7f73e-144">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="7f73e-145">La lambda proporciona una dirección URL que se genera automáticamente en función de las opciones de integración de Service Fabric que use y la configuración `Endpoint` que proporcione.</span><span class="sxs-lookup"><span data-stu-id="7f73e-145">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="7f73e-146">Esa dirección URL se puede modificar o utilizar tal cual para iniciar el servidor web.</span><span class="sxs-lookup"><span data-stu-id="7f73e-146">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="7f73e-147">Middleware de integración de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7f73e-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="7f73e-148">El paquete NuGet `Microsoft.ServiceFabric.Services.AspNetCore` incluye el método de extensión `UseServiceFabricIntegration` en `IWebHostBuilder` que agrega middleware compatible con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7f73e-148">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="7f73e-149">Este middleware configura la implementación `ICommunicationListener` de Kestrel o WebListener para que registre una dirección URL de servicio única con el servicio de nomenclatura de Service Fabric y después valida las solicitudes de cliente para asegurarse de que los clientes se conecten al servicio adecuado.</span><span class="sxs-lookup"><span data-stu-id="7f73e-149">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="7f73e-150">Esto es necesario en un entorno de host compartido como Service Fabric, donde varias aplicaciones web se pueden ejecutar en la misma máquina física o virtual pero no utilizan nombres de host únicos, para evitar que los clientes se conecten por error al servicio incorrecto.</span><span class="sxs-lookup"><span data-stu-id="7f73e-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="7f73e-151">Este escenario se describe con más detalle en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="7f73e-151">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="7f73e-152">Un caso de identidad equivocada</span><span class="sxs-lookup"><span data-stu-id="7f73e-152">A case of mistaken identity</span></span>
<span data-ttu-id="7f73e-153">Las réplicas de servicio, con independencia del protocolo, escuchan en una combinación IP:puerto única.</span><span class="sxs-lookup"><span data-stu-id="7f73e-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="7f73e-154">Una vez que una réplica de servicio ha comenzado a escuchar en un punto de conexión IP:puerto, notifica esa dirección de punto de conexión al servicio de nomenclatura de Service Fabric, donde los clientes u otros servicios pueden detectarla.</span><span class="sxs-lookup"><span data-stu-id="7f73e-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="7f73e-155">Si los servicios utilizan puertos de aplicación asignados de forma dinámica, una réplica de servicio podría casualmente utilizar el mismo punto de conexión IP:puerto que otro servicio que se encontraba antes en la misma máquina física o virtual.</span><span class="sxs-lookup"><span data-stu-id="7f73e-155">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="7f73e-156">Esto puede hacer que un cliente se conecte por error al servicio incorrecto.</span><span class="sxs-lookup"><span data-stu-id="7f73e-156">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="7f73e-157">Esto puede ocurrir si se produce la siguiente secuencia de eventos:</span><span class="sxs-lookup"><span data-stu-id="7f73e-157">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="7f73e-158">Un servicio A escucha en 10.0.0.1:30000 a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="7f73e-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="7f73e-159">El cliente resuelve el servicio A y obtiene la dirección 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="7f73e-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="7f73e-160">El servicio A se mueve a otro nodo.</span><span class="sxs-lookup"><span data-stu-id="7f73e-160">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="7f73e-161">El servicio B se coloca en 10.0.0.1 y casualmente usa el mismo puerto 30000.</span><span class="sxs-lookup"><span data-stu-id="7f73e-161">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="7f73e-162">El cliente intenta conectarse al servicio A con la dirección 10.0.0.1:30000 en caché.</span><span class="sxs-lookup"><span data-stu-id="7f73e-162">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="7f73e-163">Ahora el cliente está conectado al servicio B sin darse cuenta de que es el servicio incorrecto.</span><span class="sxs-lookup"><span data-stu-id="7f73e-163">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="7f73e-164">Esto puede causar errores aleatoriamente que son difíciles de diagnosticar.</span><span class="sxs-lookup"><span data-stu-id="7f73e-164">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="7f73e-165">Uso de direcciones URL de servicio únicas</span><span class="sxs-lookup"><span data-stu-id="7f73e-165">Using unique service URLs</span></span>
<span data-ttu-id="7f73e-166">Para evitar esto, los servicios pueden exponer un punto de conexión ante el servicio de nomenclatura con un identificador único y después validar este último durante las solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="7f73e-166">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="7f73e-167">Se trata de una acción cooperativa entre servicios en un entorno de confianza sin inquilinos hostiles.</span><span class="sxs-lookup"><span data-stu-id="7f73e-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="7f73e-168">No proporciona autenticación de servicio segura en un entorno con inquilinos hostiles.</span><span class="sxs-lookup"><span data-stu-id="7f73e-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="7f73e-169">En un entorno de confianza, el middleware que se agrega mediante el método `UseServiceFabricIntegration` anexa automáticamente un identificador único a la dirección que se expone ante el servicio de nomenclatura y valida ese identificador con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="7f73e-169">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="7f73e-170">Si el identificador no coincide, el middleware devuelve inmediatamente una respuesta HTTP 410 Ya no existe.</span><span class="sxs-lookup"><span data-stu-id="7f73e-170">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="7f73e-171">Los servicios que utilizan un puerto asignado de forma dinámica deberían usar este middleware.</span><span class="sxs-lookup"><span data-stu-id="7f73e-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="7f73e-172">Los servicios que utilizan un puerto fijo único no tienen este problema en un entorno cooperativo.</span><span class="sxs-lookup"><span data-stu-id="7f73e-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="7f73e-173">Un puerto fijo único se utiliza normalmente para servicios orientados hacia el exterior que necesitan usar un puerto conocido al que las aplicaciones cliente puedan conectarse.</span><span class="sxs-lookup"><span data-stu-id="7f73e-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="7f73e-174">Por ejemplo, la mayoría de las aplicaciones web accesibles desde Internet usarán el puerto 80 o 443 para las conexiones del explorador web.</span><span class="sxs-lookup"><span data-stu-id="7f73e-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="7f73e-175">En este caso, el identificador único no se debe habilitar.</span><span class="sxs-lookup"><span data-stu-id="7f73e-175">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="7f73e-176">En el siguiente diagrama se muestra el flujo de la solicitud con el middleware habilitado:</span><span class="sxs-lookup"><span data-stu-id="7f73e-176">The following diagram shows the request flow with the middleware enabled:</span></span>

![Integración de ASP.NET Core de Service Fabric][2]

<span data-ttu-id="7f73e-178">Tanto las implementaciones `ICommunicationListener` de Kestrel como las de WebListener utilizan este mecanismo exactamente de la misma manera.</span><span class="sxs-lookup"><span data-stu-id="7f73e-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="7f73e-179">Aunque WebListener puede diferenciar internamente las solicitudes basadas en rutas de acceso de dirección URL únicas mediante la característica subyacente para compartir puertos *http.sys*, esa funcionalidad *no* se usa en la implementación `ICommunicationListener` de WebListener, ya que se producirían códigos de estado de error HTTP 503 y HTTP 404 en el escenario descrito antes.</span><span class="sxs-lookup"><span data-stu-id="7f73e-179">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="7f73e-180">A su vez, esto hace muy difícil que los clientes determinen la intención del error, ya que HTTP 503 y HTTP 404 ya se usan habitualmente para indicar otros errores.</span><span class="sxs-lookup"><span data-stu-id="7f73e-180">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="7f73e-181">Por lo tanto, las implementaciones `ICommunicationListener` de Kestrel y WebListener se normalizan en el middleware proporcionado por el método de extensión `UseServiceFabricIntegration` para que los clientes solo necesiten repetir la acción de resolución del punto de conexión de servicio con las respuestas HTTP 410.</span><span class="sxs-lookup"><span data-stu-id="7f73e-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="7f73e-182">WebListener en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7f73e-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="7f73e-183">WebListener puede utilizarse en una instancia de Reliable Services si se importa el paquete NuGet **Microsoft.ServiceFabric.AspNetCore.WebListener**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-183">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="7f73e-184">Este paquete contiene `WebListenerCommunicationListener`, una implementación de `ICommunicationListener`, que le permite crear un elemento WebHost de ASP.NET Core dentro de una instancia de Reliable Services con WebListener como servidor web.</span><span class="sxs-lookup"><span data-stu-id="7f73e-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="7f73e-185">WebListener se basa en la [API de servidor HTTP de Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="7f73e-185">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="7f73e-186">Utiliza el controlador de kernel *http.sys* que IIS usa para procesar solicitudes HTTP y enrutarlas a procesos que ejecutan aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="7f73e-186">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="7f73e-187">Esto permite que varios procesos en la misma máquina física o virtual hospeden aplicaciones web en el mismo puerto, eliminando la ambigüedad con un nombre de host o una ruta de acceso de dirección URL únicos.</span><span class="sxs-lookup"><span data-stu-id="7f73e-187">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="7f73e-188">Estas características son útiles en Service Fabric para hospedar varios sitios web en el mismo clúster.</span><span class="sxs-lookup"><span data-stu-id="7f73e-188">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="7f73e-189">En el siguiente diagrama se muestra cómo WebListener usa el controlador de kernel *http.sys* en Windows para compartir puertos:</span><span class="sxs-lookup"><span data-stu-id="7f73e-189">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="7f73e-191">WebListener en un servicio sin estado</span><span class="sxs-lookup"><span data-stu-id="7f73e-191">WebListener in a stateless service</span></span>
<span data-ttu-id="7f73e-192">Para usar `WebListener` en un servicio sin estado, invalide el método `CreateServiceInstanceListeners` y devuelva una instancia de `WebListenerCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7f73e-192">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="7f73e-193">WebListener en un servicio con estado</span><span class="sxs-lookup"><span data-stu-id="7f73e-193">WebListener in a stateful service</span></span>

<span data-ttu-id="7f73e-194">Actualmente, `WebListenerCommunicationListener` no está diseñado para usarse en servicios con estado a causa de las complicaciones con la característica subyacente para compartir puertos *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="7f73e-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="7f73e-195">Para más información, consulte la sección siguiente sobre la asignación dinámica de puertos con WebListener.</span><span class="sxs-lookup"><span data-stu-id="7f73e-195">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="7f73e-196">Para los servicios con estado, Kestrel es el servidor web recomendado.</span><span class="sxs-lookup"><span data-stu-id="7f73e-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="7f73e-197">Configuración del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="7f73e-197">Endpoint configuration</span></span>

<span data-ttu-id="7f73e-198">Se necesita una configuración `Endpoint` para los servidores web que usen la API de servidor HTTP de Windows, lo que incluye WebListener.</span><span class="sxs-lookup"><span data-stu-id="7f73e-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="7f73e-199">Los servidores web que usan la API de servidor HTTP de Windows deben reservar en primer lugar su dirección URL con *http.sys* (normalmente con la herramienta [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx)).</span><span class="sxs-lookup"><span data-stu-id="7f73e-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="7f73e-200">Esta acción requiere privilegios elevados de los que sus servicios carecen de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7f73e-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="7f73e-201">Las opciones "http" o "https" para la propiedad `Protocol` de la configuración `Endpoint` en *ServiceManifest.xml* se utilizan específicamente para indicar al entorno de ejecución de Service Fabric que registre una dirección URL con *http.sys* en su nombre mediante un prefijo de URL con [*comodín seguro*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="7f73e-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="7f73e-202">Por ejemplo, si se quiere reservar `http://+:80` para un servicio, debe usarse la siguiente configuración en ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="7f73e-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="7f73e-203">Y se debe pasar el nombre del punto de conexión al constructor `WebListenerCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7f73e-203">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="7f73e-204">Uso de WebListener con un puerto estático</span><span class="sxs-lookup"><span data-stu-id="7f73e-204">Use WebListener with a static port</span></span>
<span data-ttu-id="7f73e-205">Para usar un puerto estático con WebListener, proporcione el número de puerto en la configuración `Endpoint`:</span><span class="sxs-lookup"><span data-stu-id="7f73e-205">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="7f73e-206">Uso de WebListener con un puerto dinámico</span><span class="sxs-lookup"><span data-stu-id="7f73e-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="7f73e-207">Para usar un puerto asignado de forma dinámica con WebListener, omita la propiedad `Port` en la configuración `Endpoint`:</span><span class="sxs-lookup"><span data-stu-id="7f73e-207">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="7f73e-208">Tenga en cuenta que un puerto dinámico asignado por una configuración `Endpoint` proporciona solo un puerto *por cada proceso de host*.</span><span class="sxs-lookup"><span data-stu-id="7f73e-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="7f73e-209">El modelo de hospedaje actual de Service Fabric permite que varias instancias o réplicas de servicio se hospeden en el mismo proceso, lo que significa que cada una compartirá el mismo puerto cuando se asigne por medio de la configuración `Endpoint`.</span><span class="sxs-lookup"><span data-stu-id="7f73e-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="7f73e-210">Varias instancias de WebListener pueden compartir un puerto mediante la característica subyacente para compartir puertos *http.sys*, pero eso no es compatible con `WebListenerCommunicationListener` debido a las complicaciones que presenta para las solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="7f73e-210">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="7f73e-211">Para el uso de puertos dinámicos, Kestrel es el servidor web recomendado.</span><span class="sxs-lookup"><span data-stu-id="7f73e-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="7f73e-212">Kestrel en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7f73e-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="7f73e-213">Kestrel puede utilizarse en una instancia de Reliable Services si se importa el paquete NuGet **Microsoft.ServiceFabric.AspNetCore.Kestrel**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="7f73e-214">Este paquete contiene `KestrelCommunicationListener`, una implementación de `ICommunicationListener`, que le permite crear un elemento WebHost de ASP.NET Core dentro de una instancia de Reliable Services con Kestrel como servidor web.</span><span class="sxs-lookup"><span data-stu-id="7f73e-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="7f73e-215">Kestrel es un servidor web multiplataforma para ASP.NET Core basado en libuv, una biblioteca de E/S asincrónica multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="7f73e-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="7f73e-216">A diferencia de WebListener, Kestrel no utiliza un administrador centralizado de puntos de conexión como *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="7f73e-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="7f73e-217">Y, a diferencia de WebListener, Kestrel no es compatible con el uso compartido de puertos entre varios procesos.</span><span class="sxs-lookup"><span data-stu-id="7f73e-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="7f73e-218">Cada instancia de Kestrel debe usar un puerto único.</span><span class="sxs-lookup"><span data-stu-id="7f73e-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="7f73e-220">Kestrel en un servicio sin estado</span><span class="sxs-lookup"><span data-stu-id="7f73e-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="7f73e-221">Para usar `Kestrel` en un servicio sin estado, invalide el método `CreateServiceInstanceListeners` y devuelva una instancia de `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7f73e-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="7f73e-222">Kestrel en un servicio con estado</span><span class="sxs-lookup"><span data-stu-id="7f73e-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="7f73e-223">Para usar `Kestrel` en un servicio con estado, invalide el método `CreateServiceReplicaListeners` y devuelva una instancia de `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7f73e-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="7f73e-224">En este ejemplo, se proporciona una instancia singleton de `IReliableStateManager` en el contenedor de inyección de dependencias de WebHost.</span><span class="sxs-lookup"><span data-stu-id="7f73e-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="7f73e-225">Esto no es estrictamente necesario, pero sí permite usar `IReliableStateManager` y Reliable Collections en los métodos de acción de controlador MVC.</span><span class="sxs-lookup"><span data-stu-id="7f73e-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="7f73e-226">Tenga en cuenta que **no** se proporciona un nombre de configuración `Endpoint` a `KestrelCommunicationListener` en un servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="7f73e-226">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="7f73e-227">Esto se explica con más detalle en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="7f73e-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="7f73e-228">Configuración del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="7f73e-228">Endpoint configuration</span></span>
<span data-ttu-id="7f73e-229">No se requiere una configuración `Endpoint` para usar Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7f73e-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="7f73e-230">Kestrel es un servidor web independiente simple; a diferencia de WebListener (o HttpListener), no necesita una configuración `Endpoint` en *ServiceManifest.xml* porque no requiere el registro de direcciones URL antes de comenzar.</span><span class="sxs-lookup"><span data-stu-id="7f73e-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="7f73e-231">Uso de Kestrel con un puerto estático</span><span class="sxs-lookup"><span data-stu-id="7f73e-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="7f73e-232">Se puede configurar un puerto estático en la configuración `Endpoint` de ServiceManifest.xml para usarlo con Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7f73e-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="7f73e-233">Aunque esto no es estrictamente necesario, ofrece dos ventajas potenciales:</span><span class="sxs-lookup"><span data-stu-id="7f73e-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="7f73e-234">Si el puerto no se encuentra en el intervalo de puertos de la aplicación, Service Fabric lo abre a través del firewall del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="7f73e-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="7f73e-235">La dirección URL proporcionada a través de `KestrelCommunicationListener` usará este puerto.</span><span class="sxs-lookup"><span data-stu-id="7f73e-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="7f73e-236">Si se configura una instancia de `Endpoint`, se debe pasar su nombre al constructor `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7f73e-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="7f73e-237">Si no se usa una configuración `Endpoint`, se omite el nombre en el constructor `KestrelCommunicationListener`.</span><span class="sxs-lookup"><span data-stu-id="7f73e-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="7f73e-238">En este caso, se utilizará un puerto dinámico.</span><span class="sxs-lookup"><span data-stu-id="7f73e-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="7f73e-239">Consulte la siguiente sección para más información.</span><span class="sxs-lookup"><span data-stu-id="7f73e-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="7f73e-240">Uso de Kestrel con un puerto dinámico</span><span class="sxs-lookup"><span data-stu-id="7f73e-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="7f73e-241">Kestrel no puede usar la asignación automática de puertos de la configuración `Endpoint` en ServiceManifest.xml, porque la asignación automática de puertos de una configuración `Endpoint` asigna un puerto único por *cada proceso de host*, y un único proceso de host puede contener varias instancias de Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7f73e-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="7f73e-242">Puesto que Kestrel no admite el uso compartido de puertos, esto no funciona porque cada instancia de Kestrel debe abrirse en un puerto único.</span><span class="sxs-lookup"><span data-stu-id="7f73e-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="7f73e-243">Para usar la asignación dinámica de puertos con Kestrel, basta con que omita la configuración `Endpoint` en ServiceManifest.xml por completo y no pase un nombre de punto de conexión al constructor `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7f73e-243">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="7f73e-244">En esta configuración, `KestrelCommunicationListener` seleccionará automáticamente un puerto no utilizado en el intervalo de puertos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f73e-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="7f73e-245">Escenarios y configuraciones</span><span class="sxs-lookup"><span data-stu-id="7f73e-245">Scenarios and configurations</span></span>
<span data-ttu-id="7f73e-246">En esta sección se describen los siguientes escenarios y se proporciona la combinación recomendada de servidor web, configuración de puerto, opciones de integración de Service Fabric y diversas configuraciones para lograr un servicio que funcione correctamente:</span><span class="sxs-lookup"><span data-stu-id="7f73e-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="7f73e-247">Servicio sin estado de ASP.NET Core expuesto al exterior</span><span class="sxs-lookup"><span data-stu-id="7f73e-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="7f73e-248">Servicio sin estado de ASP.NET Core solo interno</span><span class="sxs-lookup"><span data-stu-id="7f73e-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="7f73e-249">Servicio con estado de ASP.NET Core solo interno</span><span class="sxs-lookup"><span data-stu-id="7f73e-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="7f73e-250">Un servicio **expuesto al exterior** es aquel que expone un punto de conexión accesible desde fuera del clúster, por lo general mediante un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="7f73e-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="7f73e-251">Un servicio **solo interno** es aquel cuyo punto de conexión solo es accesible desde dentro del clúster.</span><span class="sxs-lookup"><span data-stu-id="7f73e-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7f73e-252">Los puntos de conexión de servicio con estado generalmente no se deberían exponer a Internet.</span><span class="sxs-lookup"><span data-stu-id="7f73e-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="7f73e-253">Los clústeres que se encuentran tras equilibradores de carga que desconocen la resolución del servicio de Service Fabric, como Azure Load Balancer, no podrán exponer servicios con estado porque el equilibrador de carga no podrá localizar ni enrutar el tráfico hacia la réplica de servicio con estado adecuada.</span><span class="sxs-lookup"><span data-stu-id="7f73e-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="7f73e-254">Servicios sin estado de ASP.NET Core expuestos al exterior</span><span class="sxs-lookup"><span data-stu-id="7f73e-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="7f73e-255">WebListener es el servidor web recomendado para los servicios de front-end que exponen puntos de conexión HTTP externos orientados a Internet en Windows.</span><span class="sxs-lookup"><span data-stu-id="7f73e-255">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="7f73e-256">Proporciona mejor protección frente a ataques y admite características incompatibles con Kestrel, como la autenticación de Windows y el uso compartido de puertos.</span><span class="sxs-lookup"><span data-stu-id="7f73e-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="7f73e-257">Kestrel no se admite como servidor perimetral (orientado a Internet) en este momento.</span><span class="sxs-lookup"><span data-stu-id="7f73e-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="7f73e-258">Se debe usar un servidor proxy inverso, como IIS o Nginx, para administrar el tráfico procedente de la Internet pública.</span><span class="sxs-lookup"><span data-stu-id="7f73e-258">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="7f73e-259">Cuando se expone a Internet, un servicio sin estado debe usar un punto de conexión conocido y estable que sea accesible a través de un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="7f73e-259">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="7f73e-260">Se trata de la dirección URL que va a proporcionar a los usuarios de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f73e-260">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="7f73e-261">Se recomienda la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="7f73e-261">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="7f73e-262">**Notas**</span><span class="sxs-lookup"><span data-stu-id="7f73e-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f73e-263">Servidor web</span><span class="sxs-lookup"><span data-stu-id="7f73e-263">Web server</span></span> | <span data-ttu-id="7f73e-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="7f73e-264">WebListener</span></span> | <span data-ttu-id="7f73e-265">Si el servicio solo se expone a una red de confianza, como una intranet, se puede usar Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7f73e-265">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="7f73e-266">De lo contrario, WebListener es la opción preferida.</span><span class="sxs-lookup"><span data-stu-id="7f73e-266">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="7f73e-267">Configuración de puerto</span><span class="sxs-lookup"><span data-stu-id="7f73e-267">Port configuration</span></span> | <span data-ttu-id="7f73e-268">estática</span><span class="sxs-lookup"><span data-stu-id="7f73e-268">static</span></span> | <span data-ttu-id="7f73e-269">Se debe configurar un puerto estático conocido en la configuración `Endpoints` de ServiceManifest.xml, como 80 para HTTP o 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7f73e-269">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="7f73e-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="7f73e-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="7f73e-271">None</span><span class="sxs-lookup"><span data-stu-id="7f73e-271">None</span></span> | <span data-ttu-id="7f73e-272">La opción `ServiceFabricIntegrationOptions.None` se debe usar al configurar el middleware de integración de Service Fabric para que el servicio no intente validar solicitudes entrantes para un identificador único.</span><span class="sxs-lookup"><span data-stu-id="7f73e-272">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="7f73e-273">Los usuarios externos de la aplicación no conocerán la información de identificación única utilizada por el middleware.</span><span class="sxs-lookup"><span data-stu-id="7f73e-273">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="7f73e-274">Recuento de instancias</span><span class="sxs-lookup"><span data-stu-id="7f73e-274">Instance Count</span></span> | <span data-ttu-id="7f73e-275">-1</span><span class="sxs-lookup"><span data-stu-id="7f73e-275">-1</span></span> | <span data-ttu-id="7f73e-276">En casos de uso habituales, la configuración de recuento de instancias debe establecerse en "-1" para que una instancia esté disponible en todos los nodos que reciban tráfico de un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="7f73e-276">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="7f73e-277">Si varios servicios expuestos al exterior comparten el mismo conjunto de nodos, se debe usar una ruta de acceso de dirección URL única pero estable.</span><span class="sxs-lookup"><span data-stu-id="7f73e-277">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="7f73e-278">Para lograr esto, se puede modificar la dirección URL proporcionada al configurar IWebHost.</span><span class="sxs-lookup"><span data-stu-id="7f73e-278">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="7f73e-279">Tenga en cuenta que esto solo se aplica a WebListener.</span><span class="sxs-lookup"><span data-stu-id="7f73e-279">Note this applies to WebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="7f73e-280">Servicio sin estado de ASP.NET Core solo interno</span><span class="sxs-lookup"><span data-stu-id="7f73e-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="7f73e-281">Los servicios sin estado a los que solo se llama desde dentro del clúster deben utilizar direcciones URL únicas y puertos asignados de forma dinámica para garantizar la cooperación entre varios servicios.</span><span class="sxs-lookup"><span data-stu-id="7f73e-281">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="7f73e-282">Se recomienda la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="7f73e-282">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="7f73e-283">**Notas**</span><span class="sxs-lookup"><span data-stu-id="7f73e-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f73e-284">Servidor web</span><span class="sxs-lookup"><span data-stu-id="7f73e-284">Web server</span></span> | <span data-ttu-id="7f73e-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="7f73e-285">Kestrel</span></span> | <span data-ttu-id="7f73e-286">Aunque WebListener puede utilizarse para servicios sin estado internos, Kestrel es el servidor recomendado para permitir que varias instancias de servicio compartan un host.</span><span class="sxs-lookup"><span data-stu-id="7f73e-286">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="7f73e-287">Configuración de puerto</span><span class="sxs-lookup"><span data-stu-id="7f73e-287">Port configuration</span></span> | <span data-ttu-id="7f73e-288">asignado de forma dinámica</span><span class="sxs-lookup"><span data-stu-id="7f73e-288">dynamically assigned</span></span> | <span data-ttu-id="7f73e-289">Varias réplicas de un servicio con estado pueden compartir un proceso de host o un sistema operativo host y, por tanto, necesitarán puertos únicos.</span><span class="sxs-lookup"><span data-stu-id="7f73e-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="7f73e-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="7f73e-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="7f73e-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="7f73e-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="7f73e-292">Con la asignación dinámica de puertos, esta configuración evita el problema de identidad equivocada descrito antes.</span><span class="sxs-lookup"><span data-stu-id="7f73e-292">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="7f73e-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="7f73e-293">InstanceCount</span></span> | <span data-ttu-id="7f73e-294">cualquiera</span><span class="sxs-lookup"><span data-stu-id="7f73e-294">any</span></span> | <span data-ttu-id="7f73e-295">La configuración de recuento de instancias se puede establecer en cualquier valor necesario para hacer funcionar el servicio.</span><span class="sxs-lookup"><span data-stu-id="7f73e-295">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="7f73e-296">Servicio con estado de ASP.NET Core solo interno</span><span class="sxs-lookup"><span data-stu-id="7f73e-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="7f73e-297">Los servicios con estado a los que solo se llama desde dentro del clúster deben utilizar puertos asignados de forma dinámica para garantizar la cooperación entre varios servicios.</span><span class="sxs-lookup"><span data-stu-id="7f73e-297">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="7f73e-298">Se recomienda la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="7f73e-298">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="7f73e-299">**Notas**</span><span class="sxs-lookup"><span data-stu-id="7f73e-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f73e-300">Servidor web</span><span class="sxs-lookup"><span data-stu-id="7f73e-300">Web server</span></span> | <span data-ttu-id="7f73e-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="7f73e-301">Kestrel</span></span> | <span data-ttu-id="7f73e-302">`WebListenerCommunicationListener` no está diseñado para usarse en servicios con estado en los que las réplicas comparten un proceso de host.</span><span class="sxs-lookup"><span data-stu-id="7f73e-302">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="7f73e-303">Configuración de puerto</span><span class="sxs-lookup"><span data-stu-id="7f73e-303">Port configuration</span></span> | <span data-ttu-id="7f73e-304">asignado de forma dinámica</span><span class="sxs-lookup"><span data-stu-id="7f73e-304">dynamically assigned</span></span> | <span data-ttu-id="7f73e-305">Varias réplicas de un servicio con estado pueden compartir un proceso de host o un sistema operativo host y, por tanto, necesitarán puertos únicos.</span><span class="sxs-lookup"><span data-stu-id="7f73e-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="7f73e-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="7f73e-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="7f73e-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="7f73e-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="7f73e-308">Con la asignación dinámica de puertos, esta configuración evita el problema de identidad equivocada descrito antes.</span><span class="sxs-lookup"><span data-stu-id="7f73e-308">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7f73e-309">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f73e-309">Next steps</span></span>
[<span data-ttu-id="7f73e-310">Depurar la aplicación de Service Fabric con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f73e-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
