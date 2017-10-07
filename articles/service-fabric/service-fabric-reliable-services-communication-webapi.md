---
title: "comunicación aaaService con hello ASP.NET Web API | Documentos de Microsoft"
description: "Obtenga información acerca de cómo la comunicación del servicio tooimplement paso a paso mediante el uso de Hola ASP.NET Web API con OWIN hospeda a sí mismo en hello confiable de servicios de API."
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
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="c9d0d-103">Introducción a los servicios de la API web de Microsoft Azure Service Fabric con autohospedaje OWIN</span><span class="sxs-lookup"><span data-stu-id="c9d0d-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="c9d0d-104">Azure Service Fabric aplica la potencia de hello en sus manos cuando decida cómo desea que su toocommunicate de servicios con los usuarios y entre sí.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="c9d0d-105">Este tutorial se centra en la implementación de la comunicación del servicio mediante la API web de ASP.NET con autohospedaje OWIN (Open Web Interface para .NET) en la API de Reliable Services de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="c9d0d-106">Trataremos profundamente en hello API de comunicación acoplable de servicios de confianza.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="c9d0d-107">También vamos a usar API Web en un tooshow de ejemplo paso a paso, cómo tooset un detector de comunicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="c9d0d-108">Introducción tooWeb API de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c9d0d-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="c9d0d-109">ASP.NET Web API es un marco eficaz y popular para la creación de HTTP APIs sobre Hola .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="c9d0d-110">Si no ya está familiarizado con el marco de trabajo de hello, consulte [Introducción a ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn más.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="c9d0d-111">API Web en Service Fabric es Hola mismo ASP.NET Web API conocen y adoran.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="c9d0d-112">Hello diferencia radica en cómo se *host* una aplicación de API Web.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="c9d0d-113">No va a utilizar Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="c9d0d-114">toobetter comprender la diferencia de hello, vamos a dividirla en dos partes:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="c9d0d-115">aplicación de API Web de Hello (incluidos los controladores y los modelos)</span><span class="sxs-lookup"><span data-stu-id="c9d0d-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="c9d0d-116">host de Hello (hello web server, normalmente IIS)</span><span class="sxs-lookup"><span data-stu-id="c9d0d-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="c9d0d-117">Una aplicación de la API web no cambia.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="c9d0d-118">No es distinta de las aplicaciones Web API que ha escrito en hello anterior, y debe ser toosimply pueda mover a través de la mayoría del código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="c9d0d-119">Pero si ha sido hospedaje en IIS, donde se hospeda la aplicación hello puede ser un poco diferente de lo que está acostumbrado.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="c9d0d-120">Antes de que obtenemos toohello parte de hospedaje, puede empezar con algo más conocidos: Hola aplicación Web API.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="c9d0d-121">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c9d0d-121">Create hello application</span></span>
<span data-ttu-id="c9d0d-122">Empiece por crear una nueva aplicación Service Fabric, con un servicio único sin estado en Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="c9d0d-123">Una plantilla de Visual Studio para un servicio sin estado mediante las API de Web es tooyou disponible.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="c9d0d-124">En este tutorial, crearemos desde cero un proyecto de API web que tenga como resultado lo que se obtendría si seleccionara esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="c9d0d-125">Seleccione un toolearn de proyecto de servicio sin estado en blanco cómo toobuild un proyecto de Web API desde el principio o puede empezar con el servicio sin estado Hola plantilla API Web y basta con seguir el tutorial.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="c9d0d-126">Hola primer paso es toopull en algunos paquetes de NuGet para la API Web.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="c9d0d-127">paquete de Hello queremos toouse es Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="c9d0d-128">Este paquete incluye todos los paquetes de Web API necesarios de Hola y Hola *host* paquetes.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="c9d0d-129">Esto será importante más adelante.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-129">This will be important later.</span></span>

<span data-ttu-id="c9d0d-130">Una vez instalados los paquetes de saludo, puede empezar a crear estructura de proyecto de API Web básica hello.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="c9d0d-131">Si ha utilizado la API Web, estructura de proyecto de hello deberá ser muy familiar.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="c9d0d-132">Empiece agregando un directorio `Controllers` y un controlador de valores sencillos:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="c9d0d-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="c9d0d-133">**ValuesController.cs**</span></span>

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

<span data-ttu-id="c9d0d-134">A continuación, agregue una clase de inicio Hola proyecto raíz tooregister Hola enrutamiento, los formateadores y cualquier otro programa de instalación de configuración.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="c9d0d-135">También es donde se conecta la API Web en toohello *host*, que se revisan de nuevo más tarde.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="c9d0d-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="c9d0d-136">**Startup.cs**</span></span>

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

<span data-ttu-id="c9d0d-137">Esto es todo por parte de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-137">That's it for hello application part.</span></span> <span data-ttu-id="c9d0d-138">En este punto, hemos configurado solo hello Web API proyecto diseño básico.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="c9d0d-139">Hasta ahora, no debería buscar mucho diferente de proyectos API Web que ha escrito en los último Hola o de plantilla de API Web básica hello.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="c9d0d-140">La lógica de negocios va en controladores de Hola y modelos como de costumbre.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="c9d0d-141">¿Ahora qué hacemos con el hospedaje para poder ejecutarlo en realidad?</span><span class="sxs-lookup"><span data-stu-id="c9d0d-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="c9d0d-142">Hospedaje de servicio</span><span class="sxs-lookup"><span data-stu-id="c9d0d-142">Service hosting</span></span>
<span data-ttu-id="c9d0d-143">En Service Fabric, el servicio se ejecuta en un *proceso de host de servicio*(un archivo ejecutable que ejecuta el código del servicio).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="c9d0d-144">Al escribir un servicio mediante el uso de hello confiable de servicios de API, el proyecto de servicio solo compila tooan archivo ejecutable que registra el tipo de servicio y se ejecuta el código.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="c9d0d-145">Esto ocurre en la mayoría de los casos al escribir un servicio de Service Fabric en .NET.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="c9d0d-146">Cuando abra Program.cs en el proyecto de servicio sin estado hello, verá:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

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

<span data-ttu-id="c9d0d-147">Si se ve es sospechosamente como aplicación de consola de tooa de punto de entrada de hello, que es porque es.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="c9d0d-148">Hola a más detalles sobre el proceso de host de servicio y registro del servicio están más allá del ámbito de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="c9d0d-149">Pero es importante tooknow para ahora que *se ejecuta el código de servicio en su propio proceso*.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="c9d0d-150">Autohospedaje de la API web con un host OWIN</span><span class="sxs-lookup"><span data-stu-id="c9d0d-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="c9d0d-151">¿Dado que el código de aplicación de API Web se hospeda en su propio proceso, cómo enlazó, servidor web de tooa?</span><span class="sxs-lookup"><span data-stu-id="c9d0d-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="c9d0d-152">Escriba [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="c9d0d-153">OWIN es simplemente un contrato entre las aplicaciones web .NET y servidores web.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="c9d0d-154">Tradicionalmente cuando se usa ASP.NET (arriba tooMVC 5), aplicación web de hello es tooIIS estrechamente acopladas a través de System.Web.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="c9d0d-155">Sin embargo, la API Web implementa OWIN, por lo que puede escribir una aplicación web que se separa del servidor web de Hola que lo hospeda.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="c9d0d-156">Por este motivo, puede usar un servidor web OWIN de *autohospedaje* que puede iniciar en su propio proceso.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="c9d0d-157">Esto se adapta perfectamente con los modelos de hospedaje de Service Fabric de Hola que acabamos de describir.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="c9d0d-158">En este artículo, vamos a usar Katana como host de hello OWIN para hello aplicación Web API.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="c9d0d-159">Katana es una implementación del host OWIN de código abierto basada en [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) y Hola Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c9d0d-160">más información acerca de Katana, vaya toohello toolearn [Katana sitio](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="c9d0d-161">Para obtener una introducción rápida de cómo toouse Katana tooself host Web API, consulte [OWIN Use tooSelf Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="c9d0d-162">Configurar el servidor web de Hola</span><span class="sxs-lookup"><span data-stu-id="c9d0d-162">Set up hello web server</span></span>
<span data-ttu-id="c9d0d-163">Hola confiable de servicios de API proporciona un punto de entrada de comunicación que se pueden conectar en pilas de comunicación que permiten a los usuarios y el servicio de toohello de tooconnect de clientes:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="c9d0d-164">servidor web de Hello (y cualquier otra pila de comunicación que utilizar Hola futura, por ejemplo, WebSockets) deben usar hello ICommunicationListener interfaz toointegrate correctamente con el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="c9d0d-165">los motivos Hola serán más evidentes Hola siguiendo los pasos.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="c9d0d-166">En primer lugar, cree una clase denominada OwinCommunicationListener que implemente ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="c9d0d-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="c9d0d-167">**OwinCommunicationListener.cs**</span></span>

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

<span data-ttu-id="c9d0d-168">interfaz ICommunicationListener de Hello proporciona tres toomanage métodos un agente de escucha de comunicación para el servicio:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="c9d0d-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-169">*OpenAsync*.</span></span> <span data-ttu-id="c9d0d-170">Empezar a escuchar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-170">Start listening for requests.</span></span>
* <span data-ttu-id="c9d0d-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-171">*CloseAsync*.</span></span> <span data-ttu-id="c9d0d-172">Dejar de escuchar las solicitudes, finalizar las solicitudes en curso y cerrar correctamente.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="c9d0d-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-173">*Abort*.</span></span> <span data-ttu-id="c9d0d-174">Cancelar todo y detener inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="c9d0d-175">tooget iniciado, agregue los miembros de clase privada para el agente de escucha de cosas Hola tendrá toofunction.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="c9d0d-176">Estos se inicializarán a través del constructor de Hola y utilizar más adelante cuando configure Hola escuchando la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

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

## <a name="implement-openasync"></a><span data-ttu-id="c9d0d-177">Implementación de OpenAsync</span><span class="sxs-lookup"><span data-stu-id="c9d0d-177">Implement OpenAsync</span></span>
<span data-ttu-id="c9d0d-178">tooset de servidor web de hello, necesita dos fragmentos de información:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="c9d0d-179">*Prefijo de ruta de acceso de dirección URL*.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-179">*A URL path prefix*.</span></span> <span data-ttu-id="c9d0d-180">Aunque esto es opcional, es conveniente para tooset esta una copia de seguridad ahora para que puede hospedar varios servicios web con seguridad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="c9d0d-181">*Un puerto*.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-181">*A port*.</span></span>

<span data-ttu-id="c9d0d-182">Antes de obtener un puerto de servidor web de hello, es importante que comprenda que Service Fabric proporciona una capa de aplicación que actúa como un búfer entre la aplicación y el sistema operativo subyacente Hola donde se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="c9d0d-183">Por lo tanto, Service Fabric proporciona una manera tooconfigure *extremos* para los servicios.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="c9d0d-184">Service Fabric garantiza que los puntos de conexión están disponibles para su toouse de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="c9d0d-185">De esta manera, no tiene tooconfigure a usted mismo en hello subyacente de entorno de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="c9d0d-186">Fácilmente puede hospedar la aplicación de Service Fabric en diferentes entornos sin necesidad de toomake cualquier aplicación de tooyour de cambios.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="c9d0d-187">(Por ejemplo, puede hospedar Hola la misma aplicación en Azure o en su propio centro de datos.)</span><span class="sxs-lookup"><span data-stu-id="c9d0d-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="c9d0d-188">Configurar un extremo HTTP en PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="c9d0d-189">Este paso es importante porque el proceso de host del servicio de Hola se ejecuta con credenciales restringidas (servicio de red en Windows).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="c9d0d-190">Esto significa que el servicio no tendrá acceso tooset un extremo HTTP por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="c9d0d-191">Mediante la configuración de punto de conexión de hello, Service Fabric sabe tooset una lista de control de acceso apropiado de hello (ACL) para hello escuche en direcciones URL que Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="c9d0d-192">Service Fabric también proporciona un lugar estándar tooconfigure extremos.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="c9d0d-193">De nuevo en OwinCommunicationListener.cs, puede iniciar la implementación de OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="c9d0d-194">Esto es donde se inicia el servidor de web de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-194">This is where you start hello web server.</span></span> <span data-ttu-id="c9d0d-195">En primer lugar, obtener información de punto de conexión de Hola y crear dirección URL de Hola que escucha en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="c9d0d-196">dirección URL de Hello será diferente dependiendo de si se utiliza el agente de escucha de hello en un servicio sin estado o un servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="c9d0d-197">Para un servicio con estado, el agente de escucha de hello debe toocreate un nombre único para cada réplica de servicio con estado realiza escuchas en dirección.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="c9d0d-198">Para los servicios sin estado, dirección de hello puede ser mucho más fácil.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-198">For stateless services, hello address can be much simpler.</span></span> 

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

<span data-ttu-id="c9d0d-199">Tenga en cuenta que "http://+" se utiliza aquí.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="c9d0d-200">Se trata de toomake seguro de que el servidor web Hola está escuchando en todas las direcciones disponibles, incluyendo localhost, el FQDN y la dirección IP del equipo Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="c9d0d-201">Hello OpenAsync implementación es uno de los motivos más importantes de hello ¿por qué servidor web de hello (o cualquier pila de comunicación) se implementa como un ICommunicationListener, en lugar de simplemente tener abre directamente desde `RunAsync()` en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="c9d0d-202">valor devuelto de Hola de OpenAsync es dirección Hola Hola servidor web está escuchando en.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="c9d0d-203">Cuando esta dirección se devuelve toohello system, registra dirección Hola con servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="c9d0d-204">Tejido de servicio proporciona una API que permite a los clientes y otro servicios toothen solicitar esta dirección por nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="c9d0d-205">Esto es importante porque la dirección de servicio de hello no es estático.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="c9d0d-206">Servicios se mueven en clúster de Hola para fines de disponibilidad y equilibrio de recursos.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="c9d0d-207">Este es el mecanismo de Hola que permite a los clientes hello tooresolve dirección para un servicio de escucha.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="c9d0d-208">Con esto en mente, OpenAsync inicia el servidor web de Hola y devuelve la dirección de Hola que escuchan en.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="c9d0d-209">Tenga en cuenta que realiza escuchas en "http://+", pero antes de que OpenAsync devuelve la dirección de hello, Hola "+" se reemplaza con hello IP o FQDN del nodo de hello está actualmente en.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="c9d0d-210">dirección de Hello devuelto por este método es lo que está registrado con el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="c9d0d-211">También es lo que los clientes y otros servicios ven cuando solicitan la dirección de un servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="c9d0d-212">Para los clientes toocorrectly conectar tooit, que necesitan una IP o FQDN real de dirección de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

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
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="c9d0d-213">Tenga en cuenta que esto hace referencia a clase de inicio de Hola que se pasó en toohello OwinCommunicationListener en el constructor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="c9d0d-214">Saludos toobootstrap aplicación de API Web del servidor de web de hello usa esta instancia de inicio.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="c9d0d-215">Hola `ServiceEventSource.Current.Message()` línea aparecerá en la ventana de eventos de diagnóstico de hello más adelante, al ejecutar ese servidor web de Hola Hola aplicación tooconfirm ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="c9d0d-216">Implementación de CloseAsync y Abort</span><span class="sxs-lookup"><span data-stu-id="c9d0d-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="c9d0d-217">Por último, implemente CloseAsync y anulación del servidor web de toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="c9d0d-218">servidor web de Hola se puede detener eliminando identificador de servidor de Hola que se creó durante la OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

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

<span data-ttu-id="c9d0d-219">En este ejemplo de implementación, CloseAsync y Abort simplemente detendrán servidor web de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="c9d0d-220">Puede elegir un apagado más correctamente coordinado de servidor web de hello en CloseAsync tooperform.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="c9d0d-221">Por ejemplo, apagado Hola podría esperar toobe solicitudes sobre la marcha completada antes de devolver Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="c9d0d-222">Inicie hello web server</span><span class="sxs-lookup"><span data-stu-id="c9d0d-222">Start hello web server</span></span>
<span data-ttu-id="c9d0d-223">Ahora está listo toocreate y devolver una instancia de servidor web de OwinCommunicationListener toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="c9d0d-224">Nuevo en hello clase de servicio (WebService.cs), invalidar hello `CreateServiceInstanceListeners()` método:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

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

<span data-ttu-id="c9d0d-225">Esto es donde Hola API Web *aplicación* y Hola OWIN *host* finalmente cumplir.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="c9d0d-226">host de Hello (OwinCommunicationListener) tiene una instancia del programa Hola a *aplicación* (API de Web) a través de la clase de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="c9d0d-227">Service Fabric administra su ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="c9d0d-228">Normalmente este mismo patrón puede ser seguido de cualquier pila de comunicación.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="c9d0d-229">Colocación de todo junto</span><span class="sxs-lookup"><span data-stu-id="c9d0d-229">Put it all together</span></span>
<span data-ttu-id="c9d0d-230">En este ejemplo, no es necesario toodo cualquier dato de hello `RunAsync()` método, por lo que la invalidación de simplemente puede eliminarse.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="c9d0d-231">implementación del servicio final de Hello debe ser muy simple.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="c9d0d-232">Solo necesita el agente de escucha de toocreate Hola comunicación:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-232">It only needs toocreate hello communication listener:</span></span>

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

<span data-ttu-id="c9d0d-233">Hola completa `OwinCommunicationListener` clase:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-233">hello complete `OwinCommunicationListener` class:</span></span>

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
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

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

<span data-ttu-id="c9d0d-234">Ahora que ha colocado todas las piezas de hello en su lugar, el proyecto debería parecerse a una aplicación de API Web típica con puntos de entrada de API de servicios de confianza y un host OWIN.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="c9d0d-235">Ejecutar y conectarse a través de un explorador web</span><span class="sxs-lookup"><span data-stu-id="c9d0d-235">Run and connect through a web browser</span></span>
<span data-ttu-id="c9d0d-236">Si no lo ha hecho, [configure el entorno de desarrollo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="c9d0d-237">Ahora puede compilar e implementar su servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-237">You can now build and deploy your service.</span></span> <span data-ttu-id="c9d0d-238">Presione **F5** en Visual Studio toobuild e implementar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="c9d0d-239">En la ventana de eventos de diagnóstico de hello, verá un mensaje que indica que el servidor web Hola abierto en http://localhost:8281 /.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="c9d0d-240">Si ya se ha abierto el puerto de Hola por otro proceso en el equipo, verá un error aquí.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="c9d0d-241">Esto indica que no se pudo abrir ese agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="c9d0d-242">Si ese es el caso de hello, pruebe a usar un puerto diferente para la configuración de punto de conexión de hello en ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="c9d0d-243">Una vez que se está ejecutando el servicio de hello, abra un explorador y navegue demasiado[http://localhost:8281/api/valores](http://localhost:8281/api/values) tootest lo.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="c9d0d-244">Escala horizontal</span><span class="sxs-lookup"><span data-stu-id="c9d0d-244">Scale it out</span></span>
<span data-ttu-id="c9d0d-245">Ampliación de aplicaciones web sin estado normalmente significa agregar más máquinas y girando hello las aplicaciones web en ellos.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="c9d0d-246">Motor de orquestaciones del tejido de servicio puede hacerlo automáticamente cada vez que se agregan nuevos nodos clúster tooa.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="c9d0d-247">Al crear instancias de un servicio sin estado, puede especificar el número de Hola de instancias que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="c9d0d-248">Service Fabric coloca ese número de instancias en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="c9d0d-249">Y se asegura de que no toocreate más de una instancia en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="c9d0d-250">También puede indicar al Service Fabric tooalways crear una instancia en cada nodo mediante la especificación de **-1** para recuento de instancias de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="c9d0d-251">Esto garantiza que, siempre que agregue nodos tooscale fuera del clúster, se creará una instancia del servicio sin estado en nodos nuevos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="c9d0d-252">Este valor es una propiedad de instancia de servicio de hello, por lo que se establece cuando se crea una instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9d0d-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="c9d0d-253">Puede hacerlo a través de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="c9d0d-254">También puede hacerlo al definir un servicio predeterminado en un proyecto de servicio sin estado de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c9d0d-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="c9d0d-255">Para obtener más información sobre cómo toocreate aplicación y las instancias del servicio, vea [implementar una aplicación](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c9d0d-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9d0d-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9d0d-256">Next steps</span></span>
[<span data-ttu-id="c9d0d-257">Depurar la aplicación de Service Fabric con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9d0d-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

