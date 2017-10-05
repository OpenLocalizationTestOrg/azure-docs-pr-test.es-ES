---
title: "Comunicación de servicio con la API web de ASP.NET | Microsoft Docs"
description: "Aprenda a implementar la comunicación del servicio paso a paso mediante la API web de ASP.NET con autohospedaje OWIN en la API de Reliable Services."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 73b7e1c0cb93ae7c54780a3aab837b0e5bcdb0a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="2d8bf-103">Introducción a los servicios de la API web de Microsoft Azure Service Fabric con autohospedaje OWIN</span><span class="sxs-lookup"><span data-stu-id="2d8bf-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="2d8bf-104">Azure Service Fabric delega en usted la responsabilidad de decidir cómo desea que se comuniquen sus servicios con los usuarios y entre sí.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-104">Azure Service Fabric puts the power in your hands when you're deciding how you want your services to communicate with users and with each other.</span></span> <span data-ttu-id="2d8bf-105">Este tutorial se centra en la implementación de la comunicación del servicio mediante la API web de ASP.NET con autohospedaje OWIN (Open Web Interface para .NET) en la API de Reliable Services de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="2d8bf-106">Profundizaremos más en la API de comunicación acoplable de Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-106">We'll delve deeply into the Reliable Services pluggable communication API.</span></span> <span data-ttu-id="2d8bf-107">También vamos a usar la API web en un ejemplo paso a paso para mostrar cómo configurar un agente de escucha de comunicación personalizado.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-107">We'll also use Web API in a step-by-step example to show you how to set up a custom communication listener.</span></span>

## <a name="introduction-to-web-api-in-service-fabric"></a><span data-ttu-id="2d8bf-108">Introducción a las API web de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2d8bf-108">Introduction to Web API in Service Fabric</span></span>
<span data-ttu-id="2d8bf-109">La API web de ASP.NET es un marco popular y potente que permite la creación de API HTTP sobre .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of the .NET Framework.</span></span> <span data-ttu-id="2d8bf-110">Si no está familiarizado con el marco de trabajo, consulte [Introducción a ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-110">If you're not already familiar with the framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) to learn more.</span></span>

<span data-ttu-id="2d8bf-111">La API web de Service Fabric es la misma API web de ASP.NET que conoce y ama.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-111">Web API in Service Fabric is the same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="2d8bf-112">La diferencia radica en cómo se *hospeda* la aplicación de la API web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-112">The difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="2d8bf-113">No va a utilizar Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="2d8bf-114">Para entender mejor la diferencia, dividámosla en dos partes:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-114">To better understand the difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="2d8bf-115">La aplicación de la API web (incluidos los controladores y modelos)</span><span class="sxs-lookup"><span data-stu-id="2d8bf-115">The Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="2d8bf-116">El host (el servidor web, normalmente IIS)</span><span class="sxs-lookup"><span data-stu-id="2d8bf-116">The host (the web server, usually IIS)</span></span>

<span data-ttu-id="2d8bf-117">Una aplicación de la API web no cambia.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="2d8bf-118">No difiere de las aplicaciones API web que haya realizado en el pasado y deberá poder mover simplemente la mayor parte del código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-118">It's no different from Web API applications you may have written in the past, and you should be able to simply move over most of your application code.</span></span> <span data-ttu-id="2d8bf-119">Pero si ha utilizado IIS para hospedarla, donde hospeda la aplicación puede diferir ligeramente del hospedaje que suele utilizar.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-119">But if you've been hosting on IIS, where you host the application may be a little different from what you're used to.</span></span> <span data-ttu-id="2d8bf-120">Antes de profundizar en el hospedaje, vamos a hablar sobre algo más familiar, que es la aplicación de la API web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-120">Before we get to the hosting part, let's start with something more familiar: the Web API application.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="2d8bf-121">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2d8bf-121">Create the application</span></span>
<span data-ttu-id="2d8bf-122">Empiece por crear una nueva aplicación Service Fabric, con un servicio único sin estado en Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="2d8bf-123">Si usa API web, encontrará una plantilla de Visual Studio para un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-123">A Visual Studio template for a stateless service using Web API is available to you.</span></span> <span data-ttu-id="2d8bf-124">En este tutorial, crearemos desde cero un proyecto de API web que tenga como resultado lo que se obtendría si seleccionara esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="2d8bf-125">Seleccione un proyecto de servicio sin estado en blanco para aprender a crear un proyecto de API web desde cero; también puede empezar con la plantilla de API web de servicio sin estado y seguir los pasos.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-125">Select a blank Stateless Service project to learn how to build a Web API project from scratch, or you can start with the stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="2d8bf-126">El primer paso es extraer algunos paquetes de NuGet para la API web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-126">The first step is to pull in some NuGet packages for Web API.</span></span> <span data-ttu-id="2d8bf-127">El paquete que queremos utilizar es Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-127">The package we want to use is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="2d8bf-128">Este paquete incluye todos los paquetes de la API web necesarios y los paquetes *host* .</span><span class="sxs-lookup"><span data-stu-id="2d8bf-128">This package includes all the necessary Web API packages and the *host* packages.</span></span> <span data-ttu-id="2d8bf-129">Esto será importante más adelante.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-129">This will be important later.</span></span>

<span data-ttu-id="2d8bf-130">Después de haber instalado los paquetes, podremos empezar a crear la estructura de proyecto de API web básica.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-130">After the packages have been installed, you can begin building out the basic Web API project structure.</span></span> <span data-ttu-id="2d8bf-131">Si ha utilizado la API Web, la estructura del proyecto le resultará muy familiar.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-131">If you've used Web API, the project structure should look very familiar.</span></span> <span data-ttu-id="2d8bf-132">Empiece agregando un directorio `Controllers` y un controlador de valores sencillos:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="2d8bf-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="2d8bf-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="2d8bf-134">Finalmente, agregue una clase de inicio en la raíz del proyecto para registrar el enrutamiento, los formateadores y cualquier otro programa de configuración.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-134">Next, add a Startup class at the project root to register the routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="2d8bf-135">Aquí también es donde la API web se conecta al *host*, que se revisará de nuevo más tarde.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-135">This is also where Web API plugs in to the *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="2d8bf-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="2d8bf-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="2d8bf-137">Eso es todo en lo relacionado con la parte de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-137">That's it for the application part.</span></span> <span data-ttu-id="2d8bf-138">En este momento, hemos establecido el diseño básico de proyecto de la API web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-138">At this point, we've set up just the basic Web API project layout.</span></span> <span data-ttu-id="2d8bf-139">Hasta ahora, el aspecto no debe diferir mucho de los proyectos de API web que ha creado en el pasado o de la plantilla básica de API web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-139">So far, it shouldn't look much different from Web API projects you may have written in the past or from the basic Web API template.</span></span> <span data-ttu-id="2d8bf-140">La lógica empresarial va en los controladores y los modelos como de costumbre.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-140">Your business logic goes in the controllers and models as usual.</span></span>

<span data-ttu-id="2d8bf-141">¿Ahora qué hacemos con el hospedaje para poder ejecutarlo en realidad?</span><span class="sxs-lookup"><span data-stu-id="2d8bf-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="2d8bf-142">Hospedaje de servicio</span><span class="sxs-lookup"><span data-stu-id="2d8bf-142">Service hosting</span></span>
<span data-ttu-id="2d8bf-143">En Service Fabric, el servicio se ejecuta en un *proceso de host de servicio*(un archivo ejecutable que ejecuta el código del servicio).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="2d8bf-144">Al escribir un servicio con la API de Reliable Services, el proyecto de servicio simplemente se compila en un archivo ejecutable que registra el tipo de servicio y ejecuta el código.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-144">When you write a service by using the Reliable Services API, your service project just compiles to an executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="2d8bf-145">Esto ocurre en la mayoría de los casos al escribir un servicio de Service Fabric en .NET.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="2d8bf-146">Si abre Program.cs en el proyecto de servicio sin estado, verá:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-146">When you open Program.cs in the stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="2d8bf-147">Si es sospechosamente similar al punto de entrada a una aplicación de consola, eso es porque lo es.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-147">If that looks suspiciously like the entry point to a console application, that's because it is.</span></span>

<span data-ttu-id="2d8bf-148">Los detalles adicionales sobre el proceso de host de servicio y el registro del servicio están fuera del ámbito de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-148">Further details about the service host process and service registration are beyond the scope of this article.</span></span> <span data-ttu-id="2d8bf-149">Sin embargo, es importante saber por ahora que *el código del servicio se ejecuta en su propio proceso*.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-149">But it's important to know for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="2d8bf-150">Autohospedaje de la API web con un host OWIN</span><span class="sxs-lookup"><span data-stu-id="2d8bf-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="2d8bf-151">Dado que el código de aplicación de la API web se hospeda en su propio proceso, ¿cómo se conecta a un servidor web?</span><span class="sxs-lookup"><span data-stu-id="2d8bf-151">Given that your Web API application code is hosted in its own process, how do you hook it up to a web server?</span></span> <span data-ttu-id="2d8bf-152">Escriba [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="2d8bf-153">OWIN es simplemente un contrato entre las aplicaciones web .NET y servidores web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="2d8bf-154">Tradicionalmente, cuando se usa ASP.NET (hasta MVC 5), la aplicación web se acoplaba estrechamente con IIS a través de System.Web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-154">Traditionally when ASP.NET (up to MVC 5) is used, the web application is tightly coupled to IIS through System.Web.</span></span> <span data-ttu-id="2d8bf-155">Sin embargo, la API web implementa OWIN, lo que le permite escribir una aplicación web que se separa del servidor web que la hospeda.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-155">However, Web API implements OWIN, so you can write a web application that is decoupled from the web server that hosts it.</span></span> <span data-ttu-id="2d8bf-156">Por este motivo, puede usar un servidor web OWIN de *autohospedaje* que puede iniciar en su propio proceso.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="2d8bf-157">Encaja perfectamente con el modelo de hospedaje de Service Fabric que acabamos de describir.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-157">This fits perfectly with the Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="2d8bf-158">En este artículo, usaremos Katana como el host OWIN para la aplicación API web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-158">In this article, we'll use Katana as the OWIN host for the Web API application.</span></span> <span data-ttu-id="2d8bf-159">Katana es una implementación del host OWIN de código abierto basada en [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) y la [API de servidor HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx) de Windows.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and the Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2d8bf-160">Para más información sobre Katana, vaya al [sitio de Katana](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-160">To learn more about Katana, go to the [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="2d8bf-161">Para una introducción rápida sobre cómo usar Katana para el autohospedaje de la API web, consulte [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api)(Uso de OWIN para autohospedaje de la API web de ASP.NET 2).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-161">For a quick overview of how to use Katana to self-host Web API, see [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-the-web-server"></a><span data-ttu-id="2d8bf-162">Configurar el servidor web</span><span class="sxs-lookup"><span data-stu-id="2d8bf-162">Set up the web server</span></span>
<span data-ttu-id="2d8bf-163">La API de Reliable Services ofrece un punto de entrada de comunicación en el que puede conectar pilas de comunicación para permitir a los usuarios y a los clientes conectarse al servicio:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-163">The Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients to connect to the service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="2d8bf-164">El servidor web (y las demás pilas de comunicación que utilice en el futuro, como WebSockets) debe utilizar la interfaz ICommunicationListener para integrarse correctamente en el sistema.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-164">The web server (and any other communication stack you use in the future, such as WebSockets) should use the ICommunicationListener interface to integrate correctly with the system.</span></span> <span data-ttu-id="2d8bf-165">Las razones para ello serán más evidentes en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-165">The reasons for this will become more apparent in the following steps.</span></span>

<span data-ttu-id="2d8bf-166">En primer lugar, cree una clase denominada OwinCommunicationListener que implemente ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="2d8bf-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="2d8bf-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="2d8bf-168">La interfaz de ICommunicationListener ofrece tres métodos para administrar un agente de escucha de comunicación para el servicio:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-168">The ICommunicationListener interface provides three methods to manage a communication listener for your service:</span></span>

* <span data-ttu-id="2d8bf-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-169">*OpenAsync*.</span></span> <span data-ttu-id="2d8bf-170">Empezar a escuchar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-170">Start listening for requests.</span></span>
* <span data-ttu-id="2d8bf-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-171">*CloseAsync*.</span></span> <span data-ttu-id="2d8bf-172">Dejar de escuchar las solicitudes, finalizar las solicitudes en curso y cerrar correctamente.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="2d8bf-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-173">*Abort*.</span></span> <span data-ttu-id="2d8bf-174">Cancelar todo y detener inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="2d8bf-175">Para empezar, agregue los miembros de clase privada de elementos que el agente de escucha necesite para funcionar.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-175">To get started, add private class members for things the listener will need to function.</span></span> <span data-ttu-id="2d8bf-176">Estos se inicializarán a través del constructor y se usarán más adelante cuando configure la dirección URL de escucha.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-176">These will be initialized through the constructor and used later when you set up the listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="2d8bf-177">Implementación de OpenAsync</span><span class="sxs-lookup"><span data-stu-id="2d8bf-177">Implement OpenAsync</span></span>
<span data-ttu-id="2d8bf-178">Para configurar el servidor web, necesitamos un par de datos:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-178">To set up the web server, you need two pieces of information:</span></span>

* <span data-ttu-id="2d8bf-179">*Prefijo de ruta de acceso de dirección URL*.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-179">*A URL path prefix*.</span></span> <span data-ttu-id="2d8bf-180">Aunque es opcional, es aconsejable configurar esto ahora para poder hospedar de forma segura varios servicios web en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-180">Although this is optional, it's good for you to set this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="2d8bf-181">*Un puerto*.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-181">*A port*.</span></span>

<span data-ttu-id="2d8bf-182">Antes de obtener un puerto para el servidor web, es importante comprender que Service Fabric proporciona una capa de aplicación que actúa como un búfer entre la aplicación y el sistema operativo subyacente en el que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-182">Before you get a port for the web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and the underlying operating system that it runs on.</span></span> <span data-ttu-id="2d8bf-183">Como tal, Service Fabric proporciona una manera de configurar *extremos* para los servicios.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-183">As such, Service Fabric provides a way to configure *endpoints* for your services.</span></span> <span data-ttu-id="2d8bf-184">Service Fabric garantiza que los puntos de conexión están disponibles para que el servicio los utilice.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-184">Service Fabric ensures that endpoints are available for your service to use.</span></span> <span data-ttu-id="2d8bf-185">De este modo, no tiene que configurarlos por su cuenta en el entorno de sistema operativo subyacente.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-185">This way, you don't have to configure them yourself in the underlying OS environment.</span></span> <span data-ttu-id="2d8bf-186">Puede hospedar fácilmente su aplicación de Service Fabric en diferentes entornos sin tener que realizar cambios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-186">You can easily host your Service Fabric application in different environments without having to make any changes to your application.</span></span> <span data-ttu-id="2d8bf-187">(Por ejemplo, puede hospedar la misma aplicación en Azure o en su propio centro de datos).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-187">(For example, you can host the same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="2d8bf-188">Configurar un extremo HTTP en PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="2d8bf-189">Este paso es importante porque el proceso de host de servicio se ejecuta con credenciales restringidas (servicio de red en Windows).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-189">This step is important because the service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="2d8bf-190">Esto significa que el servicio no tendrá acceso para configurar un punto de conexión HTTP por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-190">This means that your service won't have access to set up an HTTP endpoint on its own.</span></span> <span data-ttu-id="2d8bf-191">Mediante la configuración del punto de conexión, Service Fabric sabe configurar la lista de control de acceso (ACL) adecuada para la dirección URL que el servicio escuchará.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-191">By using the endpoint configuration, Service Fabric knows to set up the proper access control list (ACL) for the URL that the service will listen on.</span></span> <span data-ttu-id="2d8bf-192">Service Fabric también proporciona un lugar estándar para configurar puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-192">Service Fabric also provides a standard place to configure endpoints.</span></span>

<span data-ttu-id="2d8bf-193">De nuevo en OwinCommunicationListener.cs, puede iniciar la implementación de OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="2d8bf-194">Aquí es donde inicia el servidor web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-194">This is where you start the web server.</span></span> <span data-ttu-id="2d8bf-195">En primer lugar, obtenga la información de punto de conexión y cree la dirección URL en la que escucha el servicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-195">First, get the endpoint information and create the URL that the service will listen on.</span></span> <span data-ttu-id="2d8bf-196">La dirección URL será diferente dependiendo de si se utiliza el agente de escucha en un servicio sin estado o uno con estado.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-196">The URL will be different depending on whether the listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="2d8bf-197">Para los servicios con estado, el agente de escucha debe crear una dirección única para cada réplica de servicio con estado en la que el agente realiza la escucha.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-197">For a stateful service, the listener needs to create a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="2d8bf-198">Para los servicios sin estado, la dirección puede ser mucho más sencilla.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-198">For stateless services, the address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="2d8bf-199">Tenga en cuenta que "http://+" se utiliza aquí.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="2d8bf-200">Esto le permite asegurarse de que el servidor web está escuchando todas las direcciones disponibles, incluyendo localhost, FQDN y la dirección IP del equipo.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-200">This is to make sure that the web server is listening on all available addresses, including localhost, FQDN, and the machine IP.</span></span>

<span data-ttu-id="2d8bf-201">La implementación de OpenAsync es una de las razones más importantes por las que el servidor web (o cualquier pila de comunicación) se implementa como una interfaz ICommunicationListener en lugar de simplemente abrirse directamente desde `RunAsync()` en el servicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-201">The OpenAsync implementation is one of the most important reasons why the web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in the service.</span></span> <span data-ttu-id="2d8bf-202">El valor devuelto de OpenAsync es la dirección que está escuchando el servidor web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-202">The return value from OpenAsync is the address that the web server is listening on.</span></span> <span data-ttu-id="2d8bf-203">Cuando se devuelve esta dirección al sistema, registra la dirección con el servicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-203">When this address is returned to the system, it registers the address with the service.</span></span> <span data-ttu-id="2d8bf-204">Service Fabric proporciona una API que permite a los clientes y otros servicios pedir esta dirección por nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-204">Service Fabric provides an API that allows clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="2d8bf-205">Esto es importante porque la dirección del servicio no es estática.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-205">This is important because the service address is not static.</span></span> <span data-ttu-id="2d8bf-206">Los servicios se mueven en el clúster para fines de disponibilidad y equilibrio de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-206">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="2d8bf-207">Este es el mecanismo que permite a los clientes resolver la dirección de escucha de un servicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-207">This is the mechanism that allows clients to resolve the listening address for a service.</span></span>

<span data-ttu-id="2d8bf-208">Con eso en mente, OpenAsync inicia el servidor web y devuelve la dirección en que está escuchando.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-208">With that in mind, OpenAsync starts the web server and returns the address that it's listening on.</span></span> <span data-ttu-id="2d8bf-209">Tenga en cuenta que realiza escuchas en "http://+", pero antes de que OpenAsync devuelva la dirección, el "+" se sustituye por la dirección IP o FQDN del nodo en el que está actualmente.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-209">Note that it listens on "http://+", but before OpenAsync returns the address, the "+" is replaced with the IP or FQDN of the node it is currently on.</span></span> <span data-ttu-id="2d8bf-210">La dirección que este método devuelve es la que se registra con el sistema.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-210">The address that is returned by this method is what's registered with the system.</span></span> <span data-ttu-id="2d8bf-211">También es lo que los clientes y otros servicios ven cuando solicitan la dirección de un servicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="2d8bf-212">Para que los clientes se conecten correctamente a ella, necesitan un IP o FQDN real en la dirección.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-212">For clients to correctly connect to it, they need an actual IP or FQDN in the address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="2d8bf-213">Tenga en cuenta que esto hace referencia a la clase Inicio que se pasó a OwinCommunicationListener en el constructor.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-213">Note that this references the Startup class that was passed in to the OwinCommunicationListener in the constructor.</span></span> <span data-ttu-id="2d8bf-214">El servidor web utiliza esta instancia de inicio para arrancar la aplicación de la API web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-214">This startup instance is used by the web server to bootstrap the Web API application.</span></span>

<span data-ttu-id="2d8bf-215">La línea `ServiceEventSource.Current.Message()` aparecerá en la ventana Eventos de diagnóstico más adelante al ejecutar la aplicación para confirmar que el servidor web se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-215">The `ServiceEventSource.Current.Message()` line will appear in the Diagnostic Events window later, when you run the application to confirm that the web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="2d8bf-216">Implementación de CloseAsync y Abort</span><span class="sxs-lookup"><span data-stu-id="2d8bf-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="2d8bf-217">Por último, implemente CloseAsync y Abort para detener el servidor web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-217">Finally, implement both CloseAsync and Abort to stop the web server.</span></span> <span data-ttu-id="2d8bf-218">Es posible detener el servidor web eliminando el identificador de servidor que se creó durante la OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-218">The web server can be stopped by disposing the server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="2d8bf-219">En este ejemplo de implementación, CloseAsync y Abort simplemente detendrían el servidor web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-219">In this implementation example, both CloseAsync and Abort simply stop the web server.</span></span> <span data-ttu-id="2d8bf-220">Puede optar por realizar un apagado coordinado del servidor web de manera más correcta en CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-220">You may opt to perform a more gracefully coordinated shutdown of the web server in CloseAsync.</span></span> <span data-ttu-id="2d8bf-221">Por ejemplo, el apagado podría esperar a que finalicen las solicitudes en proceso antes de la devolución.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-221">For example, the shutdown could wait for in-flight requests to be completed before the return.</span></span>

## <a name="start-the-web-server"></a><span data-ttu-id="2d8bf-222">Iniciar el servidor web</span><span class="sxs-lookup"><span data-stu-id="2d8bf-222">Start the web server</span></span>
<span data-ttu-id="2d8bf-223">Ahora está listo para crear y devolver una instancia de OwinCommunicationListener para iniciar el servidor web.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-223">You're now ready to create and return an instance of OwinCommunicationListener to start the web server.</span></span> <span data-ttu-id="2d8bf-224">De nuevo en la clase de servicio (WebService.cs), reemplace el método `CreateServiceInstanceListeners()`:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-224">Back in the Service class (WebService.cs), override the `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="2d8bf-225">Aquí es donde la *aplicación* de la API web y el *host* OWIN se encuentran finalmente.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-225">This is where the Web API *application* and the OWIN *host* finally meet.</span></span> <span data-ttu-id="2d8bf-226">Al host (OwinCommunicationListener) se le asigna una instancia de la *aplicación* (la API web) a través del inicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-226">The host (OwinCommunicationListener) is given an instance of the *application* (Web API) via the Startup class.</span></span> <span data-ttu-id="2d8bf-227">Service Fabric administra su ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="2d8bf-228">Normalmente este mismo patrón puede ser seguido de cualquier pila de comunicación.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="2d8bf-229">Colocación de todo junto</span><span class="sxs-lookup"><span data-stu-id="2d8bf-229">Put it all together</span></span>
<span data-ttu-id="2d8bf-230">En este ejemplo, no necesita hacer nada en el método `RunAsync()` , de modo que simplemente se puede quitar la invalidación.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-230">In this example, you don't need to do anything in the `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="2d8bf-231">La implementación del servicio final debe ser muy sencilla.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-231">The final service implementation should be very simple.</span></span> <span data-ttu-id="2d8bf-232">Solo es necesario crear el agente de escucha de comunicación:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-232">It only needs to create the communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="2d8bf-233">La clase `OwinCommunicationListener` completa:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-233">The complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="2d8bf-234">Ahora que ya lo tiene todo listo, el proyecto debe presentar el aspecto de una aplicación típica de API web con los puntos de entrada de la API de Reliable Services y un host OWIN.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-234">Now that you have put all the pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="2d8bf-235">Ejecutar y conectarse a través de un explorador web</span><span class="sxs-lookup"><span data-stu-id="2d8bf-235">Run and connect through a web browser</span></span>
<span data-ttu-id="2d8bf-236">Si no lo ha hecho, [configure el entorno de desarrollo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="2d8bf-237">Ahora puede compilar e implementar su servicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-237">You can now build and deploy your service.</span></span> <span data-ttu-id="2d8bf-238">Presione **F5** en Visual Studio para compilar e implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-238">Press **F5** in Visual Studio to build and deploy the application.</span></span> <span data-ttu-id="2d8bf-239">En la ventana Eventos de diagnóstico, debe aparecer un mensaje que indica que el servidor web se ha abierto en http://localhost:8281/.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-239">In the Diagnostic Events window, you should see a message that indicates that the web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="2d8bf-240">Si el puerto ya lo ha abierto otro proceso en el equipo, puede aparecer un error aquí.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-240">If the port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="2d8bf-241">Esto indica que no se ha podido abrir el agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-241">This indicates that the listener couldn't be opened.</span></span> <span data-ttu-id="2d8bf-242">Si ese es el caso, intente utilizar un puerto diferente para configurar el punto de conexión en ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-242">If that's the case, try using a different port for the endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="2d8bf-243">Una vez que el servicio se esté ejecutando, abra un explorador y vaya a [http://localhost:8281/api/values](http://localhost:8281/api/values) para probarlo.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-243">Once the service is running, open a browser and navigate to [http://localhost:8281/api/values](http://localhost:8281/api/values) to test it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="2d8bf-244">Escala horizontal</span><span class="sxs-lookup"><span data-stu-id="2d8bf-244">Scale it out</span></span>
<span data-ttu-id="2d8bf-245">Escalar aplicaciones web sin estado normalmente supone agregar más equipos y sincronizar aplicaciones web en ellos.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-245">Scaling out stateless web apps typically means adding more machines and spinning up the web apps on them.</span></span> <span data-ttu-id="2d8bf-246">El motor de orquestaciones de Service Fabric puede hacer esto automáticamente cada vez que se agregan nuevos nodos a un clúster.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added to a cluster.</span></span> <span data-ttu-id="2d8bf-247">Al crear instancias de un servicio sin estado, puede especificar el número de instancias que desea crear.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-247">When you create instances of a stateless service, you can specify the number of instances you want to create.</span></span> <span data-ttu-id="2d8bf-248">Service Fabric coloca ese número de instancias en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-248">Service Fabric places that number of instances on nodes in the cluster.</span></span> <span data-ttu-id="2d8bf-249">Y se asegura de no crear más de una instancia en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-249">And it makes sure not to create more than one instance on any one node.</span></span> <span data-ttu-id="2d8bf-250">También puede indicar a Service Fabric que cree siempre una instancia en cada nodo mediante la especificación de **-1** en el número de instancias.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-250">You can also instruct Service Fabric to always create an instance on every node by specifying **-1** for the instance count.</span></span> <span data-ttu-id="2d8bf-251">Esto garantiza que cada vez que agregue nodos para escalar horizontalmente el clúster, se creará una instancia del servicio sin estado en los nodos nuevos.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-251">This guarantees that whenever you add nodes to scale out your cluster, an instance of your stateless service will be created on the new nodes.</span></span> <span data-ttu-id="2d8bf-252">Este valor es una propiedad de la instancia de servicio, por lo que se establece cuando se crea una instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="2d8bf-252">This value is a property of the service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="2d8bf-253">Puede hacerlo a través de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="2d8bf-254">También puede hacerlo al definir un servicio predeterminado en un proyecto de servicio sin estado de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2d8bf-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="2d8bf-255">Para más información sobre cómo crear aplicaciones e instancias de servicio, consulte [Implementar una aplicación](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="2d8bf-255">For more information on how to create application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d8bf-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d8bf-256">Next steps</span></span>
[<span data-ttu-id="2d8bf-257">Depurar la aplicación de Service Fabric con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d8bf-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

