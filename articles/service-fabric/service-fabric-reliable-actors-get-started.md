---
title: "Creación del primer microservicio de Azure basado en actores en C# | Microsoft Docs"
description: "En este tutorial se explica paso a paso cómo crear, depurar e implementar un servicio de actor sencillo con Reliable Actors de Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 3f447e049ccd33c77f422e8aa703ad6646f9ffa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="6b32c-103">Introducción a Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="6b32c-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b32c-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="6b32c-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="6b32c-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="6b32c-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="6b32c-106">En este artículo se explican los conceptos básicos de Reliable Actors de Azure Service Fabric, además de ofrecer orientación sobre cómo completar los pasos para crear, depurar e implementar una aplicación de Reliable Actors sencilla en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b32c-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="6b32c-107">Instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="6b32c-107">Installation and setup</span></span>
<span data-ttu-id="6b32c-108">Antes de comenzar, asegúrese de que el entorno de desarrollo de Service Fabric está configurado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6b32c-108">Before you start, ensure that you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="6b32c-109">Para ello, vea instrucciones detalladas sobre [cómo configurar el entorno de desarrollo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6b32c-109">If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="6b32c-110">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="6b32c-110">Basic concepts</span></span>
<span data-ttu-id="6b32c-111">Para empezar a trabajar con Reliable Actors, solo es necesario comprender cuatro conceptos básicos:</span><span class="sxs-lookup"><span data-stu-id="6b32c-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="6b32c-112">**Servicio de actor**.</span><span class="sxs-lookup"><span data-stu-id="6b32c-112">**Actor service**.</span></span> <span data-ttu-id="6b32c-113">Reliable Actors se incluye en Reliable Services, que puede implementarse en la infraestructura de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b32c-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="6b32c-114">Las instancias de actor se activan en una instancia de servicio con nombre.</span><span class="sxs-lookup"><span data-stu-id="6b32c-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="6b32c-115">**Registro de actor**.</span><span class="sxs-lookup"><span data-stu-id="6b32c-115">**Actor registration**.</span></span> <span data-ttu-id="6b32c-116">Como con Reliable Services, un servicio de Reliable Actors debe estar registrado en el runtime de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b32c-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="6b32c-117">Además, el tipo de actor debe registrarse con el tiempo de ejecución de Actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="6b32c-118">**Interfaz de actor**.</span><span class="sxs-lookup"><span data-stu-id="6b32c-118">**Actor interface**.</span></span> <span data-ttu-id="6b32c-119">La interfaz de actor se usa para definir una interfaz pública fuertemente tipada de un actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="6b32c-120">En la terminología del modelo de Reliable Actors, la interfaz de actor define los tipos de mensajes que el actor puede entender y procesar.</span><span class="sxs-lookup"><span data-stu-id="6b32c-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="6b32c-121">Otros actores y aplicaciones de cliente usan la interfaz de actor para "enviar" (asincrónicamente) mensajes al actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="6b32c-122">Reliable Actors pueden implementar varias interfaces.</span><span class="sxs-lookup"><span data-stu-id="6b32c-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="6b32c-123">**Clase ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="6b32c-123">**ActorProxy class**.</span></span> <span data-ttu-id="6b32c-124">La clase ActorProxy la usan las aplicaciones cliente para invocar los métodos expuestos a través de una interfaz de actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="6b32c-125">La clase ActorProxy ofrece dos funciones importantes:</span><span class="sxs-lookup"><span data-stu-id="6b32c-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="6b32c-126">Resolución de nombre: Es capaz de ubicar el actor en el clúster (encontrar el nodo del cluster en el que se hospeda).</span><span class="sxs-lookup"><span data-stu-id="6b32c-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="6b32c-127">Control de errores: Puede reintentar las invocaciones de métodos y volver a resolver la ubicación del actor, por ejemplo, tras un error que requiere que el actor se reubique en otro nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="6b32c-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="6b32c-128">Conviene destacar las siguientes reglas que pertenecen a las interfaces de actor:</span><span class="sxs-lookup"><span data-stu-id="6b32c-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="6b32c-129">No se pueden sobrecargar los métodos de interfaz de actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="6b32c-130">Los métodos de interfaz de actor no deben tener parámetros out, ref u opcionales.</span><span class="sxs-lookup"><span data-stu-id="6b32c-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="6b32c-131">No se admiten las interfaces genéricas.</span><span class="sxs-lookup"><span data-stu-id="6b32c-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="6b32c-132">Creación de un proyecto en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b32c-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="6b32c-133">Inicie Visual Studio 2015 o Visual Studio 2017 como administrador y cree un nuevo proyecto de aplicación de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="6b32c-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Herramientas de Service Fabric para Visual Studio: nuevo proyecto][1]

<span data-ttu-id="6b32c-135">En el siguiente cuadro de diálogo puede elegir el tipo de proyecto que desea crear.</span><span class="sxs-lookup"><span data-stu-id="6b32c-135">In the next dialog box, you can choose the type of project that you want to create.</span></span>

![Plantillas de proyecto de Service Fabric][5]

<span data-ttu-id="6b32c-137">Para el proyecto HelloWorld, se usará el servicio Reliable Actors de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b32c-137">For the HelloWorld project, let's use the Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="6b32c-138">Después de haber creado la solución, debe ver la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="6b32c-138">After you have created the solution, you should see the following structure:</span></span>

![Estructura de proyecto de Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="6b32c-140">Bloques de creación básicos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="6b32c-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="6b32c-141">Una solución típica de Reliable Actors se compone de tres proyectos:</span><span class="sxs-lookup"><span data-stu-id="6b32c-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="6b32c-142">**El proyecto de aplicación (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="6b32c-142">**The application project (MyActorApplication)**.</span></span> <span data-ttu-id="6b32c-143">Este es el proyecto que empaqueta todos los servicios juntos para la implementación.</span><span class="sxs-lookup"><span data-stu-id="6b32c-143">This is the project that packages all of the services together for deployment.</span></span> <span data-ttu-id="6b32c-144">Contiene los scripts de PowerShell y *ApplicationManifest.xml* para administrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b32c-144">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span></span>
* <span data-ttu-id="6b32c-145">**El proyecto de interfaz (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="6b32c-145">**The interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="6b32c-146">Este es el proyecto que contiene la definición de la interfaz del actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-146">This is the project that contains the interface definition for the actor.</span></span> <span data-ttu-id="6b32c-147">En el proyecto MyActor.Interfaces puede definir las interfaces que usarán los actores de la solución.</span><span class="sxs-lookup"><span data-stu-id="6b32c-147">In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution.</span></span> <span data-ttu-id="6b32c-148">Las interfaces de actor pueden definirse en cualquier proyecto con el nombre que desee, pero la interfaz define el contrato de actor que comparten la implementación del actor y los clientes que llaman al actor. Por tanto, suele tener sentido definirlas en un ensamblado independiente de la implementación del actor y que se pueda compartir entre varios otros proyectos.</span><span class="sxs-lookup"><span data-stu-id="6b32c-148">Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="6b32c-149">**El proyecto de servicio de actor (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="6b32c-149">**The actor service project (MyActor)**.</span></span> <span data-ttu-id="6b32c-150">Este es el proyecto que se usa para definir el servicio de Service Fabric que hospedará al actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-150">This is the project used to define the Service Fabric service that is going to host the actor.</span></span> <span data-ttu-id="6b32c-151">Contiene la implementación del actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-151">It contains the implementation of the actor.</span></span> <span data-ttu-id="6b32c-152">La implementación del actor es una clase que deriva de un tipo base `Actor` e implementa las interfaces definidas en el proyecto MyActor.Interfaces.</span><span class="sxs-lookup"><span data-stu-id="6b32c-152">An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project.</span></span> <span data-ttu-id="6b32c-153">Una clase de actor también debe implementar un constructor que acepta una instancia `ActorService` y `ActorId` y los pasa a la clase `Actor` base.</span><span class="sxs-lookup"><span data-stu-id="6b32c-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span></span> <span data-ttu-id="6b32c-154">Esto permite la inyección de dependencia de constructor de dependencias de plataforma.</span><span class="sxs-lookup"><span data-stu-id="6b32c-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="6b32c-155">El servicio de actor debe registrarse con un tipo de servicio en el runtime de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b32c-155">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="6b32c-156">Para que el servicio de actor ejecute las instancias de actor, el tipo de actor debe estar registrado también con el servicio de actor.</span><span class="sxs-lookup"><span data-stu-id="6b32c-156">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="6b32c-157">El método de registro `ActorRuntime` realiza este trabajo para los actores.</span><span class="sxs-lookup"><span data-stu-id="6b32c-157">The `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="6b32c-158">Si comienza a partir de un proyecto nuevo en Visual Studio y tiene una única definición de actor, el registro se incluye de forma predeterminada en el código que genera Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b32c-158">If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates.</span></span> <span data-ttu-id="6b32c-159">Si define otros actores en el servicio, deberá agregar el registro de actor mediante:</span><span class="sxs-lookup"><span data-stu-id="6b32c-159">If you define other actors in the service, you need to add the actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="6b32c-160">El sistema en tiempo de ejecución de Service Fabric Actors emite algunos [eventos y contadores de rendimiento relacionados con los métodos de actor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="6b32c-160">The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="6b32c-161">Son útiles para la supervisión del rendimiento y los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="6b32c-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="6b32c-162">Depuración</span><span class="sxs-lookup"><span data-stu-id="6b32c-162">Debugging</span></span>
<span data-ttu-id="6b32c-163">Las herramientas de Service Fabric para Visual Studio admiten la depuración en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="6b32c-163">The Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="6b32c-164">Puede iniciar una sesión de depuración presionando la tecla F5.</span><span class="sxs-lookup"><span data-stu-id="6b32c-164">You can start a debugging session by hitting the F5 key.</span></span> <span data-ttu-id="6b32c-165">Visual Studio compila (si es necesario) paquetes.</span><span class="sxs-lookup"><span data-stu-id="6b32c-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="6b32c-166">También implementa la aplicación en el clúster de Service Fabric local y asocia el depurador.</span><span class="sxs-lookup"><span data-stu-id="6b32c-166">It also deploys the application on the local Service Fabric cluster and attaches the debugger.</span></span>

<span data-ttu-id="6b32c-167">Durante el proceso de implementación, puede ver el progreso en la ventana **Resultados** .</span><span class="sxs-lookup"><span data-stu-id="6b32c-167">During the deployment process, you can see the progress in the **Output** window.</span></span>

![Ventana de resultados de depuración de Service Fabric][3]

## <a name="next-steps"></a><span data-ttu-id="6b32c-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b32c-169">Next steps</span></span>
<span data-ttu-id="6b32c-170">Aprenda más sobre [el uso de la plataforma de Service Fabric por Reliable Actor](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="6b32c-170">Learn more about [how Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
