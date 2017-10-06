---
title: aaaDeploy un tooAzure ejecutable existente Service Fabric | Documentos de Microsoft
description: "Tutorial sobre la implementación de clúster de Service Fabric tooa toopackage una aplicación existente como un ejecutable de invitado, por lo que puede ser"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="192f8-103">Implementar un tejido de invitado ejecutable tooService</span><span class="sxs-lookup"><span data-stu-id="192f8-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="192f8-104">Puede ejecutar cualquier tipo de código, como Node.js, Java o C++ en Azure Service Fabric como servicio.</span><span class="sxs-lookup"><span data-stu-id="192f8-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="192f8-105">Service Fabric hace referencia a tipos de toothese de servicios como archivos ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="192f8-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="192f8-106">Los ejecutables invitados se tratan por Service Fabric como servicios sin estado.</span><span class="sxs-lookup"><span data-stu-id="192f8-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="192f8-107">Por ello, se colocan en los nodos de un clúster, en función de la disponibilidad y otras métricas.</span><span class="sxs-lookup"><span data-stu-id="192f8-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="192f8-108">Este artículo se describe cómo toopackage e implementar un clúster de Service Fabric tooa ejecutable de invitado, mediante Visual Studio o una utilidad de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="192f8-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="192f8-109">En este artículo, se cubre Hola pasos toopackage un invitado ejecutable e impleméntela tooService tejido.</span><span class="sxs-lookup"><span data-stu-id="192f8-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="192f8-110">Ventajas de ejecutar un ejecutable invitado en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="192f8-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="192f8-111">Hay varias toorunning ventajas un ejecutable en un clúster de Service Fabric invitado:</span><span class="sxs-lookup"><span data-stu-id="192f8-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="192f8-112">Alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="192f8-112">High availability.</span></span> <span data-ttu-id="192f8-113">Las aplicaciones que se ejecutan en Service Fabric se crean con alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="192f8-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="192f8-114">Service Fabric garantiza que se están ejecutando instancias de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="192f8-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="192f8-115">Supervisión del estado.</span><span class="sxs-lookup"><span data-stu-id="192f8-115">Health monitoring.</span></span> <span data-ttu-id="192f8-116">La supervisión del mantenimiento de Service Fabric detecta si hay una aplicación en funcionamiento y proporciona información de diagnóstico si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="192f8-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="192f8-117">Administración del ciclo de vida de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="192f8-117">Application lifecycle management.</span></span> <span data-ttu-id="192f8-118">Además de proporcionar actualizaciones sin tiempo de inactividad, Service Fabric proporciona versión anterior de toohello de reversión automática si se produce un evento de mal estado notificado durante la actualización.</span><span class="sxs-lookup"><span data-stu-id="192f8-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="192f8-119">Densidad.</span><span class="sxs-lookup"><span data-stu-id="192f8-119">Density.</span></span> <span data-ttu-id="192f8-120">Puede ejecutar varias aplicaciones en un clúster, lo que elimina la necesidad de Hola de cada toorun de aplicación en su propio hardware.</span><span class="sxs-lookup"><span data-stu-id="192f8-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="192f8-121">Detectabilidad: Con REST se puede llamar a toofind del servicio de nomenclatura de tejido de servicio de hello otros servicios en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="192f8-122">Muestras</span><span class="sxs-lookup"><span data-stu-id="192f8-122">Samples</span></span>
* [<span data-ttu-id="192f8-123">Ejemplo para empaquetar e implementar un archivo ejecutable invitado</span><span class="sxs-lookup"><span data-stu-id="192f8-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="192f8-124">Ejemplo de dos archivos ejecutables (C# y nodejs) de invitado comunicarse a través del servicio de nomenclatura de hello con REST</span><span class="sxs-lookup"><span data-stu-id="192f8-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="192f8-125">Información general de los archivos de manifiesto de servicio y aplicación</span><span class="sxs-lookup"><span data-stu-id="192f8-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="192f8-126">Como parte de la implementación de un archivo ejecutable de invitado, resulta empaquetado de Service Fabric hello toounderstand útil y modelo de implementación tal y como se describe en [modelo de aplicación](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="192f8-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="192f8-127">modelo de empaquetado de Service Fabric Hola se basa en dos archivos XML: Hola manifiestos de aplicación y de servicio.</span><span class="sxs-lookup"><span data-stu-id="192f8-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="192f8-128">Hello definición de esquema para archivos ApplicationManifest.xml y ServiceManifest.xml hello está instalado una con Hola SDK del servicio de Fabric en *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="192f8-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="192f8-129">**Manifiesto de aplicación** manifiesto de aplicación de hello es aplicación de hello toodescribe usado.</span><span class="sxs-lookup"><span data-stu-id="192f8-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="192f8-130">Enumeran los servicios de Hola que lo componen y otros parámetros que son utilizado toodefine deben implementarse cómo uno o varios servicios, como el número de Hola de instancias.</span><span class="sxs-lookup"><span data-stu-id="192f8-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="192f8-131">En Service Fabric, una aplicación es una unidad de implementación y actualización.</span><span class="sxs-lookup"><span data-stu-id="192f8-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="192f8-132">Una aplicación se puede actualizar como una sola unidad donde se administran los posibles errores y reversiones.</span><span class="sxs-lookup"><span data-stu-id="192f8-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="192f8-133">Service Fabric garantiza que el proceso de actualización de hello es ya sea correcta, o bien, si se produce un error en la actualización de hello, no deje aplicación hello en un estado inestable o desconocido.</span><span class="sxs-lookup"><span data-stu-id="192f8-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="192f8-134">**Manifiesto del servicio** manifiesto del servicio Hola describe los componentes de Hola de un servicio.</span><span class="sxs-lookup"><span data-stu-id="192f8-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="192f8-135">Incluye datos, como el nombre de Hola y tipo de servicio y su código y configuración.</span><span class="sxs-lookup"><span data-stu-id="192f8-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="192f8-136">Hello manifiesto del servicio también incluye algunos parámetros adicionales que se pueden usar servicio de hello tooconfigure una vez que se implementa.</span><span class="sxs-lookup"><span data-stu-id="192f8-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="192f8-137">Estructura de archivo del paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="192f8-137">Application package file structure</span></span>
<span data-ttu-id="192f8-138">un tejido de aplicación tooService toodeploy, aplicación hello debe seguir una estructura de directorios predefinidos.</span><span class="sxs-lookup"><span data-stu-id="192f8-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="192f8-139">Hola aquí te mostramos un ejemplo de esa estructura.</span><span class="sxs-lookup"><span data-stu-id="192f8-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="192f8-140">Hola ApplicationPackageRoot contiene el archivo ApplicationManifest.xml hello que define la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="192f8-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="192f8-141">Un subdirectorio para cada servicio incluido en la aplicación hello es toocontain usado todos Hola artefactos que requiere el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="192f8-142">Estos subdirectorios son hello ServiceManifest.xml y, por lo general, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="192f8-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="192f8-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="192f8-143">*Code*.</span></span> <span data-ttu-id="192f8-144">Este directorio contiene el código del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="192f8-145">*Config*. Este directorio contiene un archivo Settings.xml (y otros archivos si es necesario) que puede tener acceso servicio de hello en Opciones de configuración específicas de tooretrieve en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="192f8-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="192f8-146">*Data*.</span><span class="sxs-lookup"><span data-stu-id="192f8-146">*Data*.</span></span> <span data-ttu-id="192f8-147">Se trata de un directorio adicional toostore local datos adicionales que Hola servicio puede necesitar.</span><span class="sxs-lookup"><span data-stu-id="192f8-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="192f8-148">Datos deben estar toostore utilizados efímera solo datos.</span><span class="sxs-lookup"><span data-stu-id="192f8-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="192f8-149">Service Fabric no copia ni replicar el directorio de datos de cambios toohello si servicio de hello necesita toobe reubicado (por ejemplo, durante la conmutación por error).</span><span class="sxs-lookup"><span data-stu-id="192f8-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="192f8-150">No tienes hello toocreate `config` y `data` directorios si no los necesite.</span><span class="sxs-lookup"><span data-stu-id="192f8-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="192f8-151">Empaquetado de un ejecutable existente</span><span class="sxs-lookup"><span data-stu-id="192f8-151">Package an existing executable</span></span>
<span data-ttu-id="192f8-152">Al empaquetar un archivo ejecutable de invitado, puede elegir cualquier toouse una plantilla de proyecto de Visual Studio o demasiado[crear paquete de aplicación Hola manualmente](#manually).</span><span class="sxs-lookup"><span data-stu-id="192f8-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="192f8-153">Con Visual Studio, Hola estructura del paquete de aplicación y se crean archivos de manifiesto por la nueva plantilla de proyecto Hola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="192f8-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="192f8-154">toopackage de manera más fácil de Hello un ejecutable a un servicio de Windows existente es toouse Visual Studio y en Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="192f8-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="192f8-155">Usar Visual Studio toopackage e implementar un archivo ejecutable existente</span><span class="sxs-lookup"><span data-stu-id="192f8-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="192f8-156">Visual Studio proporciona a un tejido de servicio toohelp de plantilla de servicio implementar un clúster de Service Fabric tooa ejecutable de invitado.</span><span class="sxs-lookup"><span data-stu-id="192f8-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="192f8-157">Seleccione **Archivo** > **Nuevo proyecto** y cree una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="192f8-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="192f8-158">Elija **invitado ejecutable** como plantilla de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="192f8-159">Haga clic en **examinar** carpeta de hello tooselect con el archivo ejecutable y rellene el resto de hello del servicio de hello parámetros toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="192f8-160">*Comportamiento del paquete de código*.</span><span class="sxs-lookup"><span data-stu-id="192f8-160">*Code Package Behavior*.</span></span> <span data-ttu-id="192f8-161">Puede ser conjunto toocopy todo el contenido de Hola de su toohello carpeta del proyecto de Visual Studio, lo que resulta útil si ejecutable hello no cambia.</span><span class="sxs-lookup"><span data-stu-id="192f8-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="192f8-162">Si espera toochange ejecutable hello y desea Hola capacidad toopick de nuevas compilaciones dinámicamente, puede elegir toolink toohello carpeta en su lugar.</span><span class="sxs-lookup"><span data-stu-id="192f8-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="192f8-163">Puede usar carpetas vinculadas al crear el proyecto de aplicación de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="192f8-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="192f8-164">Esto vincula la ubicación de origen toohello desde dentro de proyecto de hello, lo que permite invitado hello tooupdate ejecutable en su destino de origen.</span><span class="sxs-lookup"><span data-stu-id="192f8-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="192f8-165">Esas actualizaciones se convierten en parte del paquete de aplicación hello en la compilación.</span><span class="sxs-lookup"><span data-stu-id="192f8-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="192f8-166">*Programa* especifica Hola ejecutable que se debe ejecutar el servicio de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="192f8-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="192f8-167">*Argumentos* especifica los argumentos de Hola que deben pasarse a toohello ejecutable.</span><span class="sxs-lookup"><span data-stu-id="192f8-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="192f8-168">Puede ser una lista de parámetros con argumentos.</span><span class="sxs-lookup"><span data-stu-id="192f8-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="192f8-169">*WorkingFolder* especifica Hola el directorio de trabajo de proceso de Hola que queda toobe iniciado.</span><span class="sxs-lookup"><span data-stu-id="192f8-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="192f8-170">Puede especificar tres valores:</span><span class="sxs-lookup"><span data-stu-id="192f8-170">You can specify three values:</span></span>
     * <span data-ttu-id="192f8-171">`CodeBase`especifica ese directorio de trabajo de hello va toobe establecer directorio de código de toohello en el paquete de aplicación Hola (`Code` directory mostrado en hello delante de la estructura de archivos).</span><span class="sxs-lookup"><span data-stu-id="192f8-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="192f8-172">`CodePackage`especifica ese directorio de trabajo de hello va toobe establece toohello directorio raíz del paquete de aplicación Hola (`GuestService1Pkg` se muestra en hello delante de la estructura de archivos).</span><span class="sxs-lookup"><span data-stu-id="192f8-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="192f8-173">`Work`Especifica que los archivos de saludo se colocan en un subdirectorio denominado trabajo.</span><span class="sxs-lookup"><span data-stu-id="192f8-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="192f8-174">Asigne un nombre a su servicio y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="192f8-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="192f8-175">Si el servicio necesita un punto de conexión para la comunicación, ahora puede agregar Hola protocolo, puerto y archivo de tipo toohello ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="192f8-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="192f8-176">Por ejemplo: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="192f8-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="192f8-177">Ahora puede usar el paquete de Hola y acción de publicación en el grupo local mediante la depuración de la solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="192f8-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="192f8-178">Cuando esté listo, puede publicar clúster remoto de hello aplicación tooa o comprobar en el control de la solución toosource Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="192f8-179">Ir al final de toohello de este artículo toosee cómo tooview su servicio ejecutable invitado ejecuta en el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="192f8-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="192f8-180">Usar Yoeman toopackage e implementar un archivo ejecutable existente en Linux</span><span class="sxs-lookup"><span data-stu-id="192f8-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="192f8-181">procedimiento de Hola para crear e implementar un invitado ejecutable en Linux es Hola igual que implementar una aplicación de csharp o java.</span><span class="sxs-lookup"><span data-stu-id="192f8-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="192f8-182">En un terminal, escriba `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="192f8-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="192f8-183">Asigne un nombre a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="192f8-183">Name your application.</span></span>
3. <span data-ttu-id="192f8-184">El servicio de nombres y proporcionar detalles de hello como ruta de acceso del ejecutable hello y parámetros de Hola con que se debe invocar.</span><span class="sxs-lookup"><span data-stu-id="192f8-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="192f8-185">Yeoman crea un paquete de aplicación con la aplicación apropiada de Hola y archivos de manifiesto junto con instalación y desinstalación las secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="192f8-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="192f8-186">Empaquetado e implementación manuales de un archivo ejecutable existente</span><span class="sxs-lookup"><span data-stu-id="192f8-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="192f8-187">proceso de Hola de empaquetar manualmente un archivo ejecutable de invitado se basa en hello siguiendo los pasos generales:</span><span class="sxs-lookup"><span data-stu-id="192f8-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="192f8-188">Crear estructura de directorios de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="192f8-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="192f8-189">Agregar archivos de código y la configuración de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="192f8-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="192f8-190">Edite el archivo de manifiesto de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="192f8-191">Edite el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="192f8-192">Crear estructura de directorios del paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="192f8-192">Create hello package directory structure</span></span>
<span data-ttu-id="192f8-193">Puede iniciar mediante la creación de la estructura de directorios de hello, como se describe en hello anterior sección "Estructura de archivos de paquete de aplicación".</span><span class="sxs-lookup"><span data-stu-id="192f8-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="192f8-194">Agregar archivos de código y la configuración de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="192f8-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="192f8-195">Una vez haya creado la estructura de directorios de hello, puede agregar archivos de código y la configuración de la aplicación hello en los directorios de código y la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="192f8-196">También puede crear directorios adicionales o varios subdirectorios en los directorios de código o configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="192f8-197">Service Fabric un `xcopy` del contenido de Hola Hola directorio raíz de aplicación, así que no hay ningún toouse estructura predefinida aparte de la creación de dos directorios principales, código y configuración.</span><span class="sxs-lookup"><span data-stu-id="192f8-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="192f8-198">(Puede elegir diferentes nombres si lo desea.</span><span class="sxs-lookup"><span data-stu-id="192f8-198">(You can pick different names if you want.</span></span> <span data-ttu-id="192f8-199">Más detalles se encuentran en la sección siguiente Hola.)</span><span class="sxs-lookup"><span data-stu-id="192f8-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="192f8-200">Asegúrese de que incluye todos los archivos de Hola y dependencias que Hola necesidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="192f8-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="192f8-201">Service Fabric copia Hola contenido del paquete de aplicación hello en todos los nodos de clúster de Hola que Servicios de la aplicación hello están toobe continuo implementado.</span><span class="sxs-lookup"><span data-stu-id="192f8-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="192f8-202">paquete de Hello debe contener todo el código de hello que la aplicación hello necesita toorun.</span><span class="sxs-lookup"><span data-stu-id="192f8-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="192f8-203">No se da por supuesto que ya están instaladas las dependencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="192f8-204">Editar el archivo de manifiesto de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="192f8-204">Edit hello service manifest file</span></span>
<span data-ttu-id="192f8-205">Hola siguiente paso es tooedit Hola servicio archivo de manifiesto tooinclude Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="192f8-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="192f8-206">nombre de Hola Hola del tipo de servicio.</span><span class="sxs-lookup"><span data-stu-id="192f8-206">hello name of hello service type.</span></span> <span data-ttu-id="192f8-207">Se trata de un identificador que Service Fabric usa tooidentify un servicio.</span><span class="sxs-lookup"><span data-stu-id="192f8-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="192f8-208">Hola comando toouse toolaunch Hola la aplicación (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="192f8-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="192f8-209">Cualquier secuencia de comandos que necesita tooset toobe ejecutar una aplicación hello (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="192f8-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="192f8-210">Hello aquí te mostramos un ejemplo de un `ServiceManifest.xml` archivo:</span><span class="sxs-lookup"><span data-stu-id="192f8-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="192f8-211">Hola las secciones siguientes se pasa por partes diferentes de hello del archivo de Hola que necesita tooupdate.</span><span class="sxs-lookup"><span data-stu-id="192f8-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="192f8-212">Actualización de ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="192f8-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="192f8-213">Puede elegir cualquier nombre que desee para `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="192f8-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="192f8-214">se utiliza el valor de Hola Hola `ApplicationManifest.xml` tooidentify Hola servicio de archivos.</span><span class="sxs-lookup"><span data-stu-id="192f8-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="192f8-215">Especifique `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="192f8-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="192f8-216">Este atributo indica a Service Fabric que el servicio de Hola se basa en una aplicación independiente, por lo que todos los Service Fabric debe toodo es toolaunch como un proceso y supervisar su estado.</span><span class="sxs-lookup"><span data-stu-id="192f8-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="192f8-217">Actualización de CodePackage</span><span class="sxs-lookup"><span data-stu-id="192f8-217">Update CodePackage</span></span>
<span data-ttu-id="192f8-218">elemento de Hello CodePackage especifica la ubicación de hello (y versión) de código de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="192f8-219">Hola `Name` elemento es toospecify usado Hola nombre del directorio de Hola Hola paquete de aplicación que contiene el código de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="192f8-220">`CodePackage`También tiene hello `version` atributo.</span><span class="sxs-lookup"><span data-stu-id="192f8-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="192f8-221">Esto puede ser usado toospecify Hola versión de código de hello y también podrían ser usa código de servicio de tooupgrade hello mediante la infraestructura de administración de ciclo de vida de aplicación hello en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="192f8-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="192f8-222">Opcional: Actualización de SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="192f8-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="192f8-223">elemento de Hello SetupEntryPoint es toospecify usa cualquier archivo ejecutable o por lotes que se debe ejecutar antes de que se inicia el código de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="192f8-224">Es un paso opcional, por lo que no es necesario toobe incluyen si no hay ninguna inicialización necesaria.</span><span class="sxs-lookup"><span data-stu-id="192f8-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="192f8-225">Hola SetupEntryPoint se ejecuta cada vez que se reinicie el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="192f8-226">Hay solo un SetupEntryPoint, por lo que las secuencias de comandos del programa de instalación necesitan toobe agrupada en un archivo por lotes solo si el programa de instalación de la aplicación hello requiere varias secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="192f8-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="192f8-227">Hola SetupEntryPoint puede ejecutar cualquier tipo de archivo: archivos ejecutables, archivos por lotes y cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="192f8-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="192f8-228">Para más información, vea cómo [configurar SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="192f8-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="192f8-229">En el anterior ejemplo de Hola Hola SetupEntryPoint ejecuta un archivo por lotes denominado `LaunchConfig.cmd` decir Hola ubicada en `scripts` subdirectorio del directorio de código de hello (suponiendo que se establece el elemento de WorkingFolder de hello tooCodeBase).</span><span class="sxs-lookup"><span data-stu-id="192f8-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="192f8-230">Actualización de EntryPoint</span><span class="sxs-lookup"><span data-stu-id="192f8-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="192f8-231">Hola `EntryPoint` elemento de archivo de manifiesto de servicio de hello es toospecify usado cómo servicio de hello toolaunch.</span><span class="sxs-lookup"><span data-stu-id="192f8-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="192f8-232">Hola `ExeHost` elemento especifica ejecutable hello (y argumentos) que debe ser utilizado toolaunch Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="192f8-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="192f8-233">`Program`Especifica el nombre de hello del archivo ejecutable de Hola que debe iniciar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="192f8-234">`Arguments`Especifica los argumentos de Hola que deben pasarse toohello ejecutable.</span><span class="sxs-lookup"><span data-stu-id="192f8-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="192f8-235">Puede ser una lista de parámetros con argumentos.</span><span class="sxs-lookup"><span data-stu-id="192f8-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="192f8-236">`WorkingFolder`Especifica el directorio de trabajo de Hola de proceso de Hola que queda toobe iniciado.</span><span class="sxs-lookup"><span data-stu-id="192f8-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="192f8-237">Puede especificar tres valores:</span><span class="sxs-lookup"><span data-stu-id="192f8-237">You can specify three values:</span></span>
  * <span data-ttu-id="192f8-238">`CodeBase`especifica ese directorio de trabajo de hello va toobe establecer directorio de código de toohello en el paquete de aplicación Hola (`Code` directorio Hola delante de la estructura de archivos).</span><span class="sxs-lookup"><span data-stu-id="192f8-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="192f8-239">`CodePackage`especifica ese directorio de trabajo de hello va toobe establece toohello directorio raíz del paquete de aplicación Hola (`GuestService1Pkg` Hola delante de la estructura de archivos).</span><span class="sxs-lookup"><span data-stu-id="192f8-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="192f8-240">`Work`Especifica que los archivos de saludo se colocan en un subdirectorio denominado trabajo.</span><span class="sxs-lookup"><span data-stu-id="192f8-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="192f8-241">Hola WorkingFolder es directorio de trabajo correcto de tooset útil Hola para que las rutas de acceso relativas pueden utilizarse cualquier secuencias de comandos hello, aplicación o inicialización.</span><span class="sxs-lookup"><span data-stu-id="192f8-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="192f8-242">Actualización de puntos de conexión y registro mediante el servicio de nombres para la comunicación</span><span class="sxs-lookup"><span data-stu-id="192f8-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="192f8-243">En el anterior ejemplo de Hola Hola `Endpoint` elemento especifica los extremos de Hola que puede escuchar aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="192f8-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="192f8-244">En este ejemplo, hello aplicación Node.js escucha en http en el puerto 3000.</span><span class="sxs-lookup"><span data-stu-id="192f8-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="192f8-245">Además puede pedir toopublish Service Fabric este servicio de nombres de punto de conexión toohello para que otros servicios puedan detectar el servicio de toothis de dirección de punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="192f8-246">Esto le permite toobe toocommunicate capaz de entre los servicios que son ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="192f8-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="192f8-247">Hello publicado dirección del extremo es del formulario de hello `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="192f8-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="192f8-248">`UriScheme` y `PathSuffix` son atributos opcionales.</span><span class="sxs-lookup"><span data-stu-id="192f8-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="192f8-249">`IPAddressOrFQDN`es Hola dirección IP o nombre de dominio completo de este ejecutable se coloca en el nodo de Hola y se calcula automáticamente.</span><span class="sxs-lookup"><span data-stu-id="192f8-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="192f8-250">En hello siguiente ejemplo, servicio de hello una vez implementada, en el Explorador de Service Fabric verá un punto de conexión similar demasiado`http://10.1.4.92:3000/myapp/` publica para la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="192f8-251">Si se trata de un equipo local, verá `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="192f8-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="192f8-252">Puede usar estas direcciones con [proxy inverso](service-fabric-reverseproxy.md) toocommunicate entre servicios.</span><span class="sxs-lookup"><span data-stu-id="192f8-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="192f8-253">Editar el archivo de manifiesto de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="192f8-253">Edit hello application manifest file</span></span>
<span data-ttu-id="192f8-254">Una vez haya configurado hello `Servicemanifest.xml` archivo, necesita algunos cambios toohello toomake `ApplicationManifest.xml` correcta se usan el tipo de servicio y el nombre de archivo tooensure que Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="192f8-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="192f8-255">ServiceManifestImport</span></span>
<span data-ttu-id="192f8-256">Hola `ServiceManifestImport` elemento, puede especificar uno o varios servicios que desea que tooinclude en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="192f8-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="192f8-257">Se hace referencia a servicios con `ServiceManifestName`, que especifica el nombre de hello del directorio de Hola donde hello `ServiceManifest.xml` archivo se encuentra.</span><span class="sxs-lookup"><span data-stu-id="192f8-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="192f8-258">Configuración de los registros</span><span class="sxs-lookup"><span data-stu-id="192f8-258">Set up logging</span></span>
<span data-ttu-id="192f8-259">Para los ejecutables de invitado, resulta útil toobe toosee capaz de consola registros toofind out si los scripts de configuración de aplicación y de hello muestran los errores.</span><span class="sxs-lookup"><span data-stu-id="192f8-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="192f8-260">Redirección de la consola puede configurarse en hello `ServiceManifest.xml` archivo mediante hello `ConsoleRedirection` elemento.</span><span class="sxs-lookup"><span data-stu-id="192f8-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="192f8-261">Nunca use Directiva de redirección de consola de hello en una aplicación que se implementa en producción porque esto puede afectar a la conmutación por error de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="192f8-262">*Solo* debe usarla con fines de depuración y desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="192f8-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="192f8-263">`ConsoleRedirection`puede ser el directorio de trabajo de tooa de tooredirect usado consola resultado (stdout y stderr).</span><span class="sxs-lookup"><span data-stu-id="192f8-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="192f8-264">Esto proporciona Hola capacidad tooverify que no hay ningún error durante la instalación de Hola o ejecución de la aplicación hello en clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="192f8-265">`FileRetentionCount`Determina cuántos archivos se guardan en el directorio de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="192f8-266">Un valor de 5, por ejemplo, significa que los archivos de registro de hello para ejecuciones de cinco anterior Hola se almacenan en el directorio de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="192f8-267">`FileMaxSizeInKb`Especifica el tamaño máximo de Hola Hola de archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="192f8-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="192f8-268">Archivos de registro se guardan en uno de los directorios de trabajo del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="192f8-269">toodetermine donde hello encontrará los archivos, utilice Service Fabric Explorer toodetermine qué servicio de Hola de nodo se ejecuta en, y qué directorio de trabajo está usándola.</span><span class="sxs-lookup"><span data-stu-id="192f8-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="192f8-270">Este proceso se trata más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="192f8-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="192f8-271">Implementación</span><span class="sxs-lookup"><span data-stu-id="192f8-271">Deployment</span></span>
<span data-ttu-id="192f8-272">último paso de Hello es demasiado[implementar su aplicación](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="192f8-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="192f8-273">Hola después de la muestra de script de PowerShell toodeploy su clúster de desarrollo local de aplicación toohello e inicie un nuevo servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="192f8-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="192f8-274">[Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello si el paquete de hello es demasiado grande o tiene muchos archivos.</span><span class="sxs-lookup"><span data-stu-id="192f8-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="192f8-275">Obtenga más información [aquí](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="192f8-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="192f8-276">Se puede implementar un servicio Service Fabric en diversas "configuraciones".</span><span class="sxs-lookup"><span data-stu-id="192f8-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="192f8-277">Por ejemplo, se puede implementar como una o varias instancias o pueden implementarse de forma que hay una instancia del servicio de hello en cada nodo del clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="192f8-278">Hola `InstanceCount` parámetro de hello `New-ServiceFabricService` cmdlet es usado toospecify cuántas instancias del servicio de hello deben iniciarse en el clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="192f8-279">Puede establecer hello `InstanceCount` valor, según el tipo de Hola de aplicación que se va a implementar.</span><span class="sxs-lookup"><span data-stu-id="192f8-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="192f8-280">Hola dos los escenarios más comunes son:</span><span class="sxs-lookup"><span data-stu-id="192f8-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="192f8-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="192f8-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="192f8-282">En este caso, solo una instancia del servicio de Hola se implementa en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="192f8-283">Programador de Service Fabric determina qué servicio de hello nodo queda toobe implementada en.</span><span class="sxs-lookup"><span data-stu-id="192f8-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="192f8-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="192f8-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="192f8-285">En este caso, se implementa una instancia del servicio de hello en todos los nodos de clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="192f8-286">resultado de Hello tiene uno (y sólo una) instancia del servicio de Hola para cada nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="192f8-287">Se trata de una configuración resulta útil para las aplicaciones front-end (por ejemplo, un extremo REST), porque las aplicaciones cliente demasiado necesitan "conectar" tooany de nodos de hello en el punto de conexión de hello clúster toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="192f8-288">Esta configuración también se puede utilizar cuando, por ejemplo, todos los nodos del clúster de Service Fabric Hola de equilibrador de carga conectado tooa.</span><span class="sxs-lookup"><span data-stu-id="192f8-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="192f8-289">Tráfico de cliente, a continuación, se puede distribuir en servicio de Hola que se ejecuta en todos los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="192f8-290">Comprobación de la aplicación en ejecución</span><span class="sxs-lookup"><span data-stu-id="192f8-290">Check your running application</span></span>
<span data-ttu-id="192f8-291">En el Explorador de Service Fabric, identificar el nodo de Hola donde se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="192f8-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="192f8-292">En este ejemplo, se ejecuta en el nodo 1:</span><span class="sxs-lookup"><span data-stu-id="192f8-292">In this example, it runs on Node1:</span></span>

![Nodo donde se ejecuta el servicio](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="192f8-294">Si desplazarse por los nodos toohello y explorar aplicación toohello, verá información del nodo esenciales de hello, incluida su ubicación en el disco.</span><span class="sxs-lookup"><span data-stu-id="192f8-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Ubicación en el disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="192f8-296">Si examina toohello directorio mediante el Explorador de servidores, puede encontrar el directorio de trabajo de Hola y de carpeta de registro del servicio de hello, tal y como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="192f8-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Ubicación del registro](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="192f8-298">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="192f8-298">Next steps</span></span>
<span data-ttu-id="192f8-299">En este artículo, ha aprendido cómo toopackage un ejecutable de invitado e implementarlo tooService tejido.</span><span class="sxs-lookup"><span data-stu-id="192f8-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="192f8-300">Vea Hola siguientes artículos para obtener información relacionada y tareas.</span><span class="sxs-lookup"><span data-stu-id="192f8-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="192f8-301">[Ejemplo para empaquetar e implementar un archivo ejecutable de invitado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), incluida una versión preliminar de toohello de vínculo de la herramienta de empaquetado de Hola</span><span class="sxs-lookup"><span data-stu-id="192f8-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="192f8-302">Ejemplo de dos archivos ejecutables (C# y nodejs) de invitado comunicarse a través del servicio de nomenclatura de hello con REST</span><span class="sxs-lookup"><span data-stu-id="192f8-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="192f8-303">Implementación de varios ejecutables invitados</span><span class="sxs-lookup"><span data-stu-id="192f8-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="192f8-304">Creación de la primera aplicación de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="192f8-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
