---
title: "Notificación y comprobación del estado con Azure Service Fabric | Microsoft Docs"
description: "Conozca cómo se pueden enviar informes de estado desde el código de servicio y comprobar el estado del servicio mediante las herramientas de supervisión de estado que proporciona Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="bfe68-103">Notificación y comprobación del estado del servicio</span><span class="sxs-lookup"><span data-stu-id="bfe68-103">Report and check service health</span></span>
<span data-ttu-id="bfe68-104">Cuando los servicios se encuentran con problemas, su capacidad para responder y corregir cualquier incidente e interrupción depende de la capacidad de detectar los problemas rápidamente.</span><span class="sxs-lookup"><span data-stu-id="bfe68-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="bfe68-105">Si informa de problemas y errores en el administrador de estado de Azure Service Fabric desde el código de servicio, puede usar las herramientas estándar de seguimiento de estado que proporciona Service Fabric para comprobar el estado de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="bfe68-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="bfe68-106">Hay tres maneras de informar sobre el estado del servicio:</span><span class="sxs-lookup"><span data-stu-id="bfe68-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="bfe68-107">Mediante los objetos [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) o [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="bfe68-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="bfe68-108">Puede usar los objetos `Partition` y `CodePackageActivationContext` para informar sobre el estado de elementos que forman parte del contexto actual.</span><span class="sxs-lookup"><span data-stu-id="bfe68-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="bfe68-109">Por ejemplo, el código que se ejecuta como parte de una réplica solo puede informar sobre el estado de esa réplica, la partición a la que pertenece y la aplicación de la que forma parte.</span><span class="sxs-lookup"><span data-stu-id="bfe68-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="bfe68-110">Mediante `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="bfe68-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="bfe68-111">Puede usar `FabricClient` para informar sobre el estado del código de servicio si el clúster no es [seguro](service-fabric-cluster-security.md) o si el servicio se ejecuta con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="bfe68-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="bfe68-112">La mayoría de los escenarios reales no usan clústeres no seguros ni proporcionan privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="bfe68-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="bfe68-113">Con `FabricClient`, puede notificar sobre el estado de cualquier entidad que forme parte del clúster.</span><span class="sxs-lookup"><span data-stu-id="bfe68-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="bfe68-114">Sin embargo, lo ideal es que el código de servicio solo envíe informes relacionados con su propio estado.</span><span class="sxs-lookup"><span data-stu-id="bfe68-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="bfe68-115">Use las API de REST en el nivel de clúster, aplicación, aplicación implementada, servicio, paquete de servicios, partición, réplica o nodo.</span><span class="sxs-lookup"><span data-stu-id="bfe68-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="bfe68-116">Esto se puede usar para informar sobre el estado desde dentro de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="bfe68-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="bfe68-117">Este artículo le guiará a través de un ejemplo que informa del estado del código de servicio.</span><span class="sxs-lookup"><span data-stu-id="bfe68-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="bfe68-118">El ejemplo también muestra cómo se pueden usar las herramientas que ofrece Service Fabric para comprobar el estado de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="bfe68-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="bfe68-119">Este artículo pretende ser una introducción rápida a las funcionalidades de supervisión del estado de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bfe68-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="bfe68-120">Para obtener más información, puede leer la serie de artículos detallados sobre el estado, empezando por el vínculo al final de este documento.</span><span class="sxs-lookup"><span data-stu-id="bfe68-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfe68-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bfe68-121">Prerequisites</span></span>
<span data-ttu-id="bfe68-122">Debe tener instalados los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bfe68-122">You must have the following installed:</span></span>

* <span data-ttu-id="bfe68-123">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bfe68-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="bfe68-124">SDK de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bfe68-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="bfe68-125">Para crear un clúster de desarrollo seguro local</span><span class="sxs-lookup"><span data-stu-id="bfe68-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="bfe68-126">Abra PowerShell con privilegios de administrador y ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bfe68-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![Comandos que muestran cómo crear un clúster de desarrollo seguro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="bfe68-128">Para implementar una aplicación y comprobar su estado</span><span class="sxs-lookup"><span data-stu-id="bfe68-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="bfe68-129">Abra Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="bfe68-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="bfe68-130">Cree un proyecto mediante la plantilla **Servicio con estado** .</span><span class="sxs-lookup"><span data-stu-id="bfe68-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Creación de una aplicación de Service Fabric con servicio con estado](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="bfe68-132">Presione **F5** para ejecutar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="bfe68-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="bfe68-133">La aplicación se implementa en el clúster local.</span><span class="sxs-lookup"><span data-stu-id="bfe68-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="bfe68-134">Después de ejecutarse la aplicación, haga clic con el botón derecho en el icono Administrador de clúster local en el área de notificación y seleccione **Administrar clúster local** en el menú de función rápida para abrir el explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bfe68-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Apertura del explorador de Service Fabric desde el área de notificación](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="bfe68-136">El estado de la aplicación debe aparecer como se muestra en esta imagen.</span><span class="sxs-lookup"><span data-stu-id="bfe68-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="bfe68-137">En este momento, la aplicación debe ser correcta y no tener errores.</span><span class="sxs-lookup"><span data-stu-id="bfe68-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Aplicación correcta en el explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="bfe68-139">También puede comprobar el estado mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfe68-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="bfe68-140">Puede usar ```Get-ServiceFabricApplicationHealth``` y ```Get-ServiceFabricServiceHealth``` para comprobar el estado de una aplicación y un servicio, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bfe68-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="bfe68-141">El informe de estado para la misma aplicación en PowerShell se muestra en esta imagen.</span><span class="sxs-lookup"><span data-stu-id="bfe68-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![Aplicación correcta en PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="bfe68-143">Para agregar eventos de estado personalizados a su código de servicio</span><span class="sxs-lookup"><span data-stu-id="bfe68-143">To add custom health events to your service code</span></span>
<span data-ttu-id="bfe68-144">Las plantillas de proyecto de Service Fabric en Visual Studio contienen código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bfe68-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="bfe68-145">Los pasos siguientes muestran cómo puede informar sobre eventos de estado personalizados desde el código de servicio.</span><span class="sxs-lookup"><span data-stu-id="bfe68-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="bfe68-146">Estos informes aparecen automáticamente en las herramientas estándar para la supervisión del estado que proporciona Service Fabric, como Service Fabric Explorer, la vista del estado de Azure Portal y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfe68-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="bfe68-147">Vuelva a abrir la aplicación que creó anteriormente en Visual Studio o cree otra con un servicio con estado mediante la plantilla de Visual Studio **Servicio con estado** .</span><span class="sxs-lookup"><span data-stu-id="bfe68-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="bfe68-148">Abra el archivo Stateful1.cs y busque la llamada `myDictionary.TryGetValueAsync` en el método `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="bfe68-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="bfe68-149">Puede ver que este método devuelve un `result` que mantiene el valor actual del contador porque la lógica principal de esta aplicación es mantener el recuento en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="bfe68-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="bfe68-150">Si se tratara de una aplicación real y si la falta de resultados representara un error, es posible que le interesara marcar ese evento.</span><span class="sxs-lookup"><span data-stu-id="bfe68-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="bfe68-151">Para informar sobre un evento de estado cuando la falta de resultados representa un error, agregue los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="bfe68-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="bfe68-152">a.</span><span class="sxs-lookup"><span data-stu-id="bfe68-152">a.</span></span> <span data-ttu-id="bfe68-153">Agregue este espacio de nombres `System.Fabric.Health` al archivo Stateful1.cs.</span><span class="sxs-lookup"><span data-stu-id="bfe68-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="bfe68-154">b.</span><span class="sxs-lookup"><span data-stu-id="bfe68-154">b.</span></span> <span data-ttu-id="bfe68-155">Agregue el siguiente código después de la llamada `myDictionary.TryGetValueAsync` .</span><span class="sxs-lookup"><span data-stu-id="bfe68-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="bfe68-156">Informamos sobre el estado de la réplica porque se está informando desde un servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="bfe68-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="bfe68-157">El parámetro `HealthInformation` almacena información sobre el problema de estado del que se está informando.</span><span class="sxs-lookup"><span data-stu-id="bfe68-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="bfe68-158">Si ha creado un servicio sin estado, use el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="bfe68-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="bfe68-159">Si el servicio se ejecuta con privilegios de administrador o si el clúster no es [seguro`FabricClient`, también puede usar ](service-fabric-cluster-security.md) para informar sobre el estado tal y como se muestra en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="bfe68-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="bfe68-160">a.</span><span class="sxs-lookup"><span data-stu-id="bfe68-160">a.</span></span> <span data-ttu-id="bfe68-161">Cree la instancia `FabricClient` después de la declaración `var myDictionary`.</span><span class="sxs-lookup"><span data-stu-id="bfe68-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="bfe68-162">b.</span><span class="sxs-lookup"><span data-stu-id="bfe68-162">b.</span></span> <span data-ttu-id="bfe68-163">Agregue el siguiente código después de la llamada `myDictionary.TryGetValueAsync` .</span><span class="sxs-lookup"><span data-stu-id="bfe68-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="bfe68-164">Simulemos este error y veamos cómo se muestra en las herramientas de seguimiento de estado.</span><span class="sxs-lookup"><span data-stu-id="bfe68-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="bfe68-165">Para simular el error, comente la primera línea en el código de notificación de estado que agregó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bfe68-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="bfe68-166">Después de comentar la primera línea, el código tendrá el aspecto del siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bfe68-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="bfe68-167">Este código activa el informe de estado cada vez que se ejecuta `RunAsync` .</span><span class="sxs-lookup"><span data-stu-id="bfe68-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="bfe68-168">Después de realizar el cambio, presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bfe68-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="bfe68-169">Después de que la aplicación se esté ejecutando, abra el explorador de Service Fabric para comprobar el estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bfe68-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="bfe68-170">Esta vez, Service Fabric Explorer muestra que el estado de la aplicación no es correcto.</span><span class="sxs-lookup"><span data-stu-id="bfe68-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="bfe68-171">Esto es debido al error que se notificó en el código que se agregó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bfe68-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Aplicación no correcta en el explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="bfe68-173">Si selecciona la réplica principal en la vista de árbol del explorador de Service Fabric, verá que **Health State** también indica un error.</span><span class="sxs-lookup"><span data-stu-id="bfe68-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="bfe68-174">El explorador de Service Fabric también muestra los detalles del informe de estado que se agregaron al parámetro `HealthInformation` en el código.</span><span class="sxs-lookup"><span data-stu-id="bfe68-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="bfe68-175">También puede ver los mismos informes de estado en PowerShell y en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bfe68-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Estado de réplica del explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="bfe68-177">Este informe permanece en el administrador de estado hasta que se sustituya por otro o se elimine esta réplica.</span><span class="sxs-lookup"><span data-stu-id="bfe68-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="bfe68-178">Dado que no establecimos `TimeToLive` para este informe de estado en el objeto `HealthInformation`, el informe nunca expira.</span><span class="sxs-lookup"><span data-stu-id="bfe68-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="bfe68-179">Recomendamos notificar sobre el mantenimiento en el nivel más detallado, que en este caso es la réplica.</span><span class="sxs-lookup"><span data-stu-id="bfe68-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="bfe68-180">También se puede informar sobre el estado en `Partition`.</span><span class="sxs-lookup"><span data-stu-id="bfe68-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="bfe68-181">Para informar del estado en `Application`, `DeployedApplication` y `DeployedServicePackage`, use `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="bfe68-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="bfe68-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfe68-182">Next steps</span></span>
* [<span data-ttu-id="bfe68-183">Profundización en el estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bfe68-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="bfe68-184">API de REST para informar el estado del servicio</span><span class="sxs-lookup"><span data-stu-id="bfe68-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="bfe68-185">API de REST para informar el estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bfe68-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

