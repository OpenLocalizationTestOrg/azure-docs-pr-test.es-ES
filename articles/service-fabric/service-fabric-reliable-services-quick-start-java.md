---
title: "Creación del primer microservicio de Azure confiable en Java | Microsoft Docs"
description: "Introducción a la creación de una aplicación de Service Fabric de Microsoft Azure mediante servicios con y sin estado."
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
ms.openlocfilehash: 1ebabe4844732412e04bab8c277f7ebbc4a5737c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="4cc59-103">Introducción a los servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="4cc59-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4cc59-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="4cc59-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="4cc59-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="4cc59-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="4cc59-106">En este artículo se explican los conceptos básicos de Reliable Services de Azure Service Fabric, además de ofrecer orientación sobre cómo crear e implementar una aplicación de Reliable Service sencilla escrita en Java.</span><span class="sxs-lookup"><span data-stu-id="4cc59-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="4cc59-107">Este vídeo de Microsoft Virtual Academy también muestra cómo crear un servicio confiable sin estado: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="4cc59-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="4cc59-108">Instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="4cc59-108">Installation and setup</span></span>
<span data-ttu-id="4cc59-109">Antes de comenzar, asegúrese de que el entorno de desarrollo de Service Fabric está configurado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4cc59-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="4cc59-110">Si tiene que configurarlo, consulte la [introducción a Mac](service-fabric-get-started-mac.md) o a la [introducción a Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4cc59-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="4cc59-111">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="4cc59-111">Basic concepts</span></span>
<span data-ttu-id="4cc59-112">Para empezar a trabajar con Reliable Services, solo es necesario comprender cuatro conceptos básicos:</span><span class="sxs-lookup"><span data-stu-id="4cc59-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="4cc59-113">**Tipo de servicio**: se trata de la implementación del servicio.</span><span class="sxs-lookup"><span data-stu-id="4cc59-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="4cc59-114">Se ha definido a través de la clase que escribe y que extiende `StatelessService` y cualquier otro código y dependencias utilizados, junto con un nombre y un número de versión.</span><span class="sxs-lookup"><span data-stu-id="4cc59-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="4cc59-115">**Instancia de servicio con nombre**: para ejecutar su servicio, debe crear instancias con nombre de su tipo de servicio, de forma muy similar a la creación de instancias de objetos de un tipo de clase.</span><span class="sxs-lookup"><span data-stu-id="4cc59-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="4cc59-116">Las instancias de servicio son, en realidad, creaciones de instancias de objetos de la clase de servicio que escribe.</span><span class="sxs-lookup"><span data-stu-id="4cc59-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="4cc59-117">**Host de servicio**: las instancias de servicio con nombre que cree deben ejecutarse dentro de un host.</span><span class="sxs-lookup"><span data-stu-id="4cc59-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="4cc59-118">El host del servicio es simplemente un proceso donde se pueden ejecutar instancias de su servicio.</span><span class="sxs-lookup"><span data-stu-id="4cc59-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="4cc59-119">**Registro de servicio**: el registro incluye todos los elementos.</span><span class="sxs-lookup"><span data-stu-id="4cc59-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="4cc59-120">El tipo de servicio debe registrarse con Service Fabric en tiempo de ejecución en un host de servicio para permitir que Service Fabric cree instancias de él para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="4cc59-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="4cc59-121">Creación de un servicio sin estado</span><span class="sxs-lookup"><span data-stu-id="4cc59-121">Create a stateless service</span></span>
<span data-ttu-id="4cc59-122">Comience por crear una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4cc59-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="4cc59-123">El SDK de Service Fabric para Linux incluye un generador Yeoman para proporcionar el scaffolding para una aplicación de Service Fabric con un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="4cc59-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="4cc59-124">Comience ejecutando el siguiente comando de Yeoman:</span><span class="sxs-lookup"><span data-stu-id="4cc59-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="4cc59-125">Siga las instrucciones para crear un **servicio confiable sin estado**.</span><span class="sxs-lookup"><span data-stu-id="4cc59-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="4cc59-126">Para este tutorial, asigne el nombre "HelloWorldApplication" a la aplicación y "HelloWorld" al servicio.</span><span class="sxs-lookup"><span data-stu-id="4cc59-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="4cc59-127">El resultado incluirá los directorios para `HelloWorldApplication` y `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="4cc59-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

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

## <a name="implement-the-service"></a><span data-ttu-id="4cc59-128">Implementación del servicio</span><span class="sxs-lookup"><span data-stu-id="4cc59-128">Implement the service</span></span>
<span data-ttu-id="4cc59-129">Abra **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="4cc59-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="4cc59-130">Esta clase define el tipo de servicio y puede ejecutar cualquier código.</span><span class="sxs-lookup"><span data-stu-id="4cc59-130">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="4cc59-131">La API de servicios proporciona dos puntos de entrada para el código:</span><span class="sxs-lookup"><span data-stu-id="4cc59-131">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="4cc59-132">Un método de punto de entrada de extremo abierto, llamado `runAsync()`, donde puede comenzar a ejecutar cualquier carga de trabajo, incluidas cargas de trabajo de proceso de larga duración.</span><span class="sxs-lookup"><span data-stu-id="4cc59-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="4cc59-133">Un punto de entrada de comunicación en el que puede conectar su pila de comunicación preferida.</span><span class="sxs-lookup"><span data-stu-id="4cc59-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="4cc59-134">Aquí es donde puede empezar a recibir las solicitudes de usuarios y otros servicios.</span><span class="sxs-lookup"><span data-stu-id="4cc59-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="4cc59-135">En este tutorial, nos centraremos en el método de punto de entrada `runAsync()`.</span><span class="sxs-lookup"><span data-stu-id="4cc59-135">In this tutorial, we focus on the `runAsync()` entry point method.</span></span> <span data-ttu-id="4cc59-136">Aquí es donde puede comenzar a ejecutar el código de inmediato.</span><span class="sxs-lookup"><span data-stu-id="4cc59-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="4cc59-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="4cc59-137">RunAsync</span></span>
<span data-ttu-id="4cc59-138">La plataforma llama a este método cuando hay una instancia del servicio colocada y preparada para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="4cc59-138">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="4cc59-139">En el caso de un servicio sin estado, esto simplemente significa que la instancia de servicio está abierta.</span><span class="sxs-lookup"><span data-stu-id="4cc59-139">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="4cc59-140">Se proporciona un token de cancelación para coordinar cuando la instancia de servicio debe cerrarse.</span><span class="sxs-lookup"><span data-stu-id="4cc59-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="4cc59-141">En Service Fabric, este ciclo de apertura y cierre de una instancia de servicio puede producirse muchas veces durante la vigencia del servicio en su conjunto.</span><span class="sxs-lookup"><span data-stu-id="4cc59-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="4cc59-142">Esto puede ocurrir por diversos motivos, incluidos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="4cc59-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="4cc59-143">El sistema mueve las instancias de servicio para equilibrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="4cc59-143">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="4cc59-144">Se producen errores en el código.</span><span class="sxs-lookup"><span data-stu-id="4cc59-144">Faults occur in your code.</span></span>
* <span data-ttu-id="4cc59-145">Se actualiza la aplicación o el sistema.</span><span class="sxs-lookup"><span data-stu-id="4cc59-145">The application or system is upgraded.</span></span>
* <span data-ttu-id="4cc59-146">El hardware subyacente experimenta una interrupción.</span><span class="sxs-lookup"><span data-stu-id="4cc59-146">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="4cc59-147">Service Fabric es quien se encarga de la coordinación para mantener el servicio con una alta disponibilidad y correctamente equilibrado.</span><span class="sxs-lookup"><span data-stu-id="4cc59-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="4cc59-148">`runAsync()` no debe bloquearse de forma sincrónica.</span><span class="sxs-lookup"><span data-stu-id="4cc59-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="4cc59-149">La implementación de runAsync debe devolver un valor de CompletableFuture para que el tiempo de ejecución pueda continuar.</span><span class="sxs-lookup"><span data-stu-id="4cc59-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="4cc59-150">Si la carga de trabajo necesita implementar una tarea de ejecución prolongada, debe realizarse dentro de CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="4cc59-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="4cc59-151">Cancelación</span><span class="sxs-lookup"><span data-stu-id="4cc59-151">Cancellation</span></span>
<span data-ttu-id="4cc59-152">La cancelación de la carga de trabajo es un esfuerzo cooperativo organizado por el token de cancelación proporcionado.</span><span class="sxs-lookup"><span data-stu-id="4cc59-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="4cc59-153">El sistema esperará a que la tarea finalice (finalización correcta, cancelación o con errores) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="4cc59-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="4cc59-154">Es importante respetar el token de cancelación, finalizar cualquier trabajo y cerrar `runAsync()` lo antes posible cuando el sistema solicita la cancelación.</span><span class="sxs-lookup"><span data-stu-id="4cc59-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="4cc59-155">En el siguiente ejemplo le mostraremos cómo controlar un evento de cancelación:</span><span class="sxs-lookup"><span data-stu-id="4cc59-155">The following example demonstrates how to handle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
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

### <a name="service-registration"></a><span data-ttu-id="4cc59-156">Registro de servicios</span><span class="sxs-lookup"><span data-stu-id="4cc59-156">Service registration</span></span>
<span data-ttu-id="4cc59-157">Los tipos de servicio deben registrarse con el tiempo de ejecución de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4cc59-157">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="4cc59-158">El tipo de servicio se define en el archivo `ServiceManifest.xml` y la clase de servicio que implementa `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="4cc59-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="4cc59-159">El registro del servicio se realiza en el punto de entrada principal del proceso.</span><span class="sxs-lookup"><span data-stu-id="4cc59-159">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="4cc59-160">En este ejemplo, el punto de entrada principal del proceso es `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="4cc59-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

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

## <a name="run-the-application"></a><span data-ttu-id="4cc59-161">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4cc59-161">Run the application</span></span>

<span data-ttu-id="4cc59-162">El scaffolding de Yeoman incluye un script de Gradle para compilar la aplicación y scripts de Bash para implementarla y quitarla.</span><span class="sxs-lookup"><span data-stu-id="4cc59-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="4cc59-163">Para ejecutar la aplicación, primero hay que compilarla con Gradle:</span><span class="sxs-lookup"><span data-stu-id="4cc59-163">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="4cc59-164">Esto crea un paquete de aplicación de Service Fabric que puede implementarse mediante la CLI de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4cc59-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="4cc59-165">Implementación con la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4cc59-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="4cc59-166">El script install.sh contiene los comandos de la CLI de Service Fabric necesarios para implementar el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4cc59-166">The install.sh script contains the necessary Service Fabric CLI commands to deploy the application package.</span></span> <span data-ttu-id="4cc59-167">Ejecute el script install.sh para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4cc59-167">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="4cc59-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4cc59-168">Next steps</span></span>

* [<span data-ttu-id="4cc59-169">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4cc59-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
