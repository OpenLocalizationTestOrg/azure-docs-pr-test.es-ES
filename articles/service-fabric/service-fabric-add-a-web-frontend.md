---
title: "Creación de un front-end web para la aplicación de Azure Service Fabric mediante ASP.NET Core| Microsoft Docs"
description: "Exponga la aplicación de Service Fabric a la Web usando un proyecto de ASP.NET Core y la comunicación entre servicios a través de Service Remoting."
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
ms.openlocfilehash: b19aaa652f2c15573ded632ca1348e1a6752f080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="f37d5-103">Creación de un front-end de servicio web para una aplicación mediante ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f37d5-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="f37d5-104">De forma predeterminada, los servicios de Azure Service Fabric no proporcionan una interfaz pública para la Web.</span><span class="sxs-lookup"><span data-stu-id="f37d5-104">By default, Azure Service Fabric services do not provide a public interface to the web.</span></span> <span data-ttu-id="f37d5-105">Para exponer la funcionalidad de su aplicación a los clientes HTTP, tendrá que crear un proyecto web para que actúe como punto de entrada y, a continuación, comunicarse desde allí con los servicios individuales.</span><span class="sxs-lookup"><span data-stu-id="f37d5-105">To expose your application's functionality to HTTP clients, you have to create a web project to act as an entry point and then communicate from there to your individual services.</span></span>

<span data-ttu-id="f37d5-106">En este tutorial, continuaremos a partir del punto en el que terminamos en el tutorial [Creación de la primera aplicación en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) y agregaremos un servicio web de ASP.NET Core delante el servicio de contador con estado.</span><span class="sxs-lookup"><span data-stu-id="f37d5-106">In this tutorial, we pick up where we left off in the [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of the stateful counter service.</span></span> <span data-ttu-id="f37d5-107">Si aún no lo ha hecho, debe revisar primero ese tutorial.</span><span class="sxs-lookup"><span data-stu-id="f37d5-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="f37d5-108">Configuración del entorno para ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f37d5-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="f37d5-109">Necesita Visual Studio 2017 para seguir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f37d5-109">You need Visual Studio 2017 to follow along with this tutorial.</span></span> <span data-ttu-id="f37d5-110">Cualquier edición servirá.</span><span class="sxs-lookup"><span data-stu-id="f37d5-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="f37d5-111">Instalación de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f37d5-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="f37d5-112">Para desarrollar aplicaciones de ASP.NET Core de Service Fabric, debe tener las cargas de trabajo siguientes instaladas:</span><span class="sxs-lookup"><span data-stu-id="f37d5-112">To develop ASP.NET Core Service Fabric applications, you should have the following workloads installed:</span></span>
 - <span data-ttu-id="f37d5-113">**Desarrollo de Azure** (en *Web y nube*)</span><span class="sxs-lookup"><span data-stu-id="f37d5-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="f37d5-114">**ASP.NET y desarrollo web** (en *Web y nube*)</span><span class="sxs-lookup"><span data-stu-id="f37d5-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="f37d5-115">**Desarrollo multiplataforma de .NET Core** (en *Otros conjuntos de herramientas*)</span><span class="sxs-lookup"><span data-stu-id="f37d5-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="f37d5-116">Las herramientas de .NET Core para Visual Studio 2015 ya no se actualizan, sin embargo, si todavía usa Visual Studio 2015, debe tener instalado [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="f37d5-116">The .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need to have [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-to-your-application"></a><span data-ttu-id="f37d5-117">Incorporación de un servicio ASP.NET Core a una aplicación</span><span class="sxs-lookup"><span data-stu-id="f37d5-117">Add an ASP.NET Core service to your application</span></span>
<span data-ttu-id="f37d5-118">ASP.NET Core es un marco de desarrollo web ligero multiplataforma, que puede usar para crear modernas interfaces de usuario web y API web.</span><span class="sxs-lookup"><span data-stu-id="f37d5-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> 

<span data-ttu-id="f37d5-119">Vamos a agregar un proyecto API web de ASP.NET a la aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="f37d5-119">Let's add an ASP.NET Web API project to our existing application.</span></span>

1. <span data-ttu-id="f37d5-120">En el Explorador de soluciones, haga clic con el botón derecho en **Servicios**, en el proyecto de aplicación y seleccione **Agregar > Nuevo servicio de Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="f37d5-120">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Incorporación de un nuevo servicio a una aplicación existente][vs-add-new-service]
2. <span data-ttu-id="f37d5-122">En la página **Create a Service** (Crear un servicio), elija **ASP.NET Core** y asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="f37d5-122">On the **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Selección del servicio web ASP.NET en el cuadro de diálogo de nuevo servicio][vs-new-service-dialog]

3. <span data-ttu-id="f37d5-124">En la página siguiente se proporciona un conjunto de plantillas de proyecto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f37d5-124">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="f37d5-125">Tenga en cuenta que son las mismas opciones que vería si crea un proyecto de ASP.NET Core fuera de una aplicación de Service Fabric, con una pequeña cantidad de código adicional para registrar el servicio con el runtime de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f37d5-125">Note that these are the same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code to register the service with the Service Fabric runtime.</span></span> <span data-ttu-id="f37d5-126">Para este tutorial, elija **API Web**.</span><span class="sxs-lookup"><span data-stu-id="f37d5-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="f37d5-127">Sin embargo, puede aplicar los mismos conceptos a la creación de una aplicación web completa.</span><span class="sxs-lookup"><span data-stu-id="f37d5-127">However, you can apply the same concepts to building a full web application.</span></span>
   
    ![Elección del tipo de proyecto ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="f37d5-129">Una vez creado el proyecto API web, tendrá dos servicios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f37d5-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="f37d5-130">Mientras continúa la creación de la aplicación, puede agregar más servicios exactamente de la misma forma.</span><span class="sxs-lookup"><span data-stu-id="f37d5-130">As you continue to build your application, you can add more services in exactly the same way.</span></span> <span data-ttu-id="f37d5-131">Cada uno puede tener versiones y actualizaciones independientes.</span><span class="sxs-lookup"><span data-stu-id="f37d5-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="f37d5-132">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f37d5-132">Run the application</span></span>
<span data-ttu-id="f37d5-133">Para tener una idea de lo que hemos hecho, vamos a implementar la nueva aplicación y a observar el comportamiento predeterminado que proporciona la plantilla API web de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f37d5-133">To get a sense of what we've done, let's deploy the new application and take a look at the default behavior that the ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="f37d5-134">Presione F5 en Visual Studio para depurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f37d5-134">Press F5 in Visual Studio to debug the app.</span></span>
2. <span data-ttu-id="f37d5-135">Cuando se complete la implementación, Visual Studio iniciará el explorador en la raíz del servicio API Web de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f37d5-135">When deployment is complete, Visual Studio launches a browser to the root of the ASP.NET Web API service.</span></span> <span data-ttu-id="f37d5-136">La plantilla API Web de ASP.NET Core no proporciona comportamiento predeterminado para la raíz, por lo que el explorador mostrará un error 404.</span><span class="sxs-lookup"><span data-stu-id="f37d5-136">The ASP.NET Core Web API template doesn't provide default behavior for the root, so you should see a 404 error in the browser.</span></span>
3. <span data-ttu-id="f37d5-137">Agregue `/api/values` a la ubicación en el explorador.</span><span class="sxs-lookup"><span data-stu-id="f37d5-137">Add `/api/values` to the location in the browser.</span></span> <span data-ttu-id="f37d5-138">Esta acción invoca el método `Get` de la clase ValuesController de la plantilla de API Web.</span><span class="sxs-lookup"><span data-stu-id="f37d5-138">This invokes the `Get` method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="f37d5-139">Devuelve la respuesta predeterminada proporcionada por la plantilla, una matriz JSON que contiene dos cadenas:</span><span class="sxs-lookup"><span data-stu-id="f37d5-139">It returns the default response that is provided by the template--a JSON array that contains two strings:</span></span>
   
    ![Valores predeterminados devueltos desde la plantilla API web de ASP.NET Core][browser-aspnet-template-values]
   
    <span data-ttu-id="f37d5-141">Al final del tutorial, la página mostrará el valor más reciente del contador de nuestro servicio con estado en lugar de las cadenas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="f37d5-141">By the end of the tutorial, this page will show the most recent counter value from our stateful service instead of the default strings.</span></span>

## <a name="connect-the-services"></a><span data-ttu-id="f37d5-142">Conexión de los servicios</span><span class="sxs-lookup"><span data-stu-id="f37d5-142">Connect the services</span></span>
<span data-ttu-id="f37d5-143">Service Fabric proporciona una flexibilidad completa en el modo de comunicación con los servicios confiables.</span><span class="sxs-lookup"><span data-stu-id="f37d5-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="f37d5-144">En una sola aplicación, podría tener servicios que son accesibles a través de TCP, servicios que son accesibles a través de una API de REST de HTTP y servicios que son accesibles a través de sockets web.</span><span class="sxs-lookup"><span data-stu-id="f37d5-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="f37d5-145">Para más información sobre las opciones disponibles y sus inconvenientes, consulte [Conexión y comunicación con servicios en Service Fabric](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="f37d5-145">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="f37d5-146">En este tutorial, usamos [Comunicación remota de servicios de Service Fabric](service-fabric-reliable-services-communication-remoting.md), proporcionado en el SDK.</span><span class="sxs-lookup"><span data-stu-id="f37d5-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in the SDK.</span></span>

<span data-ttu-id="f37d5-147">En el enfoque de Comunicación remota de servicios (basado en llamadas a procedimientos remotos o RPC), se define una interfaz que actúa como el contrato público del servicio.</span><span class="sxs-lookup"><span data-stu-id="f37d5-147">In the Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface to act as the public contract for the service.</span></span> <span data-ttu-id="f37d5-148">Luego, se usa esa interfaz para generar una clase de proxy para interactuar con el servicio.</span><span class="sxs-lookup"><span data-stu-id="f37d5-148">Then, you use that interface to generate a proxy class for interacting with the service.</span></span>

### <a name="create-the-remoting-interface"></a><span data-ttu-id="f37d5-149">Creación de la interfaz remota</span><span class="sxs-lookup"><span data-stu-id="f37d5-149">Create the remoting interface</span></span>
<span data-ttu-id="f37d5-150">Comenzaremos por la creación de la interfaz para que actúe como contrato entre el servicio con estado y otros servicios, en este caso, el proyecto web de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f37d5-150">Let's start by creating the interface to act as the contract between the stateful service and other services, in this case the ASP.NET Core web project.</span></span> <span data-ttu-id="f37d5-151">Esta interfaz debe estar compartida por todos los servicios que la usan para realizar llamadas RPC, por lo que la vamos a crear en su propio proyecto de biblioteca de clases.</span><span class="sxs-lookup"><span data-stu-id="f37d5-151">This interface must be shared by all services that use it to make RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="f37d5-152">En el Explorador de soluciones, haga clic con el botón derecho en la solución y seleccione **Agregue** > **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="f37d5-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="f37d5-153">Elija la entrada **Visual C#** en el panel de navegación izquierdo y, después, seleccione la plantilla **Biblioteca de clases**.</span><span class="sxs-lookup"><span data-stu-id="f37d5-153">Choose the **Visual C#** entry in the left navigation pane and then select the **Class Library** template.</span></span> <span data-ttu-id="f37d5-154">Asegúrese de que el valor de la versión de .NET Framework es **4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="f37d5-154">Ensure that the .NET Framework version is set to **4.5.2**.</span></span>
   
    ![Creación de un proyecto de interfaz para el servicio con estado][vs-add-class-library-project]

3. <span data-ttu-id="f37d5-156">Instalar el paquete de NuGet **Microsoft.ServiceFabric.Services.Remoting**.</span><span class="sxs-lookup"><span data-stu-id="f37d5-156">Install the **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="f37d5-157">Busque **Microsoft.ServiceFabric.Services.Remoting** en el administrador de paquetes de NuGet e instale el mismo en todos los proyectos de la solución que usan Comunicación remota de servicios, incluidos:</span><span class="sxs-lookup"><span data-stu-id="f37d5-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in the NuGet package manager and install it for all projects in the solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="f37d5-158">El proyecto de biblioteca de clases que contiene la interfaz de servicio</span><span class="sxs-lookup"><span data-stu-id="f37d5-158">The Class Library project that contains the service interface</span></span>
   - <span data-ttu-id="f37d5-159">El proyecto del servicio con estado</span><span class="sxs-lookup"><span data-stu-id="f37d5-159">The Stateful Service project</span></span>
   - <span data-ttu-id="f37d5-160">El proyecto del servicio web de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f37d5-160">The ASP.NET Core web service project</span></span>
   
    ![Incorporación del paquete de NuGet de servicios][vs-services-nuget-package]

4. <span data-ttu-id="f37d5-162">En la biblioteca de clases, cree una interfaz con un único método, `GetCountAsync` y extienda la interfaz de `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="f37d5-162">In the class library, create an interface with a single method, `GetCountAsync`, and extend the interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="f37d5-163">La interfaz de comunicación remota debe derivar de esta interfaz para indicar que es una interfaz de comunicación remota de servicio.</span><span class="sxs-lookup"><span data-stu-id="f37d5-163">The remoting interface must derive from this interface to indicate that it is a Service Remoting interface.</span></span>
   
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

### <a name="implement-the-interface-in-your-stateful-service"></a><span data-ttu-id="f37d5-164">Implementación de la interfaz en el servicio con estado</span><span class="sxs-lookup"><span data-stu-id="f37d5-164">Implement the interface in your stateful service</span></span>
<span data-ttu-id="f37d5-165">Ahora que hemos definido la interfaz, tenemos que implementarla en el servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="f37d5-165">Now that we have defined the interface, we need to implement it in the stateful service.</span></span>

1. <span data-ttu-id="f37d5-166">En el servicio con estado, agregue una referencia al proyecto de biblioteca de clases que contiene la interfaz.</span><span class="sxs-lookup"><span data-stu-id="f37d5-166">In your stateful service, add a reference to the class library project that contains the interface.</span></span>
   
    ![Incorporación de una referencia al proyecto de biblioteca de clases en el servicio con estado][vs-add-class-library-reference]
2. <span data-ttu-id="f37d5-168">Busque la clase que se hereda de `StatefulService`, como `MyStatefulService`, y amplíela para implementar la interfaz `ICounter`.</span><span class="sxs-lookup"><span data-stu-id="f37d5-168">Locate the class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it to implement the `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="f37d5-169">Ahora, implemente el método único que se define en la interfaz `ICounter`, `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="f37d5-169">Now implement the single method that is defined in the `ICounter` interface, `GetCountAsync`.</span></span>
   
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

### <a name="expose-the-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="f37d5-170">Exposición del servicio con estado mediante un agente de escucha remoto</span><span class="sxs-lookup"><span data-stu-id="f37d5-170">Expose the stateful service using a service remoting listener</span></span>
<span data-ttu-id="f37d5-171">Con la interfaz `ICounter` implementada, el paso final consiste en abrir el canal de comunicación de Comunicación remota de servicio.</span><span class="sxs-lookup"><span data-stu-id="f37d5-171">With the `ICounter` interface implemented, the final step is to open the Service Remoting communication channel.</span></span> <span data-ttu-id="f37d5-172">Para los servicios con estado, Service Fabric proporciona un método reemplazable denominado " `CreateServiceReplicaListeners`".</span><span class="sxs-lookup"><span data-stu-id="f37d5-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="f37d5-173">Con este método, puede especificar uno o varios agentes de escucha de comunicación, según el tipo de comunicación que desee habilitar para el servicio.</span><span class="sxs-lookup"><span data-stu-id="f37d5-173">With this method, you can specify one or more communication listeners, based on the type of communication that you want to enable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="f37d5-174">El método equivalente para abrir un canal de comunicación a los servicios sin estado se llama `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="f37d5-174">The equivalent method for opening a communication channel to stateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="f37d5-175">En este caso, reemplazamos el método `CreateServiceReplicaListeners` actual e incluimos una instancia de `ServiceRemotingListener`, que crea un punto de conexión RPC al que los clientes pueden llamar usando `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="f37d5-175">In this case, we replace the existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="f37d5-176">El método de extensión `CreateServiceRemotingListener` de la interfaz `IService` le permite crear fácilmente un `ServiceRemotingListener` con todos los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="f37d5-176">The `CreateServiceRemotingListener` extension method on the `IService` interface allows you to easily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="f37d5-177">Para utilizar este método de extensión, asegúrese de que ha importado el espacio de nombres `Microsoft.ServiceFabric.Services.Remoting.Runtime`.</span><span class="sxs-lookup"><span data-stu-id="f37d5-177">To use this extension method, ensure you have the `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

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


### <a name="use-the-serviceproxy-class-to-interact-with-the-service"></a><span data-ttu-id="f37d5-178">Uso de la clase ServiceProxy para interactuar con el servicio</span><span class="sxs-lookup"><span data-stu-id="f37d5-178">Use the ServiceProxy class to interact with the service</span></span>
<span data-ttu-id="f37d5-179">Nuestro servicio con estado está ahora preparado para recibir tráfico de otros servicios a través de RPC.</span><span class="sxs-lookup"><span data-stu-id="f37d5-179">Our stateful service is now ready to receive traffic from other services over RPC.</span></span> <span data-ttu-id="f37d5-180">Así que todo lo que queda es agregar el código para comunicarse con él desde el servicio web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f37d5-180">So all that remains is adding the code to communicate with it from the ASP.NET web service.</span></span>

1. <span data-ttu-id="f37d5-181">En el proyecto ASP.NET, agregue una referencia a la biblioteca de clases que contiene la interfaz `ICounter` .</span><span class="sxs-lookup"><span data-stu-id="f37d5-181">In your ASP.NET project, add a reference to the class library that contains the `ICounter` interface.</span></span>

2. <span data-ttu-id="f37d5-182">Antes ha agregado el paquete de NuGet **Microsoft.ServiceFabric.Services.Remoting** al proyecto ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f37d5-182">Earlier you added the **Microsoft.ServiceFabric.Services.Remoting** NuGet package to the ASP.NET project.</span></span> <span data-ttu-id="f37d5-183">Este paquete ofrece la clase `ServiceProxy` que se utiliza para realizar llamadas RPC al servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="f37d5-183">This package provides the `ServiceProxy` class which you use to make RPC calls to the stateful service.</span></span> <span data-ttu-id="f37d5-184">Asegúrese de que este paquete de NuGet está instalado en el proyecto del servicio web de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f37d5-184">Ensure this NuGet package is installed in the ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="f37d5-185">En la carpeta **Controladores**, abra la clase `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="f37d5-185">In the **Controllers** folder, open the `ValuesController` class.</span></span> <span data-ttu-id="f37d5-186">Tenga en cuenta que, en estos momentos, el método `Get` solo devuelve una matriz de cadenas codificadas de forma rígida de value1 y value2, que coincide con lo que vimos anteriormente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="f37d5-186">Note that the `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in the browser.</span></span> <span data-ttu-id="f37d5-187">Reemplace esta implementación con el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="f37d5-187">Replace this implementation with the following code:</span></span>
   
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
   
    <span data-ttu-id="f37d5-188">La primera línea de código es la clave.</span><span class="sxs-lookup"><span data-stu-id="f37d5-188">The first line of code is the key one.</span></span> <span data-ttu-id="f37d5-189">Para crear el proxy ICounter para el servicio con estado, tiene que proporcionar dos fragmentos de información: un identificador de partición y el nombre del servicio.</span><span class="sxs-lookup"><span data-stu-id="f37d5-189">To create the ICounter proxy to the stateful service, you need to provide two pieces of information: a partition ID and the name of the service.</span></span>
   
    <span data-ttu-id="f37d5-190">Puede usar particiones para escalar servicios con estado dividiendo su estado en depósitos distintos en función de una clave que usted define, como puede ser un identificador de cliente o un código postal.</span><span class="sxs-lookup"><span data-stu-id="f37d5-190">You can use partitioning to scale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="f37d5-191">En nuestra sencilla aplicación, el servicio con estado tiene solo una partición, por lo que no importa la clave.</span><span class="sxs-lookup"><span data-stu-id="f37d5-191">In our trivial application, the stateful service only has one partition, so the key doesn't matter.</span></span> <span data-ttu-id="f37d5-192">Cualquier clave que proporcione llevará a la misma partición.</span><span class="sxs-lookup"><span data-stu-id="f37d5-192">Any key that you provide will lead to the same partition.</span></span> <span data-ttu-id="f37d5-193">Consulte [Partición de Service Fabric Reliable Services](service-fabric-concepts-partitioning.md)para obtener más información sobre los servicios de partición.</span><span class="sxs-lookup"><span data-stu-id="f37d5-193">To learn more about partitioning services, see [How to partition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="f37d5-194">El nombre del servicio es un identificador URI con el formato fabric:/&lt;nombre_de_aplicación&gt;/&lt;nombre_de_servicio&gt;.</span><span class="sxs-lookup"><span data-stu-id="f37d5-194">The service name is a URI of the form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="f37d5-195">Con estas dos piezas de información, Service Fabric puede identificar de forma exclusiva el equipo al que se deben enviar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="f37d5-195">With these two pieces of information, Service Fabric can uniquely identify the machine that requests should be sent to.</span></span> <span data-ttu-id="f37d5-196">La clase `ServiceProxy` también controlará sin ningún problema los casos en los que se produce un error en la máquina que hospeda la partición de servicio con estado y hay que promover otra máquina para que ocupe su lugar.</span><span class="sxs-lookup"><span data-stu-id="f37d5-196">The `ServiceProxy` class also seamlessly handles the case where the machine that hosts the stateful service partition fails and another machine must be promoted to take its place.</span></span> <span data-ttu-id="f37d5-197">Esta abstracción simplifica considerablemente la escritura del código de cliente para tratar con otros servicios.</span><span class="sxs-lookup"><span data-stu-id="f37d5-197">This abstraction makes writing the client code to deal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="f37d5-198">Una vez que se tiene el proxy, simplemente se invoca el método `GetCountAsync` y se devuelve su resultado.</span><span class="sxs-lookup"><span data-stu-id="f37d5-198">Once we have the proxy, we simply invoke the `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="f37d5-199">Presione F5 de nuevo para ejecutar la aplicación modificada.</span><span class="sxs-lookup"><span data-stu-id="f37d5-199">Press F5 again to run the modified application.</span></span> <span data-ttu-id="f37d5-200">Como antes, Visual Studio inicia automáticamente el explorador en la raíz del proyecto web.</span><span class="sxs-lookup"><span data-stu-id="f37d5-200">As before, Visual Studio automatically launches the browser to the root of the web project.</span></span> <span data-ttu-id="f37d5-201">Agregue la ruta de acceso "api/values", debería ver el valor actual del contador devuelto.</span><span class="sxs-lookup"><span data-stu-id="f37d5-201">Add the "api/values" path, and you should see the current counter value returned.</span></span>
   
    ![El valor del contador con estado aparece en el explorador][browser-aspnet-counter-value]
   
    <span data-ttu-id="f37d5-203">Actualice el explorador periódicamente para ver el valor actualizado del contador.</span><span class="sxs-lookup"><span data-stu-id="f37d5-203">Refresh the browser periodically to see the counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="f37d5-204">Kestrel y WebListener</span><span class="sxs-lookup"><span data-stu-id="f37d5-204">Kestrel and WebListener</span></span>

<span data-ttu-id="f37d5-205">Es el servidor web predeterminado de ASP.NET Core, que se conoce como Kestrel, [no se admite actualmente para controlar el tráfico directo de Internet](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="f37d5-205">The default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="f37d5-206">Como resultado, la plantilla de servicio sin estado de ASP.NET Core para Service Fabric usa [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f37d5-206">As a result, the ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="f37d5-207">Para más información sobre Kestrel y WebListener en los servicios de Service Fabric, vea [ASP.NET Core en Reliable Services de Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="f37d5-207">To learn more about Kestrel and WebListener in Service Fabric services, please refer to [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-to-a-reliable-actor-service"></a><span data-ttu-id="f37d5-208">Conexión a un servicio de Reliable Actor</span><span class="sxs-lookup"><span data-stu-id="f37d5-208">Connecting to a Reliable Actor service</span></span>
<span data-ttu-id="f37d5-209">Este tutorial se centra en la incorporación de un front-end web que se comunica con un servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="f37d5-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="f37d5-210">Sin embargo, puede seguir un modelo muy parecido a hablar con los actores.</span><span class="sxs-lookup"><span data-stu-id="f37d5-210">However, you can follow a very similar model to talk to actors.</span></span> <span data-ttu-id="f37d5-211">Cuando se crea un proyecto de Reliable Actor, Visual Studio genera automáticamente un proyecto de interfaz.</span><span class="sxs-lookup"><span data-stu-id="f37d5-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="f37d5-212">Puede usar esta interfaz para generar un proxy de actor en el proyecto web para comunicarse con el actor.</span><span class="sxs-lookup"><span data-stu-id="f37d5-212">You can use that interface to generate an actor proxy in the web project to communicate with the actor.</span></span> <span data-ttu-id="f37d5-213">El canal de comunicación se proporciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f37d5-213">The communication channel is provided automatically.</span></span> <span data-ttu-id="f37d5-214">Por tanto, no hay que realizar ninguna acción equivalente a establecer una instancia de `ServiceRemotingListener` como se hizo para el servicio con estado en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f37d5-214">So you do not need to do anything that is equivalent to establishing a `ServiceRemotingListener` like you did for the stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="f37d5-215">Cómo funcionan los servicios web en el clúster local</span><span class="sxs-lookup"><span data-stu-id="f37d5-215">How web services work on your local cluster</span></span>
<span data-ttu-id="f37d5-216">En general, puede implementar exactamente la misma aplicación de Service Fabric en un clúster de varias máquinas que en el clúster local y tener la completa seguridad de que funcionará como se espera.</span><span class="sxs-lookup"><span data-stu-id="f37d5-216">In general, you can deploy exactly the same Service Fabric application to a multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="f37d5-217">El motivo es que el clúster local es simplemente una configuración de cinco nodos que se consolida en una sola máquina.</span><span class="sxs-lookup"><span data-stu-id="f37d5-217">This is because your local cluster is simply a five-node configuration that is collapsed to a single machine.</span></span>

<span data-ttu-id="f37d5-218">En cuanto a los servicios web, de todas formas, existe un matiz clave.</span><span class="sxs-lookup"><span data-stu-id="f37d5-218">When it comes to web services, however, there is one key nuance.</span></span> <span data-ttu-id="f37d5-219">Cuando el clúster se encuentra detrás de un equilibrador de carga, como sucede en Azure, tiene que asegurarse de que los servicios web se implementan en todas las máquinas, ya que el equilibrador de carga simplemente realiza un enrutamiento del tráfico por turnos entre las máquinas.</span><span class="sxs-lookup"><span data-stu-id="f37d5-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since the load balancer simply round-robins traffic across the machines.</span></span> <span data-ttu-id="f37d5-220">Para ello, establezca `InstanceCount` para el servicio en el valor especial de -1.</span><span class="sxs-lookup"><span data-stu-id="f37d5-220">You can do this by setting the `InstanceCount` for the service to the special value of "-1".</span></span>

<span data-ttu-id="f37d5-221">Por el contrario, cuando se ejecuta un servicio web localmente, debe asegurarse de que solo una instancia del servicio se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="f37d5-221">By contrast, when you run a web service locally, you need to ensure that only one instance of the service is running.</span></span> <span data-ttu-id="f37d5-222">En caso contrario, se encontrará con problemas debido a que hay varios procesos que escuchan en la misma ruta de acceso y puerto.</span><span class="sxs-lookup"><span data-stu-id="f37d5-222">Otherwise, you run into conflicts from multiple processes that are listening on the same path and port.</span></span> <span data-ttu-id="f37d5-223">Como resultado, el recuento de instancias de servicio web debe establecerse en "1" para implementaciones locales.</span><span class="sxs-lookup"><span data-stu-id="f37d5-223">As a result, the web service instance count should be set to "1" for local deployments.</span></span>

<span data-ttu-id="f37d5-224">Para obtener información sobre cómo configurar valores diferentes para diferentes entorno, consulte [Administración de los parámetros de la aplicación en varios entornos](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="f37d5-224">To learn how to configure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f37d5-225">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f37d5-225">Next steps</span></span>
<span data-ttu-id="f37d5-226">Ahora que tiene un front-end web configurado para la aplicación con ASP.NET Core, obtenga más información sobre [ASP.NET Core en Reliable Services de Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) para una descripción detallada de cómo funciona ASP.NET Core con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f37d5-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="f37d5-227">Después, [obtenga más información sobre la comunicación con los servicios](service-fabric-connect-and-communicate-with-services.md) en general para obtener una imagen completa de cómo funciona la comunicación con el servicio en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f37d5-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general to get a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="f37d5-228">Una vez que haya entendido bien el funcionamiento de la comunicación del servicio, [cree un clúster en Azure e implemente la aplicación en la nube](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f37d5-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application to the cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

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
