---
title: aaaCreate su primera microservicio Azure basado en actores en C# | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de crear, depurar e implementar un servicio simple basado en actores mediante servicio de Fabric Reliable Actors."
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
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="daf4f-103">Introducción a Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="daf4f-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="daf4f-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="daf4f-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="daf4f-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="daf4f-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="daf4f-106">En este artículo se explica conceptos básicos de Hola de Azure Service Fabric Reliable Actors y le guía a través de crear, depurar e implementar una aplicación sencilla de Actor confiable en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daf4f-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="daf4f-107">Instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="daf4f-107">Installation and setup</span></span>
<span data-ttu-id="daf4f-108">Antes de empezar, asegúrese de que tiene el entorno de desarrollo de Service Fabric Hola configurado en su equipo.</span><span class="sxs-lookup"><span data-stu-id="daf4f-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="daf4f-109">Si necesita tooset, configúrelo, vea instrucciones detalladas en [cómo tooset el entorno de desarrollo de hello](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="daf4f-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="daf4f-110">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="daf4f-110">Basic concepts</span></span>
<span data-ttu-id="daf4f-111">tooget partió Reliable Actors, sólo necesita toounderstand algunos conceptos básicos:</span><span class="sxs-lookup"><span data-stu-id="daf4f-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="daf4f-112">**Servicio de actor**.</span><span class="sxs-lookup"><span data-stu-id="daf4f-112">**Actor service**.</span></span> <span data-ttu-id="daf4f-113">Actores confiables se empaquetan en servicios de confianza que se pueden implementar en la infraestructura de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="daf4f-114">Las instancias de actor se activan en una instancia de servicio con nombre.</span><span class="sxs-lookup"><span data-stu-id="daf4f-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="daf4f-115">**Registro de actor**.</span><span class="sxs-lookup"><span data-stu-id="daf4f-115">**Actor registration**.</span></span> <span data-ttu-id="daf4f-116">Como con los servicios de confianza, un servicio de Actor confiable debe toobe registrado con el tiempo de ejecución de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="daf4f-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="daf4f-117">Además, el tipo de actor de hello necesita toobe registrado con el tiempo de ejecución de hello Actor.</span><span class="sxs-lookup"><span data-stu-id="daf4f-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="daf4f-118">**Interfaz de actor**.</span><span class="sxs-lookup"><span data-stu-id="daf4f-118">**Actor interface**.</span></span> <span data-ttu-id="daf4f-119">interfaz de actor Hello es toodefine usa una interfaz pública fuertemente tipada de un actor.</span><span class="sxs-lookup"><span data-stu-id="daf4f-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="daf4f-120">Hola terminología del modelo confiable Actor, interfaz de actor de hello define Hola pueden entender y procesar tipos de mensajes que Hola actor.</span><span class="sxs-lookup"><span data-stu-id="daf4f-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="daf4f-121">Hola actor interfaz la utilizan otros actores y las aplicaciones cliente demasiado "envían" (de forma asincrónica) actor toohello de mensajes.</span><span class="sxs-lookup"><span data-stu-id="daf4f-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="daf4f-122">Reliable Actors pueden implementar varias interfaces.</span><span class="sxs-lookup"><span data-stu-id="daf4f-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="daf4f-123">**Clase ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="daf4f-123">**ActorProxy class**.</span></span> <span data-ttu-id="daf4f-124">tooinvoke de las aplicaciones cliente utilizan Hello ActorProxy clase Hola métodos expuestos a través de la interfaz de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="daf4f-125">Hola ActorProxy clase proporciona dos funciones importantes:</span><span class="sxs-lookup"><span data-stu-id="daf4f-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="daf4f-126">La resolución de nombres: es capaz de toolocate actor de hello en clúster de hello (Buscar Hola nodo de clúster Hola donde estén hospedados).</span><span class="sxs-lookup"><span data-stu-id="daf4f-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="daf4f-127">Control de error: se puede reintentar las invocaciones de método y volver a resolver la ubicación de actor de hello después, por ejemplo, un error que requiere Hola actor toobe reubicado tooanother nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="daf4f-128">Hola siguiendo las reglas que pertenecen tooactor interfaces merece la pena comentar:</span><span class="sxs-lookup"><span data-stu-id="daf4f-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="daf4f-129">No se pueden sobrecargar los métodos de interfaz de actor.</span><span class="sxs-lookup"><span data-stu-id="daf4f-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="daf4f-130">Los métodos de interfaz de actor no deben tener parámetros out, ref u opcionales.</span><span class="sxs-lookup"><span data-stu-id="daf4f-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="daf4f-131">No se admiten las interfaces genéricas.</span><span class="sxs-lookup"><span data-stu-id="daf4f-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="daf4f-132">Creación de un proyecto en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="daf4f-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="daf4f-133">Inicie Visual Studio 2015 o Visual Studio 2017 como administrador y cree un nuevo proyecto de aplicación de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="daf4f-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Herramientas de Service Fabric para Visual Studio: nuevo proyecto][1]

<span data-ttu-id="daf4f-135">En el siguiente cuadro de diálogo hello, puede elegir a tipo hello de proyecto que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="daf4f-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Plantillas de proyecto de Service Fabric][5]

<span data-ttu-id="daf4f-137">Proyecto HelloWorld de hello, vamos a usar servicio de Service Fabric Reliable Actors Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="daf4f-138">Después de haber creado la solución de hello, debería ver Hola siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="daf4f-138">After you have created hello solution, you should see hello following structure:</span></span>

![Estructura de proyecto de Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="daf4f-140">Bloques de creación básicos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="daf4f-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="daf4f-141">Una solución típica de Reliable Actors se compone de tres proyectos:</span><span class="sxs-lookup"><span data-stu-id="daf4f-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="daf4f-142">**proyecto de aplicación Hola (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="daf4f-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="daf4f-143">Se trata de un proyecto de Hola que todos los servicios de hello juntos para la implementación de los paquetes.</span><span class="sxs-lookup"><span data-stu-id="daf4f-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="daf4f-144">Contiene hello *ApplicationManifest.xml* y scripts de PowerShell para administrar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="daf4f-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="daf4f-145">**proyecto de interfaz de Hello (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="daf4f-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="daf4f-146">Este es el proyecto de Hola que contiene la definición de interfaz Hola actor Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="daf4f-147">En el proyecto de MyActor.Interfaces hello, se pueden definir las interfaces de Hola que se usará en actores de hello en soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="daf4f-148">Las interfaces de actor pueden definirse en cualquier proyecto con cualquier nombre, pero la interfaz de hello define el contrato de actor de hello compartida por la implementación de actor de Hola y clientes de Hola que llaman actor hello, por lo que normalmente tiene sentido toodefine en un ensamblado separar de la implementación de actor hello y puede compartirse entre varios otros proyectos.</span><span class="sxs-lookup"><span data-stu-id="daf4f-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="daf4f-149">**proyecto de servicio de actor Hello (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="daf4f-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="daf4f-150">Esto es Hola proyecto utilizado toodefine Hola Service Fabric servicio que es continuo toohost Hola actor.</span><span class="sxs-lookup"><span data-stu-id="daf4f-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="daf4f-151">Contiene implementación Hola de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="daf4f-152">Una implementación de actor es una clase que deriva de un tipo base hello `Actor` e implementa Hola interfaces que se definen en hello MyActor.Interfaces proyecto.</span><span class="sxs-lookup"><span data-stu-id="daf4f-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="daf4f-153">Una clase de actor también debe implementar un constructor que acepta un `ActorService` instancia y un `ActorId` y los pasa toohello base `Actor` clase.</span><span class="sxs-lookup"><span data-stu-id="daf4f-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="daf4f-154">Esto permite la inyección de dependencia de constructor de dependencias de plataforma.</span><span class="sxs-lookup"><span data-stu-id="daf4f-154">This allows for constructor dependency injection of platform dependencies.</span></span>

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

<span data-ttu-id="daf4f-155">servicio de actor Hola debe estar registrado con un tipo de servicio en tiempo de ejecución de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="daf4f-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="daf4f-156">En orden para hello toorun de servicio de Actor las instancias del actor, el tipo de actor también deben registrarse con el servicio de Actor hello.</span><span class="sxs-lookup"><span data-stu-id="daf4f-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="daf4f-157">Hola `ActorRuntime` método de registro realizará esta tarea para actores.</span><span class="sxs-lookup"><span data-stu-id="daf4f-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

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

<span data-ttu-id="daf4f-158">Si se inicia desde un proyecto nuevo en Visual Studio y tiene una sola definición de actor, registro de hello se incluye de forma predeterminada en el código de hello que genera Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daf4f-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="daf4f-159">Si define otros actores en servicio de hello, necesita registro de actor hello tooadd mediante:</span><span class="sxs-lookup"><span data-stu-id="daf4f-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="daf4f-160">Hello en tiempo de ejecución de servicio Fabric actores emite algunos [eventos y contadores de rendimiento relacionados con los métodos de tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="daf4f-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="daf4f-161">Son útiles para la supervisión del rendimiento y los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="daf4f-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="daf4f-162">Depuración</span><span class="sxs-lookup"><span data-stu-id="daf4f-162">Debugging</span></span>
<span data-ttu-id="daf4f-163">herramientas de Service Fabric Hola para Visual Studio admiten la depuración en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="daf4f-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="daf4f-164">Puede iniciar una sesión de depuración mediante la tecla F5 de posicionamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="daf4f-165">Visual Studio compila (si es necesario) paquetes.</span><span class="sxs-lookup"><span data-stu-id="daf4f-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="daf4f-166">También implementa la aplicación hello en clúster de Service Fabric local hello y asocia el depurador de Hola.</span><span class="sxs-lookup"><span data-stu-id="daf4f-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="daf4f-167">Durante el proceso de implementación de hello, puede ver el progreso de Hola Hola **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="daf4f-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Ventana de resultados de depuración de Service Fabric][3]

## <a name="next-steps"></a><span data-ttu-id="daf4f-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="daf4f-169">Next steps</span></span>
<span data-ttu-id="daf4f-170">Obtenga más información sobre [cómo Reliable Actors usar plataforma Service Fabric de hello](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="daf4f-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
