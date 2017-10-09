---
title: "aaaReport y comprobación de mantenimiento con Azure Service Fabric | Documentos de Microsoft"
description: "Obtenga información acerca de cómo informes de mantenimiento de toosend desde el código de servicio y cómo proporciona el estado de hello toocheck de su servicio mediante el uso de herramientas de supervisión de estado de Hola que Azure Service Fabric."
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
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="45dd7-103">Notificación y comprobación del estado del servicio</span><span class="sxs-lookup"><span data-stu-id="45dd7-103">Report and check service health</span></span>
<span data-ttu-id="45dd7-104">Cuando los servicios encuentran problemas, los incidentes de corrección de capacidad toorespond tooand e interrupciones depende de sus capacidad toodetect Hola problemas rápidamente.</span><span class="sxs-lookup"><span data-stu-id="45dd7-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="45dd7-105">Si notificar problemas y errores de servicio de mantenimiento de Azure Service Fabric toohello desde el código de servicio, puede usar herramientas que Service Fabric proporciona el estado de mantenimiento de hello toocheck de supervisión de estado estándar.</span><span class="sxs-lookup"><span data-stu-id="45dd7-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="45dd7-106">Hay tres formas que puede crear informes de estado del servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="45dd7-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="45dd7-107">Mediante los objetos [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) o [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="45dd7-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="45dd7-108">Puede usar hello `Partition` y `CodePackageActivationContext` objetos de estado de hello tooreport de elementos que forman parte del contexto actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="45dd7-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="45dd7-109">Por ejemplo, código que se ejecuta como parte de una réplica puede notificar el estado solo en esa réplica, partición de Hola que pertenece y aplicación Hola que forma parte de.</span><span class="sxs-lookup"><span data-stu-id="45dd7-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="45dd7-110">Mediante `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="45dd7-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="45dd7-111">Puede usar `FabricClient` tooreport mantenimiento del código del servicio Hola si el clúster hello no está [segura](service-fabric-cluster-security.md) o si el servicio de saludo se está ejecutando con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="45dd7-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="45dd7-112">La mayoría de los escenarios reales no usan clústeres no seguros ni proporcionan privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="45dd7-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="45dd7-113">Con `FabricClient`, puede notificar el estado en cualquier entidad que forma parte del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="45dd7-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="45dd7-114">Lo ideal es que, sin embargo, código de servicio sólo enviará informes que están relacionados tooits propio estado.</span><span class="sxs-lookup"><span data-stu-id="45dd7-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="45dd7-115">Usar hello las API de REST en el clúster de hello, aplicación, aplicación implementada, servicio, paquete de servicio, partición, réplica o niveles de nodos.</span><span class="sxs-lookup"><span data-stu-id="45dd7-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="45dd7-116">Puede tratarse de mantenimiento de tooreport usado desde dentro de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="45dd7-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="45dd7-117">Este artículo le guiará a través de un ejemplo en el que informa del estado del código del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="45dd7-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="45dd7-118">ejemplo de Hola también muestra cómo herramientas Hola proporcionadas por Service Fabric pueden ser usado toocheck Hola estado.</span><span class="sxs-lookup"><span data-stu-id="45dd7-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="45dd7-119">En este artículo es toobe previsto en un estado de toohello introducción rápida a las capacidades de Service Fabric de supervisión.</span><span class="sxs-lookup"><span data-stu-id="45dd7-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="45dd7-120">Para obtener más información, puede leer serie de Hola de artículos detallados sobre el estado que comienzan con hello vínculo final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="45dd7-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45dd7-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="45dd7-121">Prerequisites</span></span>
<span data-ttu-id="45dd7-122">Debe tener instalado el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="45dd7-122">You must have hello following installed:</span></span>

* <span data-ttu-id="45dd7-123">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="45dd7-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="45dd7-124">SDK de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="45dd7-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="45dd7-125">toocreate un clúster local desarrollo seguro</span><span class="sxs-lookup"><span data-stu-id="45dd7-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="45dd7-126">Abra PowerShell con privilegios de administrador y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="45dd7-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![Comandos que muestran cómo toocreate un clúster de desarrollo seguro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="45dd7-128">toodeploy una aplicación y comprobar su estado</span><span class="sxs-lookup"><span data-stu-id="45dd7-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="45dd7-129">Abra Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="45dd7-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="45dd7-130">Crear un proyecto mediante el uso de hello **servicio con estado** plantilla.</span><span class="sxs-lookup"><span data-stu-id="45dd7-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Creación de una aplicación de Service Fabric con servicio con estado](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="45dd7-132">Presione **F5** toorun aplicación de hello en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="45dd7-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="45dd7-133">aplicación Hello es toohello implementado de clúster local.</span><span class="sxs-lookup"><span data-stu-id="45dd7-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="45dd7-134">Una vez que se ejecuta la aplicación hello, haga clic en el icono de administrador de clústeres Local de hello en el área de notificación de Hola y seleccione **administrar clúster Local** de tooopen de menú contextual de hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="45dd7-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Apertura del explorador de Service Fabric desde el área de notificación](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="45dd7-136">estado de la aplicación Hello debe mostrarse como se muestra en esta imagen.</span><span class="sxs-lookup"><span data-stu-id="45dd7-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="45dd7-137">En este momento, la aplicación hello deben funcionar correctamente sin errores.</span><span class="sxs-lookup"><span data-stu-id="45dd7-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Aplicación correcta en el explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="45dd7-139">También puede comprobar el estado de hello mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45dd7-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="45dd7-140">Puede usar ```Get-ServiceFabricApplicationHealth``` toocheck el estado de una aplicación y se pueden usar ```Get-ServiceFabricServiceHealth``` toocheck estado del servicio.</span><span class="sxs-lookup"><span data-stu-id="45dd7-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="45dd7-141">Hola informe de mantenimiento para hello misma aplicación en PowerShell está en esta imagen.</span><span class="sxs-lookup"><span data-stu-id="45dd7-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![Aplicación correcta en PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="45dd7-143">código de servicio de tooadd personalizada del estado eventos tooyour</span><span class="sxs-lookup"><span data-stu-id="45dd7-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="45dd7-144">las plantillas de proyecto de Service Fabric Hello en Visual Studio contienen código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="45dd7-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="45dd7-145">Hello pasos siguientes muestran cómo puede crear informes de eventos de estado personalizado desde el código de servicio.</span><span class="sxs-lookup"><span data-stu-id="45dd7-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="45dd7-146">Estos informes se muestran automáticamente en las herramientas estándar de Hola que proporciona Service Fabric, como explorador de Service Fabric y vista de estado de portal de Azure, PowerShell de supervisión de estado.</span><span class="sxs-lookup"><span data-stu-id="45dd7-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="45dd7-147">Vuelva a abrir la aplicación hello que creó en Visual Studio o cree una nueva aplicación mediante el uso de hello **servicio con estado** plantilla de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45dd7-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="45dd7-148">Abra el archivo de hello Stateful1.cs y encontrar Hola `myDictionary.TryGetValueAsync` llamar a en hello `RunAsync` método.</span><span class="sxs-lookup"><span data-stu-id="45dd7-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="45dd7-149">Puede ver que este método devuelve un `result` que contiene Hola valor actual del contador de hello porque lógica de las claves hello en esta aplicación es tookeep un ejecución de recuento.</span><span class="sxs-lookup"><span data-stu-id="45dd7-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="45dd7-150">Si se tratara de una aplicación real, y si falta de Hola de resultado representa un error, sería aconsejable tooflag ese evento.</span><span class="sxs-lookup"><span data-stu-id="45dd7-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="45dd7-151">tooreport un evento de mantenimiento cuando falta de Hola de resultado representa un error, agregue Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="45dd7-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="45dd7-152">a.</span><span class="sxs-lookup"><span data-stu-id="45dd7-152">a.</span></span> <span data-ttu-id="45dd7-153">Agregar hello `System.Fabric.Health` espacio de nombres toohello Stateful1.cs archivo.</span><span class="sxs-lookup"><span data-stu-id="45dd7-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="45dd7-154">b.</span><span class="sxs-lookup"><span data-stu-id="45dd7-154">b.</span></span> <span data-ttu-id="45dd7-155">Agregar Hola siguiente código después de hello `myDictionary.TryGetValueAsync` llamar a</span><span class="sxs-lookup"><span data-stu-id="45dd7-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="45dd7-156">Informamos sobre el estado de la réplica porque se está informando desde un servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="45dd7-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="45dd7-157">Hola `HealthInformation` parámetro almacena información sobre el problema de estado de Hola que se va a notificar.</span><span class="sxs-lookup"><span data-stu-id="45dd7-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="45dd7-158">Si ha creado un servicio sin estado, usar hello después de código</span><span class="sxs-lookup"><span data-stu-id="45dd7-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="45dd7-159">Si el servicio se ejecuta con privilegios de administrador o si hello clúster no está [segura](service-fabric-cluster-security.md), también puede usar `FabricClient` tooreport estado tal como se muestra en hello pasos.</span><span class="sxs-lookup"><span data-stu-id="45dd7-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="45dd7-160">a.</span><span class="sxs-lookup"><span data-stu-id="45dd7-160">a.</span></span> <span data-ttu-id="45dd7-161">Crear hello `FabricClient` instancia después de hello `var myDictionary` declaración.</span><span class="sxs-lookup"><span data-stu-id="45dd7-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="45dd7-162">b.</span><span class="sxs-lookup"><span data-stu-id="45dd7-162">b.</span></span> <span data-ttu-id="45dd7-163">Agregar Hola siguiente código después de hello `myDictionary.TryGetValueAsync` llamar.</span><span class="sxs-lookup"><span data-stu-id="45dd7-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="45dd7-164">Vamos a simular este error y se muestre en herramientas de supervisión de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="45dd7-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="45dd7-165">Error de hello toosimulate, comenta la primera línea de hello en estado de hello informa del código que agregó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="45dd7-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="45dd7-166">Después Comente la primera línea de hello, código de hello se parecerá al siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="45dd7-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="45dd7-167">Este código activa informe de mantenimiento de hello cada vez que `RunAsync` se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="45dd7-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="45dd7-168">Después de cambiar hello, presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="45dd7-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="45dd7-169">Después de que se ejecuta la aplicación hello, abra estado de Service Fabric Explorer toocheck Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="45dd7-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="45dd7-170">En esta ocasión, Service Fabric Explorer muestra que la aplicación hello es incorrecto.</span><span class="sxs-lookup"><span data-stu-id="45dd7-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="45dd7-171">Esto es debido a error de hello devuelto desde el código de hello que agregamos previamente.</span><span class="sxs-lookup"><span data-stu-id="45dd7-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Aplicación no correcta en el explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="45dd7-173">Si selecciona la réplica principal de hello en la vista de árbol de Hola de Service Fabric Explorer, verá que **estado** indica un error, demasiado.</span><span class="sxs-lookup"><span data-stu-id="45dd7-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="45dd7-174">Explorador de Service Fabric también muestra el informe de mantenimiento de hello detalles que agregan toohello `HealthInformation` parámetro en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="45dd7-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="45dd7-175">Puede ver Hola mismos informes de mantenimiento en PowerShell y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="45dd7-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Estado de réplica del explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="45dd7-177">Este informe permanece en el Administrador de mantenimiento de hello hasta que sea reemplazado por otro informe o hasta que se elimine esta réplica.</span><span class="sxs-lookup"><span data-stu-id="45dd7-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="45dd7-178">Dado que no se estableció `TimeToLive` para este informe de mantenimiento en hello `HealthInformation` objeto, informe de hello nunca caduca.</span><span class="sxs-lookup"><span data-stu-id="45dd7-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="45dd7-179">Se recomienda que se debería notificar mantenimiento en el nivel más granular de hello, que en este caso es réplica Hola.</span><span class="sxs-lookup"><span data-stu-id="45dd7-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="45dd7-180">También se puede informar sobre el estado en `Partition`.</span><span class="sxs-lookup"><span data-stu-id="45dd7-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="45dd7-181">estado de tooreport `Application`, `DeployedApplication`, y `DeployedServicePackage`, utilice `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="45dd7-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="45dd7-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45dd7-182">Next steps</span></span>
* [<span data-ttu-id="45dd7-183">Profundización en el estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="45dd7-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="45dd7-184">API de REST para informar el estado del servicio</span><span class="sxs-lookup"><span data-stu-id="45dd7-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="45dd7-185">API de REST para informar el estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="45dd7-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

