---
title: aaaCreate su primera microservicio Azure basado en actores en Java | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de crear, depurar e implementar un servicio simple basado en actores mediante servicio de Fabric Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="8d572-103">Introducción a Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8d572-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8d572-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="8d572-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="8d572-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="8d572-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="8d572-106">En este artículo se explica conceptos básicos de Hola de Azure Service Fabric Reliable Actors y le guía a través de la creación e implementación de una aplicación sencilla de Actor confiable en Java.</span><span class="sxs-lookup"><span data-stu-id="8d572-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="8d572-107">Instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="8d572-107">Installation and setup</span></span>
<span data-ttu-id="8d572-108">Antes de empezar, asegúrese de que tiene el entorno de desarrollo de Service Fabric Hola configurado en su equipo.</span><span class="sxs-lookup"><span data-stu-id="8d572-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="8d572-109">Si necesita tooset, configúrelo, vaya demasiado[introducción en Mac](service-fabric-get-started-mac.md) o [introducción en Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8d572-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="8d572-110">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="8d572-110">Basic concepts</span></span>
<span data-ttu-id="8d572-111">tooget partió Reliable Actors, sólo necesita toounderstand algunos conceptos básicos:</span><span class="sxs-lookup"><span data-stu-id="8d572-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="8d572-112">**Servicio de actor**.</span><span class="sxs-lookup"><span data-stu-id="8d572-112">**Actor service**.</span></span> <span data-ttu-id="8d572-113">Actores confiables se empaquetan en servicios de confianza que se pueden implementar en la infraestructura de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="8d572-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="8d572-114">Las instancias de actor se activan en una instancia de servicio con nombre.</span><span class="sxs-lookup"><span data-stu-id="8d572-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="8d572-115">**Registro de actor**.</span><span class="sxs-lookup"><span data-stu-id="8d572-115">**Actor registration**.</span></span> <span data-ttu-id="8d572-116">Como con los servicios de confianza, un servicio de Actor confiable debe toobe registrado con el tiempo de ejecución de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8d572-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="8d572-117">Además, el tipo de actor de hello necesita toobe registrado con el tiempo de ejecución de hello Actor.</span><span class="sxs-lookup"><span data-stu-id="8d572-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="8d572-118">**Interfaz de actor**.</span><span class="sxs-lookup"><span data-stu-id="8d572-118">**Actor interface**.</span></span> <span data-ttu-id="8d572-119">interfaz de actor Hello es toodefine usa una interfaz pública fuertemente tipada de un actor.</span><span class="sxs-lookup"><span data-stu-id="8d572-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="8d572-120">Hola terminología del modelo confiable Actor, interfaz de actor de hello define Hola pueden entender y procesar tipos de mensajes que Hola actor.</span><span class="sxs-lookup"><span data-stu-id="8d572-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="8d572-121">Hola actor interfaz la utilizan otros actores y las aplicaciones cliente demasiado "envían" (de forma asincrónica) actor toohello de mensajes.</span><span class="sxs-lookup"><span data-stu-id="8d572-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="8d572-122">Reliable Actors pueden implementar varias interfaces.</span><span class="sxs-lookup"><span data-stu-id="8d572-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="8d572-123">**Clase ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="8d572-123">**ActorProxy class**.</span></span> <span data-ttu-id="8d572-124">tooinvoke de las aplicaciones cliente utilizan Hello ActorProxy clase Hola métodos expuestos a través de la interfaz de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="8d572-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="8d572-125">Hola ActorProxy clase proporciona dos funciones importantes:</span><span class="sxs-lookup"><span data-stu-id="8d572-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="8d572-126">La resolución de nombres: es capaz de toolocate actor de hello en clúster de hello (Buscar Hola nodo de clúster Hola donde estén hospedados).</span><span class="sxs-lookup"><span data-stu-id="8d572-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="8d572-127">Control de error: se puede reintentar las invocaciones de método y volver a resolver la ubicación de actor de hello después, por ejemplo, un error que requiere Hola actor toobe reubicado tooanother nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d572-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="8d572-128">Hola siguiendo las reglas que pertenecen tooactor interfaces merece la pena comentar:</span><span class="sxs-lookup"><span data-stu-id="8d572-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="8d572-129">No se pueden sobrecargar los métodos de interfaz de actor.</span><span class="sxs-lookup"><span data-stu-id="8d572-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="8d572-130">Los métodos de interfaz de actor no deben tener parámetros out, ref u opcionales.</span><span class="sxs-lookup"><span data-stu-id="8d572-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="8d572-131">No se admiten las interfaces genéricas.</span><span class="sxs-lookup"><span data-stu-id="8d572-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="8d572-132">Creación de un servicio de actor</span><span class="sxs-lookup"><span data-stu-id="8d572-132">Create an actor service</span></span>
<span data-ttu-id="8d572-133">Comience por crear una nueva aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8d572-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="8d572-134">Hola servicio SDK de tejido para Linux incluye un Yeoman scaffolding de hello tooprovide de generador para una aplicación de Service Fabric con un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="8d572-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="8d572-135">Comience ejecutando Hola siguientes Yeoman de comandos:</span><span class="sxs-lookup"><span data-stu-id="8d572-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="8d572-136">Siga Hola instrucciones toocreate una **servicio de Actor confiable**.</span><span class="sxs-lookup"><span data-stu-id="8d572-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="8d572-137">Para este tutorial, el nombre actor de hello y "HelloWorldActorApplication" a los aplicación Hola "HelloWorldActor."</span><span class="sxs-lookup"><span data-stu-id="8d572-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="8d572-138">se crearán Hola siguiendo la técnica scaffolding:</span><span class="sxs-lookup"><span data-stu-id="8d572-138">hello following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="8d572-139">Bloques de creación básicos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8d572-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="8d572-140">conceptos básicos de Hello descritos anteriormente se traducen en Hola de bloques de creación básicos de un servicio de Actor confiable.</span><span class="sxs-lookup"><span data-stu-id="8d572-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="8d572-141">Interfaz de actor</span><span class="sxs-lookup"><span data-stu-id="8d572-141">Actor interface</span></span>
<span data-ttu-id="8d572-142">Esto contiene la definición de interfaz de Hola de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="8d572-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="8d572-143">Esta interfaz define el contrato de actor Hola compartida por la implementación de actor de Hola y clientes de Hola que llaman actor hello, por lo que normalmente tiene sentido toodefine en un lugar al que se separe de implementación de actor hello y puede compartirse por otros diversos servicios o aplicaciones de cliente.</span><span class="sxs-lookup"><span data-stu-id="8d572-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="8d572-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="8d572-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="8d572-145">Servicio de actor</span><span class="sxs-lookup"><span data-stu-id="8d572-145">Actor service</span></span>
<span data-ttu-id="8d572-146">Contiene la implementación del actor y el código de registro del actor.</span><span class="sxs-lookup"><span data-stu-id="8d572-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="8d572-147">clase de actor Hello implementa la interfaz de actor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d572-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="8d572-148">Aquí es donde el actor realiza su trabajo.</span><span class="sxs-lookup"><span data-stu-id="8d572-148">This is where your actor does its work.</span></span>

<span data-ttu-id="8d572-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="8d572-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="8d572-150">Registro del actor</span><span class="sxs-lookup"><span data-stu-id="8d572-150">Actor registration</span></span>
<span data-ttu-id="8d572-151">servicio de actor Hola debe estar registrado con un tipo de servicio en tiempo de ejecución de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8d572-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="8d572-152">En orden para hello toorun de servicio de Actor las instancias del actor, el tipo de actor también deben registrarse con el servicio de Actor hello.</span><span class="sxs-lookup"><span data-stu-id="8d572-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="8d572-153">Hola `ActorRuntime` método de registro realizará esta tarea para actores.</span><span class="sxs-lookup"><span data-stu-id="8d572-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="8d572-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="8d572-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="8d572-155">Cliente de prueba</span><span class="sxs-lookup"><span data-stu-id="8d572-155">Test client</span></span>
<span data-ttu-id="8d572-156">Se trata de una aplicación de cliente de prueba simple se puede ejecutar por separado de hello Service Fabric aplicación tootest su servicio de actor.</span><span class="sxs-lookup"><span data-stu-id="8d572-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="8d572-157">Este es un ejemplo de donde hello ActorProxy puede tooactivate usado y comunicarse con instancias de actor.</span><span class="sxs-lookup"><span data-stu-id="8d572-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="8d572-158">No se implementa con el servicio.</span><span class="sxs-lookup"><span data-stu-id="8d572-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="8d572-159">aplicación Hello</span><span class="sxs-lookup"><span data-stu-id="8d572-159">hello application</span></span>
<span data-ttu-id="8d572-160">Por último, los paquetes de aplicación Hola Hola servicio de actor y cualquier otro servicio que se puede agregar en hello futura juntos para la implementación.</span><span class="sxs-lookup"><span data-stu-id="8d572-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="8d572-161">Contiene hello *ApplicationManifest.xml* y marcadores de posición para el paquete de servicio de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="8d572-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="8d572-162">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="8d572-162">Run hello application</span></span>

<span data-ttu-id="8d572-163">Hola Yeoman scaffolding incluye un gradle script toobuild Hola aplicación y bash scripts toodeploy y quitar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d572-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="8d572-164">aplicación de hello toodeploy, primera aplicación Hola de compilación con gradle:</span><span class="sxs-lookup"><span data-stu-id="8d572-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="8d572-165">Esto creará un paquete de aplicación de Service Fabric que puede implementarse mediante las herramientas de CLI de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8d572-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="8d572-166">Implementación de la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8d572-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="8d572-167">script de "Install.sh" Hello contiene Hola necesarios CLI de tejido de servicio (sfctl) comandos toodeploy Hola paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d572-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="8d572-168">Ejecute hello "Install.sh" script toodeploy Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d572-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="8d572-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8d572-169">Next steps</span></span>

* [<span data-ttu-id="8d572-170">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8d572-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
