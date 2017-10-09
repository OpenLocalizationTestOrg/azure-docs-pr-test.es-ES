---
title: "una aplicación de Java de Azure Service Fabric actores confiable en Linux aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate e implementar una aplicación de Java Service Fabric actores confiable en cinco minutos."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="c0363-103">Creación de su primera aplicación Java de Reliable Actors de Service Fabric en Linux</span><span class="sxs-lookup"><span data-stu-id="c0363-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0363-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="c0363-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="c0363-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="c0363-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="c0363-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="c0363-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="c0363-107">Este inicio rápido le ayuda a crear su primera aplicación Java de Azure Service Fabric en un entorno de desarrollo de Linux en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c0363-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="c0363-108">Cuando haya terminado, tendrá una aplicación de servicio de single Java simple que se ejecuta en clúster de desarrollo local Hola.</span><span class="sxs-lookup"><span data-stu-id="c0363-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c0363-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c0363-109">Prerequisites</span></span>
<span data-ttu-id="c0363-110">Antes de empezar a instalar Hola SDK del servicio de Fabric, Hola CLI de tejido de servicio y la instalación de un clúster de desarrollo en su [entorno de desarrollo de Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c0363-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="c0363-111">Si usa Mac OS X, puede [configurar un entorno de desarrollo de Linux en una máquina virtual mediante Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="c0363-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="c0363-112">También deberá hello tooinstall [Service Fabric CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c0363-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="c0363-113">Instalar y configurar los generadores de Hola para Java</span><span class="sxs-lookup"><span data-stu-id="c0363-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="c0363-114">Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear una aplicación Java de Service Fabric desde el terminal mediante el generador de plantillas Yeoman.</span><span class="sxs-lookup"><span data-stu-id="c0363-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="c0363-115">Siga estos pasos hello tooensure que tiene generador de plantilla yeoman Hola Service Fabric para Java trabajar en su equipo.</span><span class="sxs-lookup"><span data-stu-id="c0363-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="c0363-116">Instalación de nodejs y NPM en la máquina</span><span class="sxs-lookup"><span data-stu-id="c0363-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="c0363-117">Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM</span><span class="sxs-lookup"><span data-stu-id="c0363-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="c0363-118">Instalar el generador de aplicaciones de servicio Fabric Yeo Java Hola desde NPM</span><span class="sxs-lookup"><span data-stu-id="c0363-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="c0363-119">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c0363-119">Create hello application</span></span>
<span data-ttu-id="c0363-120">Una aplicación de Service Fabric contiene uno o varios servicios, cada uno con un rol específico en la entrega de la funcionalidad de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c0363-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="c0363-121">Generador de Hola que instaló en la última sección de hello, resulta fácil toocreate su primer servicio y tooadd más adelante.</span><span class="sxs-lookup"><span data-stu-id="c0363-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="c0363-122">También puede crear, compilar e implementar aplicaciones Java de Service Fabric mediante un complemento para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c0363-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="c0363-123">Consulte [Creación e implementación de la primera aplicación Java mediante Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="c0363-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="c0363-124">Para este tutorial, utilice Yeoman toocreate una aplicación con un único servicio que almacena y obtiene un valor de contador.</span><span class="sxs-lookup"><span data-stu-id="c0363-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="c0363-125">En un terminal, escriba ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="c0363-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="c0363-126">Asigne un nombre a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0363-126">Name your application.</span></span>
3. <span data-ttu-id="c0363-127">Elegir tipo de Hola de su primer servicio y asígnele el nombre.</span><span class="sxs-lookup"><span data-stu-id="c0363-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="c0363-128">En este tutorial, elija un servicio de Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="c0363-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="c0363-129">Para obtener más información acerca de hello otros tipos de servicios, consulte [Service Fabric información general del modelo de programación](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="c0363-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="c0363-130">![Generador Yeoman de Service Fabric para Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="c0363-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="c0363-131">Compilar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c0363-131">Build hello application</span></span>
<span data-ttu-id="c0363-132">plantillas de servicio tejido Yeoman Hola incluyen un script de compilación para [Gradle](https://gradle.org/), que puede usar toobuild aplicación Hola Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="c0363-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="c0363-133">Las dependencias de Java de Service Fabric se recuperan de Maven.</span><span class="sxs-lookup"><span data-stu-id="c0363-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="c0363-134">toobuild y trabajo en aplicaciones de Java de tejido de servicio de hello, deberá tooensure que tiene JDK y Gradle instalados.</span><span class="sxs-lookup"><span data-stu-id="c0363-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="c0363-135">Si aún no se ha instalado, puede ejecutar Hola siguientes tooinstall JDK(openjdk-8-jdk) y Gradle -</span><span class="sxs-lookup"><span data-stu-id="c0363-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="c0363-136">toobuild y el paquete de aplicación hello, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0363-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="c0363-137">Implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c0363-137">Deploy hello application</span></span>
<span data-ttu-id="c0363-138">Una vez que se compila la aplicación hello, puede implementarlo toohello local del clúster.</span><span class="sxs-lookup"><span data-stu-id="c0363-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="c0363-139">Conectar el clúster de Service Fabric local toohello.</span><span class="sxs-lookup"><span data-stu-id="c0363-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="c0363-140">Ejecutar script de instalación de hello en hello plantilla toocopy aplicación hello empaquetar almacén de imágenes del clúster toohello, registrar el tipo de aplicación hello y cree una instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c0363-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="c0363-141">Implementar aplicación Hola integrada es Hola igual que cualquier otra aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0363-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="c0363-142">Consulte la documentación de hello en [administrar una aplicación de Service Fabric con hello CLI de tejido de servicio](service-fabric-application-lifecycle-sfctl.md) para obtener instrucciones detalladas.</span><span class="sxs-lookup"><span data-stu-id="c0363-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="c0363-143">Comandos de toothese parámetros pueden encontrarse en los manifiestos de hello generado dentro del paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c0363-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="c0363-144">Una vez que se ha implementado la aplicación hello, abra un explorador y vaya a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) en [http://localhost:19080/explorador](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="c0363-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="c0363-145">A continuación, expanda hello **aplicaciones** nodo y observe que ahora hay una entrada para el tipo de aplicación y otro para hello primera instancia de ese tipo.</span><span class="sxs-lookup"><span data-stu-id="c0363-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="c0363-146">Inicie el cliente de prueba de Hola y realizar una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="c0363-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="c0363-147">Actores no hacen nada por sí solas, que requieren otro toosend de servicio o cliente mensajes de ellos.</span><span class="sxs-lookup"><span data-stu-id="c0363-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="c0363-148">plantilla de actor Hola incluye un script de prueba simple que puede usar con el servicio de actor hello toointeract.</span><span class="sxs-lookup"><span data-stu-id="c0363-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="c0363-149">Ejecutar script de Hola con hello inspección utilidad toosee Hola obtenidos del servicio de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="c0363-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="c0363-150">script de prueba de Hello llama hello `setCountAsync()` llamadas de método en hello actor tooincrement un contador, hello `getCountAsync()` método en hello actor tooget Hola nuevo valor del contador y muestra ese valor toohello consola.</span><span class="sxs-lookup"><span data-stu-id="c0363-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="c0363-151">En el Explorador de Service Fabric, busque Hola nodo hospedaje Hola réplica principal de servicio de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="c0363-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="c0363-152">En la captura de pantalla de hello siguiente, es el nodo 3.</span><span class="sxs-lookup"><span data-stu-id="c0363-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="c0363-153">identificadores de réplica de servicio principal de Hello operaciones lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="c0363-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="c0363-154">Cambios de estado de servicio, a continuación, se replicaron toohello réplicas secundarias, ejecutar en los nodos 0 y 1 en la siguiente captura de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="c0363-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Buscar la réplica principal de hello en el Explorador de Service Fabric][sfx-primary]

3. <span data-ttu-id="c0363-156">En **nodos**, haga clic en el nodo de Hola que encontró en el paso anterior de hello, a continuación, seleccione **desactivar (reiniciar)** desde el menú de acciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0363-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="c0363-157">Esta acción reinicia nodo Hola ejecute réplica de servicio principal de Hola y fuerza una tooone de conmutación por error de réplicas secundarias Hola ejecuta en otro nodo.</span><span class="sxs-lookup"><span data-stu-id="c0363-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="c0363-158">Esa réplica secundaria es tooprimary promocionada, otra réplica secundaria se crea en un nodo diferente y réplica principal de hello inicia las operaciones de lectura/escritura de tootake.</span><span class="sxs-lookup"><span data-stu-id="c0363-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="c0363-159">Cuando se reinicie el nodo de hello, ver salida de hello de cliente de prueba de hello y observe que ese contador Hola continúa tooincrement a pesar de hello conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="c0363-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="c0363-160">Quitar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c0363-160">Remove hello application</span></span>
<span data-ttu-id="c0363-161">Usar script de desinstalación de hello proporcionado en la instancia de la aplicación de hello plantilla toodelete hello, anular el registro del paquete de aplicación Hola y quitar el paquete de aplicación Hola del clúster de hello almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="c0363-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="c0363-162">En el Explorador de Service Fabric verá que aplicación hello y el tipo de aplicación ya no aparecen en hello **aplicaciones** nodo.</span><span class="sxs-lookup"><span data-stu-id="c0363-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="c0363-163">Bibliotecas de Java de Service Fabric en Maven</span><span class="sxs-lookup"><span data-stu-id="c0363-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="c0363-164">Las bibliotecas de Java de Service Fabric han sido hospedadas en Maven.</span><span class="sxs-lookup"><span data-stu-id="c0363-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="c0363-165">También puede agregar dependencias de Hola Hola ``pom.xml`` o ``build.gradle`` de las bibliotecas de Java de tejido de servicio de proyectos toouse desde **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="c0363-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="c0363-166">Actores</span><span class="sxs-lookup"><span data-stu-id="c0363-166">Actors</span></span>

<span data-ttu-id="c0363-167">Compatibilidad con Reliable Actor de Service Fabric para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0363-167">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="c0363-168">Services</span><span class="sxs-lookup"><span data-stu-id="c0363-168">Services</span></span>

<span data-ttu-id="c0363-169">Compatibilidad con el servicio sin estado de Service Fabric para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0363-169">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="c0363-170">Otros</span><span class="sxs-lookup"><span data-stu-id="c0363-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="c0363-171">Transporte</span><span class="sxs-lookup"><span data-stu-id="c0363-171">Transport</span></span>

<span data-ttu-id="c0363-172">Compatibilidad de la capa de transporte para aplicaciones Java de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0363-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="c0363-173">No es necesario tooexplicitly agregar esta dependencia tooyour Actor confiable o aplicaciones de servicio, a menos que se programan en la capa de transporte de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0363-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="c0363-174">Compatibilidad con Fabric</span><span class="sxs-lookup"><span data-stu-id="c0363-174">Fabric support</span></span>

<span data-ttu-id="c0363-175">Compatibilidad de nivel de sistema para Service Fabric, que se comunica en tiempo de ejecución de toonative Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0363-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="c0363-176">No es necesario tooexplicitly agregar esta dependencia tooyour Actor confiable o las aplicaciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="c0363-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="c0363-177">Esto obtiene capturan automáticamente desde Maven, al incluir Hola otras dependencias anteriores.</span><span class="sxs-lookup"><span data-stu-id="c0363-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="c0363-178">Migrar toobe de aplicaciones de Java de tejido de servicio anterior utilizado con Maven</span><span class="sxs-lookup"><span data-stu-id="c0363-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="c0363-179">Recientemente se han transferido bibliotecas de Java de tejido de servicio desde el repositorio de tooMaven del SDK de Java del tejido de servicio.</span><span class="sxs-lookup"><span data-stu-id="c0363-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="c0363-180">Mientras que las aplicaciones nuevas de Hola que genere con Yeoman o Eclipse, generará más reciente de los proyectos actualizados (que serán capaz de toowork con Maven), puede actualizar su tejido de servicio existente sin estado o las aplicaciones de Java de actor, que usaba Hola servicio Tejido SDK de Java de versiones anteriores, las dependencias de Java de tejido de servicio de Hola de toouse de Maven.</span><span class="sxs-lookup"><span data-stu-id="c0363-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="c0363-181">Siga los pasos de hello mencionados [aquí](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure la aplicación anterior funcione con Maven.</span><span class="sxs-lookup"><span data-stu-id="c0363-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0363-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0363-182">Next steps</span></span>

* [<span data-ttu-id="c0363-183">Creación de la primera aplicación Java de Service Fabric en Linux</span><span class="sxs-lookup"><span data-stu-id="c0363-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="c0363-184">Más información acerca de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="c0363-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="c0363-185">Interactuar con los clústeres de Service Fabric mediante Hola CLI de tejido de servicio</span><span class="sxs-lookup"><span data-stu-id="c0363-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="c0363-186">Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="c0363-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="c0363-187">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c0363-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
