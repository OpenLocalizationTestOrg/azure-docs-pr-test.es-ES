---
title: "Depuración de la aplicación en Visual Studio | Microsoft Docs"
description: "Mejore la confiabilidad y el rendimiento de los servicios mediante su desarrollo y depuración en Visual Studio en un clúster de desarrollo local."
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
ms.openlocfilehash: 2459025899a7f5ffebf44fa104ed112c0eb99dfa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="89180-103">Depurar la aplicación de Service Fabric con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89180-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89180-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="89180-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="89180-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="89180-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="89180-106">Depurar una aplicación de Service Fabric local</span><span class="sxs-lookup"><span data-stu-id="89180-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="89180-107">Puede ahorrar tiempo y dinero implementando y depurando su aplicación de Service Fabric de Azure en un clúster de desarrollo del equipo local.</span><span class="sxs-lookup"><span data-stu-id="89180-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="89180-108">Visual Studio 2017 o Visual Studio 2015 pueden implementar la aplicación en el clúster local y conectar automáticamente el depurador a todas las instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="89180-108">Visual Studio 2017 or Visual Studio 2015 can deploy the application to the local cluster and automatically connect the debugger to all instances of your application.</span></span>

1. <span data-ttu-id="89180-109">Inicie un clúster de desarrollo local siguiendo los pasos descritos en [Configurar el entorno de desarrollo de Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="89180-109">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="89180-110">Presione **F5** o haga clic en **Depurar** > **Iniciar depuración**.</span><span class="sxs-lookup"><span data-stu-id="89180-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Empezar a depurar una aplicación][startdebugging]
3. <span data-ttu-id="89180-112">Establezca puntos de interrupción en el código y recorra la aplicación haciendo clic en los comandos del menú **Depurar** .</span><span class="sxs-lookup"><span data-stu-id="89180-112">Set breakpoints in your code and step through the application by clicking commands in the **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="89180-113">Visual Studio se conecta a todas las instancias de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="89180-113">Visual Studio attaches to all instances of your application.</span></span> <span data-ttu-id="89180-114">Al recorrer el código, se pueden alcanzar los puntos de interrupción por varios procesos, lo que da lugar a sesiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="89180-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="89180-115">Intente deshabilitar los puntos de interrupción después de que se alcancen, haciendo que el punto de interrupción sea condicional en el id. del subproceso o use los eventos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="89180-115">Try disabling the breakpoints after they're hit, by making each breakpoint conditional on the thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="89180-116">La ventana **Eventos de diagnóstico** se abrirá automáticamente para que pueda ver los eventos de diagnóstico en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="89180-116">The **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Ver eventos de diagnóstico en tiempo real][diagnosticevents]
5. <span data-ttu-id="89180-118">También puede abrir la ventana **Eventos de diagnóstico** en Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="89180-118">You can also open the **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="89180-119">En **Service Fabric**, haga clic con el botón derecho en cualquier nodo y elija **Ver seguimientos en streaming**.</span><span class="sxs-lookup"><span data-stu-id="89180-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Abrir la ventana de eventos de diagnóstico][viewdiagnosticevents]
   
    <span data-ttu-id="89180-121">Si quiere filtrar los seguimientos para mostrar una aplicación o un servicio específicos, simplemente habilite los seguimientos en streaming en ellos.</span><span class="sxs-lookup"><span data-stu-id="89180-121">If you want to filter your traces to a specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="89180-122">Los eventos de diagnóstico se pueden ver en el archivo **ServiceEventSource.cs** generado automáticamente y se llaman desde el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="89180-122">The diagnostic events can be seen in the automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="89180-123">La ventana **Eventos de diagnóstico** admite filtrado, pausas y la inspección de eventos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="89180-123">The **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="89180-124">El filtro es una búsqueda de cadena simple del mensaje de evento, incluido su contenido.</span><span class="sxs-lookup"><span data-stu-id="89180-124">The filter is a simple string search of the event message, including its contents.</span></span>
   
    ![Filtrar, pausar y reanudar, o inspeccionar eventos en tiempo real][diagnosticeventsactions]
8. <span data-ttu-id="89180-126">Depurar servicios es parecido a depurar cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="89180-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="89180-127">Para facilitar el proceso, lo normal es establecer puntos de interrupción a través de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89180-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="89180-128">Aunque las instancias de Reliable Collections se replican en varios nodos, siguen implementando IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="89180-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="89180-129">Esto significa que puede usar la vista de resultados en Visual Studio durante la depuración para ver lo que ha almacenado dentro.</span><span class="sxs-lookup"><span data-stu-id="89180-129">This means that you can use the Results View in Visual Studio while debugging to see what you've stored inside.</span></span> <span data-ttu-id="89180-130">Solo tiene que establecer un punto de interrupción en el código.</span><span class="sxs-lookup"><span data-stu-id="89180-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Empezar a depurar una aplicación][breakpoint]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="89180-132">Depurar una aplicación de Service Fabric remota</span><span class="sxs-lookup"><span data-stu-id="89180-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="89180-133">Si las aplicaciones de Service Fabric se están ejecutando en un clúster de Service Fabric de Azure, es posible depurarlas de forma remota, directamente desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89180-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able to remotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="89180-134">La característica requiere [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) y el [SDK de Azure para .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="89180-134">The feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="89180-135">La depuración remota está diseñada para escenarios de desarrollo y pruebas y no para su uso en entornos de producción, debido al impacto en las aplicaciones en ejecución.</span><span class="sxs-lookup"><span data-stu-id="89180-135">Remote debugging is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> 
> 

1. <span data-ttu-id="89180-136">Vaya a su clúster de **Cloud Explorer**, haga clic con el botón derecho y elija **Habilitar depuración**</span><span class="sxs-lookup"><span data-stu-id="89180-136">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Habilitar la depuración remota][enableremotedebugging]
   
    <span data-ttu-id="89180-138">De esta forma se inicia el proceso de habilitar la extensión de depuración remota en los nodos del clúster, así como las configuraciones de red necesarias.</span><span class="sxs-lookup"><span data-stu-id="89180-138">This will kick off the process of enabling the remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="89180-139">Haga clic con el botón derecho en el nodo de clúster en **Cloud Explorer** y elija **Adjuntar depurador**</span><span class="sxs-lookup"><span data-stu-id="89180-139">Right-click the cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Asociar depurador][attachdebugger]
3. <span data-ttu-id="89180-141">En el cuadro de diálogo **Asociar al proceso**, elija el proceso que quiere depurar y haga clic en **Adjuntar**</span><span class="sxs-lookup"><span data-stu-id="89180-141">In the **Attach to process** dialog, choose the process you want to debug, and click **Attach**</span></span>
   
    ![Elegir proceso][chooseprocess]
   
    <span data-ttu-id="89180-143">El nombre del proceso que desea asociar equivale al nombre del ensamblado del proyecto de servicio.</span><span class="sxs-lookup"><span data-stu-id="89180-143">The name of the process you want to attach to, equals the name of your service project assembly name.</span></span>
   
    <span data-ttu-id="89180-144">El depurador se asociará a todos los nodos que ejecutan el proceso.</span><span class="sxs-lookup"><span data-stu-id="89180-144">The debugger will attach to all nodes running the process.</span></span>
   
   * <span data-ttu-id="89180-145">En caso de que vaya a depurar un servicio sin estado, todas las instancias del servicio en todos los nodos forman parte de la sesión de depuración.</span><span class="sxs-lookup"><span data-stu-id="89180-145">In the case where you are debugging a stateless service, all instances of the service on all nodes are part of the debug session.</span></span>
   * <span data-ttu-id="89180-146">Si va a depurar un servicio con estado, solo la réplica principal de cualquier partición estará activa y, por tanto, será la que capture el depurador.</span><span class="sxs-lookup"><span data-stu-id="89180-146">If you are debugging a stateful service, only the primary replica of any partition will be active and therefore caught by the debugger.</span></span> <span data-ttu-id="89180-147">Si se mueve la réplica principal durante la sesión de depuración, el procesamiento de esa réplica todavía será parte de la sesión de depuración.</span><span class="sxs-lookup"><span data-stu-id="89180-147">If the primary replica moves during the debug session, the processing of that replica will still be part of the debug session.</span></span>
   * <span data-ttu-id="89180-148">Para capturar solo las particiones o instancias pertinentes de un servicio determinado, puede utilizar puntos de interrupción condicionales para interrumpir solo una instancia o una partición específica.</span><span class="sxs-lookup"><span data-stu-id="89180-148">In order to only catch relevant partitions or instances of a given service, you can use conditional breakpoints to only break a specific partition or instance.</span></span>
     
     ![Punto de interrupción condicional][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="89180-150">Actualmente no se admite la depuración de un clúster de Service Fabric con varias instancias del mismo nombre ejecutable de servicio.</span><span class="sxs-lookup"><span data-stu-id="89180-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of the same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="89180-151">Cuando termine de depurar la aplicación, puede deshabilitar la extensión de depuración remota; para ello, haga clic con el botón derecho en el clúster en **Cloud Explorer** y elija **Deshabilitar depuración**</span><span class="sxs-lookup"><span data-stu-id="89180-151">Once you finish debugging your application, you can disable the remote debugging extension by right-clicking the cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Deshabilitar la depuración remota][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="89180-153">Seguimientos en streaming desde un nodo de clúster remoto</span><span class="sxs-lookup"><span data-stu-id="89180-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="89180-154">También puede trasmitir seguimientos directamente desde un nodo de clúster remoto a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89180-154">You are also able to stream traces directly from a remote cluster node to Visual Studio.</span></span> <span data-ttu-id="89180-155">Esta característica permite transmitir eventos de seguimiento ETW, generados en un nodo de clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="89180-155">This feature allows you to stream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="89180-156">Esta característica requiere [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) y el [SDK de Azure para .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="89180-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="89180-157">Esta característica solo es compatible con clústeres que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="89180-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="89180-158">Los seguimientos en streaming están concebidos para escenarios de desarrollo y pruebas y no para su uso en entornos de producción, debido al impacto en las aplicaciones en ejecución.</span><span class="sxs-lookup"><span data-stu-id="89180-158">Streaming traces is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> <span data-ttu-id="89180-159">En un escenario de producción, debe depender del reenvío de eventos mediante Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="89180-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="89180-160">Vaya a su clúster en **Cloud Explorer**, haga clic con el botón derecho y elija **Habilitar seguimientos en streaming**</span><span class="sxs-lookup"><span data-stu-id="89180-160">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Habilitar seguimientos en streaming remotos][enablestreamingtraces]
   
    <span data-ttu-id="89180-162">De esta forma se inicia el proceso de habilitar la extensión de seguimientos en streaming en los nodos del clúster, así como las configuraciones de red necesarias.</span><span class="sxs-lookup"><span data-stu-id="89180-162">This will kick off the process of enabling the streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="89180-163">Expanda el elemento **Nodos** en **Cloud Explorer**, haga clic con el botón derecho en el nodo desde el que desea transmitir seguimientos y elija **Ver seguimientos en streaming**</span><span class="sxs-lookup"><span data-stu-id="89180-163">Expand the **Nodes** element in **Cloud Explorer**, right-click the node you want to stream traces from and choose **View Streaming Traces**</span></span>
   
    ![Ver seguimientos en streaming remotos][viewremotestreamingtraces]
   
    <span data-ttu-id="89180-165">Repita el paso 2 en todos los nodos desde los que quiera ver seguimientos.</span><span class="sxs-lookup"><span data-stu-id="89180-165">Repeat step 2 for as many nodes as you want to see traces from.</span></span> <span data-ttu-id="89180-166">Cada transmisión de nodos se mostrará en una ventana dedicada.</span><span class="sxs-lookup"><span data-stu-id="89180-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="89180-167">Ahora puede ver los seguimientos emitidos por Service Fabric y sus servicios.</span><span class="sxs-lookup"><span data-stu-id="89180-167">You are now able to see the traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="89180-168">Si quiere filtrar los eventos para mostrar solo una aplicación específica, simplemente escriba el nombre de la aplicación en el filtro.</span><span class="sxs-lookup"><span data-stu-id="89180-168">If you want to filter the events to only show a specific application, simply type in the name of the application in the filter.</span></span>
   
    ![Ver seguimientos en streaming][viewingstreamingtraces]
3. <span data-ttu-id="89180-170">Cuando haya realizado los seguimientos en streaming desde el clúster, puede deshabilitar los seguimientos en streaming remotos; para ello, haga clic con el botón derecho en el clúster en **Cloud Explorer** y elija **Deshabilitar seguimientos en streaming**</span><span class="sxs-lookup"><span data-stu-id="89180-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking the cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Deshabilitar seguimientos en streaming remotos][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="89180-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89180-172">Next steps</span></span>
* <span data-ttu-id="89180-173">[Pruebe un servicio de Service Fabric](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="89180-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="89180-174">[Administración de aplicaciones de Service Fabric en Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="89180-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

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
