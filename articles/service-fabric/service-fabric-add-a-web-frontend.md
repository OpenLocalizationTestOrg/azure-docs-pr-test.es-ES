---
title: "aaaCreate un front-end web para la aplicación de Azure Service Fabric mediante ASP.NET Core | Documentos de Microsoft"
description: "Exponer su web toohello de aplicación de Service Fabric mediante el uso de un proyecto de ASP.NET Core y la comunicación entre servicio a través de comunicación remota de servicio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="be687-103">Creación de un front-end de servicio web para una aplicación mediante ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="be687-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="be687-104">De forma predeterminada, servicios de Azure Service Fabric no proporcionan un sitio web toohello de interfaz pública.</span><span class="sxs-lookup"><span data-stu-id="be687-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="be687-105">tooexpose los clientes tooHTTP de funcionalidad de la aplicación, deberá toocreate un sitio web tooact como un punto de entrada del proyecto y, a continuación, comunicarse desde ahí tooyour servicios individuales.</span><span class="sxs-lookup"><span data-stu-id="be687-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="be687-106">En este tutorial, se retomar donde se dejó en hello [crear su primera aplicación en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial y agregar un servicio web de ASP.NET Core delante de servicio de contador con estado Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="be687-107">Si aún no lo ha hecho, debe revisar primero ese tutorial.</span><span class="sxs-lookup"><span data-stu-id="be687-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="be687-108">Configuración del entorno para ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="be687-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="be687-109">Necesita Visual Studio de 2017 toofollow junto con este tutorial.</span><span class="sxs-lookup"><span data-stu-id="be687-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="be687-110">Cualquier edición servirá.</span><span class="sxs-lookup"><span data-stu-id="be687-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="be687-111">Instalación de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="be687-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="be687-112">las aplicaciones de ASP.NET Core Service Fabric toodevelop, debe tener Hola siguiendo las cargas de trabajo instalados:</span><span class="sxs-lookup"><span data-stu-id="be687-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="be687-113">**Desarrollo de Azure** (en *Web y nube*)</span><span class="sxs-lookup"><span data-stu-id="be687-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="be687-114">**ASP.NET y desarrollo web** (en *Web y nube*)</span><span class="sxs-lookup"><span data-stu-id="be687-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="be687-115">**Desarrollo multiplataforma de .NET Core** (en *Otros conjuntos de herramientas*)</span><span class="sxs-lookup"><span data-stu-id="be687-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="be687-116">Hello herramientas de .NET Core para Visual Studio 2015 ya no se actualizan, no obstante, si todavía se usa Visual Studio 2015, necesita toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) instalado.</span><span class="sxs-lookup"><span data-stu-id="be687-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="be687-117">Agregar una aplicación de ASP.NET Core servicio tooyour</span><span class="sxs-lookup"><span data-stu-id="be687-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="be687-118">Núcleo de ASP.NET es un marco de desarrollo web ligera y multiplataforma que puede usar la interfaz de usuario de web moderna toocreate y las API web.</span><span class="sxs-lookup"><span data-stu-id="be687-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="be687-119">Vamos a agregar una aplicación existente de ASP.NET Web API proyecto tooour.</span><span class="sxs-lookup"><span data-stu-id="be687-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="be687-120">En el Explorador de soluciones, haga clic en **servicios** en Hola proyecto de aplicación y elija **Agregar > nuevo servicio de Fabric**.</span><span class="sxs-lookup"><span data-stu-id="be687-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Agregar una nueva aplicación existente de tooan de servicio][vs-add-new-service]
2. <span data-ttu-id="be687-122">En hello **crear un servicio** página, elija **ASP.NET Core** y asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="be687-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Elegir el servicio web ASP.NET en el cuadro de diálogo de hello nuevo servicio][vs-new-service-dialog]

3. <span data-ttu-id="be687-124">página siguiente de Hello proporciona un conjunto de ASP.NET Core plantillas de proyecto.</span><span class="sxs-lookup"><span data-stu-id="be687-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="be687-125">Tenga en cuenta que estos se Hola mismo opciones que vería si crea un proyecto de ASP.NET Core fuera de una aplicación de Service Fabric, con una pequeña cantidad de código adicional tooregister Hola servicio con el tiempo de ejecución de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="be687-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="be687-126">Para este tutorial, elija **API Web**.</span><span class="sxs-lookup"><span data-stu-id="be687-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="be687-127">Sin embargo, puede aplicar Hola mismo conceptos toobuilding una aplicación web completa.</span><span class="sxs-lookup"><span data-stu-id="be687-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![Elección del tipo de proyecto ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="be687-129">Una vez creado el proyecto API web, tendrá dos servicios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="be687-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="be687-130">Mientras continúa toobuild con la aplicación, puede agregar más servicios en hello exactamente igual.</span><span class="sxs-lookup"><span data-stu-id="be687-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="be687-131">Cada uno puede tener versiones y actualizaciones independientes.</span><span class="sxs-lookup"><span data-stu-id="be687-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="be687-132">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="be687-132">Run hello application</span></span>
<span data-ttu-id="be687-133">tooget una idea de lo que hemos hecho, vamos a implementar la nueva aplicación de Hola y realice un vistazo en el comportamiento predeterminado de Hola que Hola plantilla API Web de ASP.NET Core proporciona.</span><span class="sxs-lookup"><span data-stu-id="be687-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="be687-134">Presione F5 en Visual Studio toodebug Hola app.</span><span class="sxs-lookup"><span data-stu-id="be687-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="be687-135">Cuando se completa la implementación, Visual Studio inicia una raíz de toohello del explorador de hello servicio ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="be687-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="be687-136">plantilla de API Web de ASP.NET Core Hello no proporciona comportamiento predeterminado para la raíz de hello, por lo que debería ver un error 404 en explorador Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="be687-137">Agregar `/api/values` toohello ubicación en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="be687-138">Esto invoca hello `Get` método en hello ValuesController en la plantilla de la API Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="be687-139">Devuelve respuesta predeterminada de hello proporcionada por la plantilla de hello: una matriz JSON que contiene dos cadenas:</span><span class="sxs-lookup"><span data-stu-id="be687-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![Valores predeterminados devueltos desde la plantilla API web de ASP.NET Core][browser-aspnet-template-values]
   
    <span data-ttu-id="be687-141">Extremo de Hola de tutorial de hello, esta página mostrará valor más reciente del contador Hola de nuestro servicio con estado en lugar de hello cadenas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="be687-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="be687-142">Conectar servicios de Hola</span><span class="sxs-lookup"><span data-stu-id="be687-142">Connect hello services</span></span>
<span data-ttu-id="be687-143">Service Fabric proporciona una flexibilidad completa en el modo de comunicación con los servicios confiables.</span><span class="sxs-lookup"><span data-stu-id="be687-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="be687-144">En una sola aplicación, podría tener servicios que son accesibles a través de TCP, servicios que son accesibles a través de una API de REST de HTTP y servicios que son accesibles a través de sockets web.</span><span class="sxs-lookup"><span data-stu-id="be687-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="be687-145">Para obtener información sobre opciones de hello disponibles y los inconvenientes de hello, consulte [comunicarse con servicios](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="be687-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="be687-146">En este tutorial, usamos [comunicación remota de servicio de Service Fabric](service-fabric-reliable-services-communication-remoting.md), proporcionado en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="be687-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="be687-147">Hola enfoque de comunicación remota de servicio (modelada en llamadas a procedimiento remoto o RPC), se define una interfaz tooact como contrato público de hello para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="be687-148">A continuación, usar ese toogenerate interfaz una clase de proxy para interactuar con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="be687-149">Crear la interfaz de comunicación remota de Hola</span><span class="sxs-lookup"><span data-stu-id="be687-149">Create hello remoting interface</span></span>
<span data-ttu-id="be687-150">Empecemos creando Hola interfaz tooact como Hola contrato entre el servicio con estado de Hola y otros servicios, en este caso Hola proyecto web de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="be687-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="be687-151">Esta interfaz debe estar compartida por todos los servicios que usan llamadas a RPC toomake, por lo que vamos a crear en su propio proyecto de biblioteca de clases.</span><span class="sxs-lookup"><span data-stu-id="be687-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="be687-152">En el Explorador de soluciones, haga clic con el botón derecho en la solución y seleccione **Agregue** > **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="be687-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="be687-153">Elija hello **Visual C#** entrada Hola dejado el panel de navegación y, a continuación, seleccione hello **biblioteca de clases** plantilla.</span><span class="sxs-lookup"><span data-stu-id="be687-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="be687-154">Asegurarse de esa versión de .NET Framework Hola se establece demasiado**4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="be687-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![Creación de un proyecto de interfaz para el servicio con estado][vs-add-class-library-project]

3. <span data-ttu-id="be687-156">Instalar hello **Microsoft.ServiceFabric.Services.Remoting** paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="be687-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="be687-157">Busque **Microsoft.ServiceFabric.Services.Remoting** en hello NuGet paquete Administrador e instalarlo para todos los proyectos de solución de Hola que usar el servicio de acceso remoto, incluidos:</span><span class="sxs-lookup"><span data-stu-id="be687-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="be687-158">proyecto de biblioteca de clases de Hola que contiene la interfaz de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="be687-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="be687-159">proyecto de servicio con estado Hola</span><span class="sxs-lookup"><span data-stu-id="be687-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="be687-160">Hola proyecto de servicio web de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="be687-160">hello ASP.NET Core web service project</span></span>
   
    ![Agregando el paquete NuGet de servicios Hola][vs-services-nuget-package]

4. <span data-ttu-id="be687-162">En la biblioteca de clases de hello, crear una interfaz con un único método, `GetCountAsync`, y extender la interfaz de Hola desde `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="be687-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="be687-163">interfaz de comunicación remota de Hello debe derivar de esta interfaz tooindicate que es una interfaz de comunicación remota de servicio.</span><span class="sxs-lookup"><span data-stu-id="be687-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="be687-164">Implementar interfaz hello en el servicio con estado</span><span class="sxs-lookup"><span data-stu-id="be687-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="be687-165">Ahora que hemos definido interfaz hello, necesitamos tooimplement en servicio con estado Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="be687-166">En el servicio con estado, agregue un proyecto de biblioteca de clases de toohello de referencia que contiene la interfaz de Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![Agregar un proyecto de biblioteca de clases de toohello de referencia de servicio con estado Hola][vs-add-class-library-reference]
2. <span data-ttu-id="be687-168">Busque Hola clase que hereda de `StatefulService`, como `MyStatefulService`y ampliarlo hello tooimplement `ICounter` interfaz.</span><span class="sxs-lookup"><span data-stu-id="be687-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="be687-169">Ahora implemente Hola único método que se define en hello `ICounter` interfaz, `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="be687-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="be687-170">Exponer Hola servicio con estado con un agente de escucha de comunicación remota de servicio</span><span class="sxs-lookup"><span data-stu-id="be687-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="be687-171">Con hello `ICounter` interfaz implementada, el paso final de hello es canal de comunicación de comunicación remota de servicio de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="be687-172">Para los servicios con estado, Service Fabric proporciona un método reemplazable denominado " `CreateServiceReplicaListeners`".</span><span class="sxs-lookup"><span data-stu-id="be687-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="be687-173">Con este método, puede especificar una o varias escuchas de comunicación, según tipo hello de comunicación que necesite tooenable para el servicio.</span><span class="sxs-lookup"><span data-stu-id="be687-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="be687-174">se llama a Hola método equivalente para abrir los servicios de toostateless de canal de comunicación `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="be687-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="be687-175">En este caso, reemplazamos Hola existente `CreateServiceReplicaListeners` método y proporcionar una instancia de `ServiceRemotingListener`, que crea un punto de conexión RPC que sea accesible desde los clientes a través de `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="be687-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="be687-176">Hola `CreateServiceRemotingListener` método de extensión en hello `IService` interfaz permite tooeasily crear un `ServiceRemotingListener` con todos los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="be687-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="be687-177">toouse este método de extensión, asegúrese de tener hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` espacio de nombres importado.</span><span class="sxs-lookup"><span data-stu-id="be687-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="be687-178">Utilizar hello ServiceProxy clase toointeract con el servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="be687-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="be687-179">Nuestro servicio con estado ahora está listo tooreceive tráfico de otros servicios a través de RPC.</span><span class="sxs-lookup"><span data-stu-id="be687-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="be687-180">Por lo que todo lo que sigue siendo consiste en Agregar Hola código toocommunicate con él de hello servicio web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="be687-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="be687-181">En el proyecto ASP.NET, agregue una biblioteca de clases de toohello de referencia que contiene Hola `ICounter` interfaz.</span><span class="sxs-lookup"><span data-stu-id="be687-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="be687-182">Antes de que se ha agregado hello **Microsoft.ServiceFabric.Services.Remoting** proyecto ASP.NET de toohello de paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="be687-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="be687-183">Este paquete proporciona hello `ServiceProxy` clase que usar toomake RPC llama toohello de servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="be687-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="be687-184">Asegúrese de que este paquete de NuGet está instalado en el proyecto de servicio web de ASP.NET Core Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="be687-185">Hola **controladores** carpeta, abra hello `ValuesController` clase.</span><span class="sxs-lookup"><span data-stu-id="be687-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="be687-186">Tenga en cuenta que hello `Get` método actualmente solo devuelve una matriz de cadenas codificadas de forma rígida de "value1" y "value2", que coincide con lo que vimos anteriormente en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="be687-187">Reemplace esta implementación con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="be687-187">Replace this implementation with hello following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="be687-188">primera línea de código de Hello es clave Hola uno.</span><span class="sxs-lookup"><span data-stu-id="be687-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="be687-189">toocreate Hola ICounter proxy toohello servicio con estado, deberá tooprovide dos piezas de información: nombre de servicio de Hola hello y el Id. de partición.</span><span class="sxs-lookup"><span data-stu-id="be687-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="be687-190">Puede usar servicios con estado de partición tooscale dividiendo su estado en sectores de almacenamiento diferentes, en función de una clave que defina, por ejemplo, un identificador de cliente o un código postal.</span><span class="sxs-lookup"><span data-stu-id="be687-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="be687-191">En nuestra aplicación trivial, servicio con estado de hello sólo tiene una partición, por lo que no importa la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="be687-192">Cualquier tecla proporcionada por usted llevará toohello misma partición.</span><span class="sxs-lookup"><span data-stu-id="be687-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="be687-193">toolearn más información acerca de la creación de particiones de servicios, consulte [cómo toopartition servicios confiables de tejido de servicio](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="be687-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="be687-194">nombre del servicio Hello es un URI de tejido de formulario de hello: /&lt;$application_name&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="be687-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="be687-195">Con estos dos fragmentos de información, Service Fabric puede identificar máquina Hola que se deben enviar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="be687-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="be687-196">Hola `ServiceProxy` clase controla también perfectamente caso de hello donde se produce un error en la máquina de Hola que aloja la partición de servicio con estado de Hola y otra máquina debe ser promocionada tootake su lugar.</span><span class="sxs-lookup"><span data-stu-id="be687-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="be687-197">Esta abstracción permite escribir Hola toodeal de código de cliente con otros servicios de proceso mucho más sencillas.</span><span class="sxs-lookup"><span data-stu-id="be687-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="be687-198">Una vez que tenemos proxy hello, basta con invocar hello `GetCountAsync` método y devuelva su resultado.</span><span class="sxs-lookup"><span data-stu-id="be687-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="be687-199">Presione F5 nuevo toorun Hola modificó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="be687-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="be687-200">Como antes, Visual Studio inicia automáticamente Hola explorador toohello raíz Hola proyecto web.</span><span class="sxs-lookup"><span data-stu-id="be687-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="be687-201">Agregar ruta de acceso de "api/valores" hello y debería ver el valor de contador actual de hello devuelto.</span><span class="sxs-lookup"><span data-stu-id="be687-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![valor de contador con estado de Hello muestra en el Explorador de Hola][browser-aspnet-counter-value]
   
    <span data-ttu-id="be687-203">Actualice el Explorador de hello actualización del valor toosee Hola contador periódicamente.</span><span class="sxs-lookup"><span data-stu-id="be687-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="be687-204">Kestrel y WebListener</span><span class="sxs-lookup"><span data-stu-id="be687-204">Kestrel and WebListener</span></span>

<span data-ttu-id="be687-205">Hello predeterminada ASP.NET web server Core, conocido como Kestrel, es [no se admite actualmente para controlar el tráfico de internet directa](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="be687-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="be687-206">Como resultado, hello plantilla de servicio sin estado ASP.NET Core Service Fabric usa [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="be687-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="be687-207">toolearn más información sobre Kestrel y WebListener en servicios de Service Fabric, consulte demasiado[ASP.NET Core en servicios de Service Fabric confiable](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="be687-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="be687-208">Conexión de servicio de Actor confiable tooa</span><span class="sxs-lookup"><span data-stu-id="be687-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="be687-209">Este tutorial se centra en la incorporación de un front-end web que se comunica con un servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="be687-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="be687-210">Sin embargo, puede seguir una muy similar tooactors tootalk de modelo.</span><span class="sxs-lookup"><span data-stu-id="be687-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="be687-211">Cuando se crea un proyecto de Reliable Actor, Visual Studio genera automáticamente un proyecto de interfaz.</span><span class="sxs-lookup"><span data-stu-id="be687-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="be687-212">Puede usar ese toogenerate interfaz un proxy de actor en hello web proyecto toocommunicate con actor Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="be687-213">canal de comunicación de Hola se proporciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="be687-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="be687-214">Así, no es necesario toodo cualquier cosa que es equivalente tooestablishing un `ServiceRemotingListener` como hizo para el servicio con estado de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="be687-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="be687-215">Cómo funcionan los servicios web en el clúster local</span><span class="sxs-lookup"><span data-stu-id="be687-215">How web services work on your local cluster</span></span>
<span data-ttu-id="be687-216">En general, puede implementar exactamente Hola mismo tejido de servicio aplicación tooa varias máquinas de clúster que se implementa en el clúster local y ser muy seguro que funciona según lo esperado.</span><span class="sxs-lookup"><span data-stu-id="be687-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="be687-217">Esto es porque el clúster local es simplemente una configuración de cinco nodos que contrae tooa único equipo.</span><span class="sxs-lookup"><span data-stu-id="be687-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="be687-218">Cuando se trata de servicios de tooweb, sin embargo, hay un matiz de clave.</span><span class="sxs-lookup"><span data-stu-id="be687-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="be687-219">Cuando el clúster se encuentra detrás de un equilibrador de carga, como ocurre en Azure, debe asegurarse de que los servicios web se implementan en todos los equipos desde el equilibrador de carga de hello simplemente operaciones por turnos de tráfico en los equipos de Hola.</span><span class="sxs-lookup"><span data-stu-id="be687-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="be687-220">Para ello, establecer hello `InstanceCount` para hello servicio toohello valor especial "-1".</span><span class="sxs-lookup"><span data-stu-id="be687-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="be687-221">Por el contrario, cuando se ejecuta un servicio web localmente, necesita tooensure que solo una instancia del servicio de saludo se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="be687-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="be687-222">En caso contrario, experimenta conflictos de varios procesos que están escuchando en hello misma ruta de acceso y el puerto.</span><span class="sxs-lookup"><span data-stu-id="be687-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="be687-223">Como resultado, se debe establecer recuento de instancias de servicio web de hello demasiado "1" para implementaciones locales.</span><span class="sxs-lookup"><span data-stu-id="be687-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="be687-224">toolearn tooconfigure distintos valores de entorno diferente, vea [administrar parámetros de la aplicación para varios entornos](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="be687-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="be687-225">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be687-225">Next steps</span></span>
<span data-ttu-id="be687-226">Ahora que tiene un front-end web configurado para la aplicación con ASP.NET Core, obtenga más información sobre [ASP.NET Core en Reliable Services de Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) para una descripción detallada de cómo funciona ASP.NET Core con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="be687-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="be687-227">Después, [más información sobre la comunicación con servicios](service-fabric-connect-and-communicate-with-services.md) en general tooget a completar imagen de servicio cómo funciona la comunicación en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="be687-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="be687-228">Una vez que tenga una buena comprensión del funcionamiento de la comunicación del servicio, [crear un clúster de Azure e implementar la nube de toohello aplicación](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be687-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
