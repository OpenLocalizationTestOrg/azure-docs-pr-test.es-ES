---
title: "aaaDebug la aplicación en Visual Studio | Documentos de Microsoft"
description: "Mejorar Hola confiabilidad y rendimiento de los servicios mediante el desarrollo y depuración en Visual Studio en un clúster de desarrollo local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="6c3e8-103">Depurar la aplicación de Service Fabric con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6c3e8-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c3e8-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="6c3e8-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="6c3e8-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="6c3e8-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="6c3e8-106">Depurar una aplicación de Service Fabric local</span><span class="sxs-lookup"><span data-stu-id="6c3e8-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="6c3e8-107">Puede ahorrar tiempo y dinero implementando y depurando su aplicación de Service Fabric de Azure en un clúster de desarrollo del equipo local.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="6c3e8-108">Visual Studio 2017 o Visual Studio 2015 puede implementar el clúster local de hello aplicación toohello y conectarse automáticamente instancias de hello depurador tooall de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="6c3e8-109">Iniciar un clúster de desarrollo local siguiendo los pasos de hello en [configuración del entorno de desarrollo de Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6c3e8-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="6c3e8-110">Presione **F5** o haga clic en **Depurar** > **Iniciar depuración**.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Empezar a depurar una aplicación][startdebugging]
3. <span data-ttu-id="6c3e8-112">Establecer puntos de interrupción en el código y paso a través de la aplicación hello haciendo clic en los comandos de hello **depurar** menú.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c3e8-113">Visual Studio asocia tooall instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="6c3e8-114">Al recorrer el código, se pueden alcanzar los puntos de interrupción por varios procesos, lo que da lugar a sesiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="6c3e8-115">Pruebe a deshabilitar los puntos de interrupción de hello una vez que está alcanzados, mediante la realización de cada punto de interrupción condicional en el identificador de subproceso de Hola o mediante el uso de eventos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="6c3e8-116">Hola **eventos de diagnóstico** ventana se abrirá automáticamente para que pueda ver los eventos de diagnóstico en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Ver eventos de diagnóstico en tiempo real][diagnosticevents]
5. <span data-ttu-id="6c3e8-118">También puede abrir hello **eventos de diagnóstico** ventana en el explorador en la nube.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="6c3e8-119">En **Service Fabric**, haga clic con el botón derecho en cualquier nodo y elija **Ver seguimientos en streaming**.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Ventana de eventos de diagnóstico de hello abierto][viewdiagnosticevents]
   
    <span data-ttu-id="6c3e8-121">Si desea toofilter el servicio específico de seguimientos tooa o la aplicación, habilite simplemente seguimientos de transmisión por secuencias en esa aplicación o servicio específico.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="6c3e8-122">eventos de diagnóstico de Hello pueden verse en hello genera automáticamente **ServiceEventSource.cs** de archivos y se llama desde código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="6c3e8-123">Hola **eventos de diagnóstico** ventana admite el filtrado, la pausa y la inspección de eventos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="6c3e8-124">filtro de Hello es una búsqueda de cadena simple de mensaje de evento de hello, incluido su contenido.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![Filtrar, pausar y reanudar, o inspeccionar eventos en tiempo real][diagnosticeventsactions]
8. <span data-ttu-id="6c3e8-126">Depurar servicios es parecido a depurar cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="6c3e8-127">Para facilitar el proceso, lo normal es establecer puntos de interrupción a través de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="6c3e8-128">Aunque las instancias de Reliable Collections se replican en varios nodos, siguen implementando IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="6c3e8-129">Esto significa que puede usar Hola vista de resultados en Visual Studio mientras se depura toosee que hayas guardado dentro.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="6c3e8-130">Solo tiene que establecer un punto de interrupción en el código.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Empezar a depurar una aplicación][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="6c3e8-132">Depurar una aplicación de Service Fabric remota</span><span class="sxs-lookup"><span data-stu-id="6c3e8-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="6c3e8-133">Si las aplicaciones de Service Fabric se ejecutan en un clúster de Service Fabric en Azure, es posible depurar tooremotely estos, directamente desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="6c3e8-134">característica de Hello requiere [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) y [Azure SDK para .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6c3e8-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="6c3e8-135">Depuración remota está pensada para escenarios de desarrollo/pruebas y no toobe usar en entornos de producción, debido al impacto hello en hello las aplicaciones en ejecución.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="6c3e8-136">Navegar por clúster tooyour en **nube explorador**, haga clic en y elija **habilitar la depuración**</span><span class="sxs-lookup"><span data-stu-id="6c3e8-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Habilitar la depuración remota][enableremotedebugging]
   
    <span data-ttu-id="6c3e8-138">Esto se lanzará el proceso de Hola de habilitar la extensión en los nodos del clúster de la depuración remota de hello, así como las configuraciones de red necesarias.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="6c3e8-139">Nodo de clúster de hello contextual en **Explorer nube**y elija **adjuntar depurador**</span><span class="sxs-lookup"><span data-stu-id="6c3e8-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Asociar depurador][attachdebugger]
3. <span data-ttu-id="6c3e8-141">Hola **adjuntar tooprocess** cuadro de diálogo, elija el proceso de Hola que desee toodebug y haga clic en **adjuntar**</span><span class="sxs-lookup"><span data-stu-id="6c3e8-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![Elegir proceso][chooseprocess]
   
    <span data-ttu-id="6c3e8-143">nombre de Hello del proceso de Hola que desee tooattach a, es igual a Hola nombre de su nombre de ensamblado del proyecto de servicio.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="6c3e8-144">depurador de Hola se conectará nodos tooall ejecutando el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="6c3e8-145">En el caso de hello donde se depura un servicio sin estado, todas las instancias de servicio de hello en todos los nodos forman parte de la sesión de depuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="6c3e8-146">Si está depurando un servicio con estado, sólo Hola réplica principal de cualquier partición será detectada por lo tanto, el depurador de Hola y active.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="6c3e8-147">Si la réplica principal de Hola se mueve durante la sesión de depuración de hello, procesamiento de Hola de esa réplica seguirán parte de la sesión de depuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="6c3e8-148">En las particiones pertinentes de orden tooonly catch o instancias de un servicio determinado, puede usar puntos de interrupción condicionales tooonly interrupción una partición específica o una instancia.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![Punto de interrupción condicional][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="6c3e8-150">Actualmente no se admite la depuración de un clúster de Service Fabric con varias instancias de hello mismo nombre ejecutable del servicio.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="6c3e8-151">Una vez que termine de depurar la aplicación, puede deshabilitar la extensión de depuración remota de hello haciendo clic en el clúster de hello en **Explorer nube** y elija **deshabilitar la depuración**</span><span class="sxs-lookup"><span data-stu-id="6c3e8-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Deshabilitar la depuración remota][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="6c3e8-153">Seguimientos en streaming desde un nodo de clúster remoto</span><span class="sxs-lookup"><span data-stu-id="6c3e8-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="6c3e8-154">También es capaz de toostream seguimientos directamente desde un tooVisual de nodo de clúster remoto Studio.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="6c3e8-155">Esta característica permite toostream ETW eventos de seguimiento generados en un nodo de clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="6c3e8-156">Esta característica requiere [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) y el [SDK de Azure para .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6c3e8-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="6c3e8-157">Esta característica solo es compatible con clústeres que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="6c3e8-158">Transmisión por secuencias seguimientos está pensado para escenarios de desarrollo/pruebas y no toobe usar en entornos de producción, debido al impacto hello en hello las aplicaciones en ejecución.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="6c3e8-159">En un escenario de producción, debe depender del reenvío de eventos mediante Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="6c3e8-160">Navegar por clúster tooyour en **nube explorador**, haga clic en y elija **habilitar seguimientos de transmisión por secuencias**</span><span class="sxs-lookup"><span data-stu-id="6c3e8-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Habilitar seguimientos en streaming remotos][enablestreamingtraces]
   
    <span data-ttu-id="6c3e8-162">Esto se lanzará el proceso de Hola de habilitar Hola streaming extensión seguimientos en los nodos del clúster, así como las configuraciones de red necesarias.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="6c3e8-163">Expanda hello **nodos** elemento en **nube explorador**, nodo de hello contextual desee toostream seguimientos de y elija **seguimientos de transmisión por secuencias de vista**</span><span class="sxs-lookup"><span data-stu-id="6c3e8-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![Ver seguimientos en streaming remotos][viewremotestreamingtraces]
   
    <span data-ttu-id="6c3e8-165">Repita el paso 2 para tantos nodos como se desee toosee seguimientos de.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="6c3e8-166">Cada transmisión de nodos se mostrará en una ventana dedicada.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="6c3e8-167">Ya estás toosee capaz de seguimientos de hello emitidos por Service Fabric y los servicios.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="6c3e8-168">Si quiere toofilter Hola eventos tooonly muestran una aplicación específica, simplemente escriba Hola nombre de la aplicación hello en el filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c3e8-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![Ver seguimientos en streaming][viewingstreamingtraces]
3. <span data-ttu-id="6c3e8-170">Una vez que haya terminado de seguimientos de transmisión por secuencias desde el clúster, puede deshabilitar remotos seguimientos de transmisión por secuencias, haciendo clic en el clúster de hello en **Explorer nube** y elija **deshabilitar seguimientos de transmisión por secuencias**</span><span class="sxs-lookup"><span data-stu-id="6c3e8-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Deshabilitar seguimientos en streaming remotos][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="6c3e8-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c3e8-172">Next steps</span></span>
* <span data-ttu-id="6c3e8-173">[Pruebe un servicio de Service Fabric](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c3e8-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="6c3e8-174">[Administración de aplicaciones de Service Fabric en Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="6c3e8-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
