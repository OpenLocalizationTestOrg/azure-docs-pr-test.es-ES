---
title: aaaCreate su primera microservicio confiable de Azure en Java | Documentos de Microsoft
description: "Introducción toocreating una aplicación de Microsoft Azure Service Fabric con servicios y sin estado."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="eb6f1-103">Introducción a los servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="eb6f1-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb6f1-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="eb6f1-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="eb6f1-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="eb6f1-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="eb6f1-106">En este artículo se explica conceptos básicos de hello de servicios de Azure Service Fabric confiable y le guía a través de la creación e implementación de una aplicación de servicio confiable simple escrita en Java.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="eb6f1-107">Este vídeo de Microsoft Virtual Academy también muestra cómo toocreate un servicio confiable sin estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="eb6f1-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="eb6f1-108">Instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="eb6f1-108">Installation and setup</span></span>
<span data-ttu-id="eb6f1-109">Antes de empezar, asegúrese de que tiene el entorno de desarrollo de Service Fabric Hola configurado en su equipo.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="eb6f1-110">Si necesita tooset, configúrelo, vaya demasiado[introducción en Mac](service-fabric-get-started-mac.md) o [introducción en Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="eb6f1-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="eb6f1-111">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="eb6f1-111">Basic concepts</span></span>
<span data-ttu-id="eb6f1-112">tooget a trabajar con servicios de confianza, solo se necesita toounderstand algunos conceptos básicos:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="eb6f1-113">**Tipo de servicio**: se trata de la implementación del servicio.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="eb6f1-114">Se define mediante la clase hello escribir que extiende `StatelessService` y cualquier otro código o a las dependencias que se usan en él, junto con un nombre y un número de versión.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="eb6f1-115">**Con el nombre de instancia de servicio**: toorun su servicio, crear instancias con nombre de su tipo de servicio, mucho como crear instancias de objeto de un tipo de clase.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="eb6f1-116">Las instancias de servicio son, en realidad, creaciones de instancias de objetos de la clase de servicio que escribe.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="eb6f1-117">**Host de servicio**: Hola instancias de servicio crear necesidad toorun dentro de un host con nombre.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="eb6f1-118">host de servicio de Hello es simplemente un proceso donde se pueden ejecutar instancias de su servicio.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="eb6f1-119">**Registro de servicio**: el registro incluye todos los elementos.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="eb6f1-120">Hello service type debe estar registrado con hello Service Fabric en tiempo de ejecución en un servicio de instancias de host tooallow Service Fabric toocreate del mismo toorun.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="eb6f1-121">Creación de un servicio sin estado</span><span class="sxs-lookup"><span data-stu-id="eb6f1-121">Create a stateless service</span></span>
<span data-ttu-id="eb6f1-122">Comience por crear una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="eb6f1-123">Hola servicio SDK de tejido para Linux incluye un Yeoman scaffolding de hello tooprovide de generador para una aplicación de Service Fabric con un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="eb6f1-124">Comience ejecutando Hola siguientes Yeoman de comandos:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="eb6f1-125">Siga Hola instrucciones toocreate una **confiable servicio sin estado**.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="eb6f1-126">Para este tutorial, hello y aplicación de hello de nombre "HelloWorldApplication" servicio "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="eb6f1-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="eb6f1-127">resultado de Hello incluye directorios para hello `HelloWorldApplication` y `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="eb6f1-128">Implementar el servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="eb6f1-128">Implement hello service</span></span>
<span data-ttu-id="eb6f1-129">Abra **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="eb6f1-130">Esta clase define el tipo de servicio de Hola y puede ejecutar cualquier código.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="eb6f1-131">API de servicio de Hello proporciona dos puntos de entrada para el código:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="eb6f1-132">Un método de punto de entrada de extremo abierto, llamado `runAsync()`, donde puede comenzar a ejecutar cualquier carga de trabajo, incluidas cargas de trabajo de proceso de larga duración.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="eb6f1-133">Un punto de entrada de comunicación en el que puede conectar su pila de comunicación preferida.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="eb6f1-134">Aquí es donde puede empezar a recibir las solicitudes de usuarios y otros servicios.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="eb6f1-135">En este tutorial, nos centramos en hello `runAsync()` método de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="eb6f1-136">Aquí es donde puede comenzar a ejecutar el código de inmediato.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="eb6f1-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="eb6f1-137">RunAsync</span></span>
<span data-ttu-id="eb6f1-138">plataforma de Hello llama a este método cuando una instancia de un servicio es tooexecute colocado y listo.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="eb6f1-139">Para un servicio sin estado, que simplemente significa que cuando se abre la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="eb6f1-140">Un token de cancelación se proporciona toocoordinate cuando la instancia de servicio necesita toobe cerrado.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="eb6f1-141">En Service Fabric, este ciclo de apertura y cierre de una instancia de servicio puede producir varias veces más vida Hola Hola como un todo.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="eb6f1-142">Esto puede ocurrir por diversos motivos, incluidos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="eb6f1-143">sistema de Hello mueve las instancias de servicio para equilibrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="eb6f1-144">Se producen errores en el código.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-144">Faults occur in your code.</span></span>
* <span data-ttu-id="eb6f1-145">se actualiza la aplicación Hello o sistema.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="eb6f1-146">hardware subyacente Hola experimenta una interrupción inesperada.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="eb6f1-147">Esta orquestación está administrada por Service Fabric tookeep el servicio de alta disponibilidad y equilibrado correctamente.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="eb6f1-148">`runAsync()` no debe bloquearse de forma sincrónica.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="eb6f1-149">La implementación de Coredispatcher debe devolver un toocontinue de CompletableFuture tooallow hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="eb6f1-150">Si la carga de trabajo necesita tooimplement una tarea de ejecución prolongada que debe realizarse dentro de Hola CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="eb6f1-151">Cancelación</span><span class="sxs-lookup"><span data-stu-id="eb6f1-151">Cancellation</span></span>
<span data-ttu-id="eb6f1-152">Cancelación de la carga de trabajo es un esfuerzo cooperativo organizado Hola proporcionada el token de cancelación.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="eb6f1-153">Hola sistema espera que la tarea tooend (de realización correcta, cancelación o error) antes de que pase.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="eb6f1-154">Es importante toohonor Hola cancelación token, finalizar cualquier trabajo y salir `runAsync()` lo más rápido posible al sistema de hello solicita la cancelación.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="eb6f1-155">Hello ejemplo siguiente se muestra cómo toohandle un evento de cancelación:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="eb6f1-156">Registro de servicios</span><span class="sxs-lookup"><span data-stu-id="eb6f1-156">Service registration</span></span>
<span data-ttu-id="eb6f1-157">Tipos de servicio deben registrarse con el tiempo de ejecución de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="eb6f1-158">tipo de servicio de Hola se define en hello `ServiceManifest.xml` y la clase de servicio que implementa `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="eb6f1-159">Registro del servicio se realiza en el punto de entrada principal del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="eb6f1-160">En este ejemplo, Hola proceso en el punto de entrada principal sea `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="eb6f1-161">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="eb6f1-161">Run hello application</span></span>

<span data-ttu-id="eb6f1-162">Hola Yeoman scaffolding incluye un gradle script toobuild Hola aplicación y bash scripts toodeploy y quitar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="eb6f1-163">aplicación de hello toorun, primera aplicación Hola de compilación con gradle:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="eb6f1-164">Esto crea un paquete de aplicación de Service Fabric que puede implementarse mediante la CLI de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="eb6f1-165">Implementación con la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb6f1-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="eb6f1-166">script de "Install.sh" Hello contiene Hola necesarios Service Fabric CLI comandos toodeploy Hola paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="eb6f1-167">Ejecute la aplicación de "Install.sh" script toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="eb6f1-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb6f1-168">Next steps</span></span>

* [<span data-ttu-id="eb6f1-169">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb6f1-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
