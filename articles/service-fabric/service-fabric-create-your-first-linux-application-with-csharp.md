---
title: "aaaCreate su primera aplicación de Azure microservicios en Linux con C# | Documentos de Microsoft"
description: "Creación e implementación de una aplicación de Service Fabric con C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="a8769-103">Creación de la primera aplicación de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a8769-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8769-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="a8769-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="a8769-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="a8769-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="a8769-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="a8769-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="a8769-107">Service Fabric ofrece SDK para compilar servicios en Linux tanto en .NET Core como Java.</span><span class="sxs-lookup"><span data-stu-id="a8769-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="a8769-108">En este tutorial, veremos cómo toocreate una aplicación para Linux y generar un servicio usando C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="a8769-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8769-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a8769-109">Prerequisites</span></span>
<span data-ttu-id="a8769-110">Antes de empezar, asegúrese de [configurar el entorno de desarrollo Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a8769-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="a8769-111">Si usa Mac OS X, puede [configurar un entorno one-box de Linux en una máquina virtual mediante Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="a8769-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="a8769-112">También deberá tooinstall hello [CLI de tejido de servicio](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a8769-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="a8769-113">Instale y configure los generadores de Hola de CSharp</span><span class="sxs-lookup"><span data-stu-id="a8769-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="a8769-114">Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear una aplicación de CSharp de Service Fabric desde el terminal mediante el generador de plantillas Yeoman.</span><span class="sxs-lookup"><span data-stu-id="a8769-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="a8769-115">Siga estos pasos hello tooensure que tendrá el generador de plantilla yeoman de Service Fabric Hola para CSharp trabajar en su equipo.</span><span class="sxs-lookup"><span data-stu-id="a8769-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="a8769-116">Instalación de nodejs y NPM en la máquina</span><span class="sxs-lookup"><span data-stu-id="a8769-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="a8769-117">Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM</span><span class="sxs-lookup"><span data-stu-id="a8769-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="a8769-118">Instalar el generador de aplicaciones de servicio Fabric Yeo Java Hola desde NPM</span><span class="sxs-lookup"><span data-stu-id="a8769-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="a8769-119">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="a8769-119">Create hello application</span></span>
<span data-ttu-id="a8769-120">Una aplicación de Service Fabric puede contener uno o varios servicios, cada uno con un rol específico en la entrega de la funcionalidad de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a8769-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="a8769-121">Hola Service Fabric [Yeoman](http://yeoman.io/) generador para CSharp, que instala en el último paso, resulta fácil toocreate su primer servicio y tooadd más adelante.</span><span class="sxs-lookup"><span data-stu-id="a8769-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="a8769-122">Vamos a usar Yeoman toocreate una aplicación con un único servicio.</span><span class="sxs-lookup"><span data-stu-id="a8769-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="a8769-123">En un terminal, escriba Hola después toostart comando compilar scaffolding hello:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="a8769-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="a8769-124">Asigne un nombre a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a8769-124">Name your application.</span></span>
3. <span data-ttu-id="a8769-125">Elegir tipo de Hola de su primer servicio y asígnele el nombre.</span><span class="sxs-lookup"><span data-stu-id="a8769-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="a8769-126">Para fines de Hola de este tutorial, elegimos un servicio de Actor confiable.</span><span class="sxs-lookup"><span data-stu-id="a8769-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Generador Yeoman de Service Fabric para C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="a8769-128">Para obtener más información acerca de las opciones de hello, consulte [Service Fabric información general del modelo de programación](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="a8769-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="a8769-129">Compilar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="a8769-129">Build hello application</span></span>
<span data-ttu-id="a8769-130">las plantillas de servicio tejido Yeoman Hola incluyen un script de compilación que puede usar toobuild aplicación Hola Hola terminal (después de navegar toohello carpeta de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="a8769-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="a8769-131">Implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="a8769-131">Deploy hello application</span></span>

<span data-ttu-id="a8769-132">Una vez que se compila la aplicación hello, puede implementarlo toohello local del clúster.</span><span class="sxs-lookup"><span data-stu-id="a8769-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="a8769-133">Conectar el clúster de Service Fabric local toohello.</span><span class="sxs-lookup"><span data-stu-id="a8769-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="a8769-134">Ejecutar script de instalación de hello en hello plantilla toocopy aplicación hello empaquetar almacén de imágenes del clúster toohello, registrar el tipo de aplicación hello y cree una instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a8769-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="a8769-135">Implementar aplicación Hola integrada es Hola igual que cualquier otra aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a8769-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="a8769-136">Consulte la documentación de hello en [administrar una aplicación de Service Fabric con hello CLI de tejido de servicio](service-fabric-application-lifecycle-sfctl.md) para obtener instrucciones detalladas.</span><span class="sxs-lookup"><span data-stu-id="a8769-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="a8769-137">Comandos de toothese parámetros pueden encontrarse en los manifiestos de hello generado dentro del paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="a8769-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="a8769-138">Una vez que se ha implementado la aplicación hello, abra un explorador y vaya a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) en [http://localhost:19080/explorador](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="a8769-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="a8769-139">A continuación, expanda hello **aplicaciones** nodo y observe que ahora hay una entrada para el tipo de aplicación y otro para hello primera instancia de ese tipo.</span><span class="sxs-lookup"><span data-stu-id="a8769-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="a8769-140">Inicie el cliente de prueba de Hola y realizar una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="a8769-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="a8769-141">Los proyectos de actor no hacen nada por sí solos.</span><span class="sxs-lookup"><span data-stu-id="a8769-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="a8769-142">Requieren otro toosend de servicio o cliente mensajes de ellos.</span><span class="sxs-lookup"><span data-stu-id="a8769-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="a8769-143">plantilla de actor Hola incluye un script de prueba simple que puede usar con el servicio de actor hello toointeract.</span><span class="sxs-lookup"><span data-stu-id="a8769-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="a8769-144">Ejecutar script de Hola con hello inspección utilidad toosee Hola obtenidos del servicio de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="a8769-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="a8769-145">En Service Fabric Explorer, busque el nodo que hospeda la réplica principal de hello para el servicio de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="a8769-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="a8769-146">En la captura de pantalla de hello siguiente, es el nodo 3.</span><span class="sxs-lookup"><span data-stu-id="a8769-146">In hello screenshot below, it is node 3.</span></span>

    ![Buscar la réplica principal de hello en el Explorador de Service Fabric][sfx-primary]
3. <span data-ttu-id="a8769-148">Haga clic en el nodo de Hola que encontró en el paso anterior de hello, a continuación, seleccione **desactivar (reiniciar)** desde el menú de acciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8769-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="a8769-149">Esta acción reinicia un nodo en el clúster local forzar una réplica secundaria de conmutación por error tooa ejecuta en otro nodo.</span><span class="sxs-lookup"><span data-stu-id="a8769-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="a8769-150">Al realizar esta acción, paga salida toohello de atención de cliente de prueba de hello y observe que ese contador Hola continúa tooincrement a pesar de hello conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="a8769-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="a8769-151">Agregar más servicios tooan existente aplicación</span><span class="sxs-lookup"><span data-stu-id="a8769-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="a8769-152">tooadd otra aplicación de tooan de servicio ya creado mediante `yo`, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a8769-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="a8769-153">Cambiar toohello raíz del directorio de aplicación existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8769-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="a8769-154">Por ejemplo, `cd ~/YeomanSamples/MyApplication`si `MyApplication` es aplicación Hola creado por Yeoman.</span><span class="sxs-lookup"><span data-stu-id="a8769-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="a8769-155">Ejecute `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="a8769-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="a8769-156">Migrar desde too.csproj project.json</span><span class="sxs-lookup"><span data-stu-id="a8769-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="a8769-157">Ejecutando 'dotnet migrar' en el directorio raíz del proyecto migrará el formato de todos los hello project.json toocsproj.</span><span class="sxs-lookup"><span data-stu-id="a8769-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="a8769-158">Actualización Hola referencias del proyecto en consecuencia toocsproj en archivos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="a8769-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="a8769-159">Actualizar archivos toocsproj nombres de archivo de proyecto de hello en build.sh.</span><span class="sxs-lookup"><span data-stu-id="a8769-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8769-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8769-160">Next steps</span></span>

* [<span data-ttu-id="a8769-161">Más información acerca de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="a8769-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="a8769-162">Interactuar con los clústeres de Service Fabric usando Hola CLI de tejido de servicio</span><span class="sxs-lookup"><span data-stu-id="a8769-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="a8769-163">Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="a8769-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="a8769-164">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a8769-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
