---
title: "las aplicaciones de Service Fabric con el uso de análisis de registros aaaAssess Hola portal de Azure | Documentos de Microsoft"
description: "Puede usar soluciones de Service Fabric hello en análisis de registros con el riesgo de hello tooassess portal Azure de Hola y el estado de las aplicaciones de Service Fabric, micro-services, nodos y clústeres."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="e55ab-103">Evaluar las aplicaciones de Service Fabric y microservicios con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e55ab-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e55ab-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e55ab-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="e55ab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e55ab-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Símbolo de Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="e55ab-107">Este artículo describe cómo toouse Hola solución de Service Fabric en análisis de registros toohelp identificar y solucionar problemas en el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e55ab-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="e55ab-108">Hola soluciones de Service Fabric utiliza datos de diagnósticos de Azure de las máquinas virtuales tejido de servicio, mediante la recopilación de estos datos de las tablas de WAD de Azure.</span><span class="sxs-lookup"><span data-stu-id="e55ab-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="e55ab-109">Posteriormente, Log Analytics lee los eventos del marco de Service Fabric, incluidos los **eventos de servicios de confianza**, los **eventos de actor**, los **eventos operativos** y los **eventos ETW personalizados**.</span><span class="sxs-lookup"><span data-stu-id="e55ab-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="e55ab-110">Con el panel de la solución de hello, son problemas importantes capaz de tooview y los eventos relevantes en su entorno de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e55ab-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="e55ab-111">tooget a trabajar con soluciones de hello, deberá tooconnect el área de trabajo de análisis de registros de Service Fabric clúster tooa.</span><span class="sxs-lookup"><span data-stu-id="e55ab-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="e55ab-112">A continuación, presentamos tres tooconsider de escenarios:</span><span class="sxs-lookup"><span data-stu-id="e55ab-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="e55ab-113">Si no ha implementado el clúster de Service Fabric, siga los pasos de hello en ***implementar un área de trabajo de análisis de registros de servicio de Cluster Server tejido conectado tooa*** toodeploy un nuevo clúster y configuró tooreport tooLog análisis.</span><span class="sxs-lookup"><span data-stu-id="e55ab-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="e55ab-114">Si necesita toocollect los contadores de rendimiento de su toouse hosts otras soluciones OMS como la seguridad en su clúster de Service Fabric, siga los pasos de hello en ***implementar un área de trabajo de análisis de registros de tooa de clúster de Service Fabric conectado con la extensión de máquina virtual instalado.***</span><span class="sxs-lookup"><span data-stu-id="e55ab-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="e55ab-115">Si ya ha implementado el clúster de Service Fabric y desea tooconnect se tooLog análisis, siga los pasos de hello en ***agregando un tooLog de cuenta de almacenamiento existente análisis.***</span><span class="sxs-lookup"><span data-stu-id="e55ab-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="e55ab-116">Implementar un área de trabajo de análisis de registros de tooa conectado el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e55ab-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="e55ab-117">Esta plantilla Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e55ab-117">This template does hello following:</span></span>

1. <span data-ttu-id="e55ab-118">Implementa un área de trabajo de análisis de registros de Azure Service Fabric ya está conectado el clúster tooa.</span><span class="sxs-lookup"><span data-stu-id="e55ab-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="e55ab-119">Tener Hola opción toocreate una nueva área de trabajo durante la implementación de plantilla de Hola o nombre de entrada Hola de un área de trabajo de análisis de registros ya existente.</span><span class="sxs-lookup"><span data-stu-id="e55ab-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="e55ab-120">Agrega el área de trabajo de análisis de registro de toohello de cuenta de hello el almacenamiento de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e55ab-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="e55ab-121">Habilita la solución de Service Fabric de hello en el área de trabajo de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="e55ab-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="e55ab-122">[![Implementar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e55ab-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="e55ab-123">Una vez que selecciona Hola implementar el botón de más arriba, hello Azure abre portal con parámetros para tooedit.</span><span class="sxs-lookup"><span data-stu-id="e55ab-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="e55ab-124">Ser seguro toocreate un nuevo grupo de recursos si se escribe un nuevo nombre de área de trabajo de análisis de registros:</span><span class="sxs-lookup"><span data-stu-id="e55ab-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="e55ab-127">Acepte los términos legales de Hola y haga clic en **crear** implementación de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="e55ab-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="e55ab-128">Una vez completada la implementación de hello, debería ver área de trabajo nueva hello y clúster creado y Hola WADServiceFabric * WADWindowsEventLogs de eventos y WADETWEvent tablas agregadas:</span><span class="sxs-lookup"><span data-stu-id="e55ab-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="e55ab-130">Implementar un área de trabajo de análisis de registros de tooa de clúster de Service Fabric conectado con la extensión de VM instalado.</span><span class="sxs-lookup"><span data-stu-id="e55ab-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="e55ab-131">Esta plantilla Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e55ab-131">This template does hello following:</span></span>

1. <span data-ttu-id="e55ab-132">Implementa un área de trabajo de análisis de registros de Azure Service Fabric ya está conectado el clúster tooa.</span><span class="sxs-lookup"><span data-stu-id="e55ab-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="e55ab-133">Puede crear una tabla o usar una existente.</span><span class="sxs-lookup"><span data-stu-id="e55ab-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="e55ab-134">Agrega el área de trabajo de análisis de registro de toohello de cuentas de hello el almacenamiento de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e55ab-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="e55ab-135">Habilita la solución de Service Fabric hello en el área de trabajo de análisis de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="e55ab-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="e55ab-136">Instala la extensión del agente MMA hello en cada conjunto en el clúster de Service Fabric de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e55ab-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="e55ab-137">Con instalado el agente MMA hello, está tooview capaz de métricas de rendimiento acerca de los nodos.</span><span class="sxs-lookup"><span data-stu-id="e55ab-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="e55ab-138">[![Implementar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e55ab-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="e55ab-139">A continuación Hola los mismos pasos anteriormente, los parámetros necesarios de entrada hello y comenzar una implementación.</span><span class="sxs-lookup"><span data-stu-id="e55ab-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="e55ab-140">Una vez más verá nueva área de trabajo de hello, el clúster y creadas todas las tablas WAD:</span><span class="sxs-lookup"><span data-stu-id="e55ab-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="e55ab-142">Visualización de datos de rendimiento</span><span class="sxs-lookup"><span data-stu-id="e55ab-142">Viewing Performance Data</span></span>

<span data-ttu-id="e55ab-143">tooview datos de rendimiento de los nodos:</span><span class="sxs-lookup"><span data-stu-id="e55ab-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="e55ab-144">Inicie el área de trabajo de análisis de registros de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e55ab-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="e55ab-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="e55ab-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="e55ab-146">Vaya tooSettings en el panel izquierdo de Hola y seleccionar los datos >> contadores de rendimiento de Windows >> "hello complemento seleccionado los contadores de rendimiento": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="e55ab-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="e55ab-147">En búsqueda de registros, utilice Hola después toodelve de las consultas en las métricas clave sobre los nodos:</span><span class="sxs-lookup"><span data-stu-id="e55ab-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="e55ab-148">a.</span><span class="sxs-lookup"><span data-stu-id="e55ab-148">a.</span></span> <span data-ttu-id="e55ab-149">Comparar Hola uso promedio de CPU en todos los nodos de hello último una hora toosee qué nodos están experimentando problemas al y en el intervalo de tiempo que un nodo tenía un pico:</span><span class="sxs-lookup"><span data-stu-id="e55ab-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="e55ab-151">b.</span><span class="sxs-lookup"><span data-stu-id="e55ab-151">b.</span></span> <span data-ttu-id="e55ab-152">Vea gráficos de líneas similares para la memoria disponible en cada nodo con esta consulta:</span><span class="sxs-lookup"><span data-stu-id="e55ab-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="e55ab-153">tooview una lista de todos los nodos, donde se muestran un valor promedio exacto Hola de MBytes disponibles para cada nodo, use esta consulta:</span><span class="sxs-lookup"><span data-stu-id="e55ab-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="e55ab-155">c.</span><span class="sxs-lookup"><span data-stu-id="e55ab-155">c.</span></span> <span data-ttu-id="e55ab-156">En caso de Hola que quiera toodrill hacia abajo en un nodo específico mediante el examen de media hora de hello, uso de CPU mínimo, máximo y percentil 75, le toodo puede confirmarlo mediante esta consulta (sustituya el campo de equipo):</span><span class="sxs-lookup"><span data-stu-id="e55ab-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="e55ab-158">Leer más información acerca de las métricas de rendimiento de análisis de registros en hello [blog de Operations Management Suite](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="e55ab-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="e55ab-159">Agregar un tooLog de cuenta de almacenamiento existente análisis</span><span class="sxs-lookup"><span data-stu-id="e55ab-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="e55ab-160">Esta plantilla simplemente agrega su almacenamiento cuentas tooa nuevo o existente análisis de registros área de trabajo existente.</span><span class="sxs-lookup"><span data-stu-id="e55ab-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="e55ab-161">[![Implementar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e55ab-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="e55ab-162">En la selección de un grupo de recursos, si está trabajando con un área de trabajo de análisis de registros ya existente, seleccione "Usar existente" y busque el grupo de recursos de Hola que contiene el área de trabajo de análisis de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="e55ab-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="e55ab-163">En caso contrario, cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="e55ab-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="e55ab-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="e55ab-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="e55ab-165">Una vez se ha implementado esta plantilla, es posible que el área de trabajo de toosee capaz de hello almacenamiento cuenta conectada tooyour análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="e55ab-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="e55ab-166">En este caso, agregué una más almacenamiento cuenta toohello Exchange área de trabajo que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e55ab-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="e55ab-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="e55ab-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="e55ab-168">Visualización de eventos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e55ab-168">View Service Fabric events</span></span>

<span data-ttu-id="e55ab-169">Una vez que se completen las implementaciones de Hola y Hola soluciones de tejido de servicio se ha habilitado en el área de trabajo, seleccione hello **Service Fabric** el icono Panel de hello análisis de registros toolaunch portal Hola Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e55ab-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="e55ab-170">panel de Hello incluye columnas de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="e55ab-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="e55ab-171">Cada columna muestra top 10 eventos de hello mediante la correspondencia de recuento que han especificado criterios de la columna para hello intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e55ab-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="e55ab-172">Puede ejecutar una búsqueda de registros que proporciona la lista completa de hello haciendo clic en **ver todas** en hello derecha, abajo de cada columna, o haciendo clic en el encabezado de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="e55ab-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="e55ab-173">**Evento de Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="e55ab-173">**Service Fabric event**</span></span> | <span data-ttu-id="e55ab-174">**descripción**</span><span class="sxs-lookup"><span data-stu-id="e55ab-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="e55ab-175">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="e55ab-175">Notable Issues</span></span> |<span data-ttu-id="e55ab-176">Una pantalla con problemas como RunAsyncFailures RunAsynCancellations y nodos inactivos.</span><span class="sxs-lookup"><span data-stu-id="e55ab-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="e55ab-177">Eventos operativos</span><span class="sxs-lookup"><span data-stu-id="e55ab-177">Operational Events</span></span> |<span data-ttu-id="e55ab-178">Eventos operativos importantes como implementaciones y actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e55ab-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="e55ab-179">Eventos de servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="e55ab-179">Reliable Service Events</span></span> |<span data-ttu-id="e55ab-180">Eventos de servicios de confianza importantes como Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="e55ab-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="e55ab-181">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="e55ab-181">Actor Events</span></span> |<span data-ttu-id="e55ab-182">Eventos de actor importantes generados por los microservicios, como las excepciones que inician un método de actor, activaciones y desactivaciones de actor, etc.</span><span class="sxs-lookup"><span data-stu-id="e55ab-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="e55ab-183">Eventos de aplicación</span><span class="sxs-lookup"><span data-stu-id="e55ab-183">Application Events</span></span> |<span data-ttu-id="e55ab-184">Todos los eventos ETW personalizados generados por las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e55ab-184">All custom ETW events generated by your applications.</span></span> |

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="e55ab-187">Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e55ab-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="e55ab-188">plataforma</span><span class="sxs-lookup"><span data-stu-id="e55ab-188">platform</span></span> | <span data-ttu-id="e55ab-189">Agente directo</span><span class="sxs-lookup"><span data-stu-id="e55ab-189">Direct Agent</span></span> | <span data-ttu-id="e55ab-190">Agente de Operations Manager</span><span class="sxs-lookup"><span data-stu-id="e55ab-190">Operations Manager agent</span></span> | <span data-ttu-id="e55ab-191">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e55ab-191">Azure Storage</span></span> | <span data-ttu-id="e55ab-192">¿Se requiere Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="e55ab-192">Operations Manager required?</span></span> | <span data-ttu-id="e55ab-193">Se envían los datos del agente de Operations Manager a través del grupo de administración</span><span class="sxs-lookup"><span data-stu-id="e55ab-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="e55ab-194">Frecuencia de recopilación</span><span class="sxs-lookup"><span data-stu-id="e55ab-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e55ab-195">Windows</span><span class="sxs-lookup"><span data-stu-id="e55ab-195">Windows</span></span> |  |  | <span data-ttu-id="e55ab-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e55ab-196">&#8226;</span></span> |  |  |<span data-ttu-id="e55ab-197">10 minutos</span><span class="sxs-lookup"><span data-stu-id="e55ab-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="e55ab-198">También puede cambiar el ámbito de Hola de estos eventos en hello soluciones de Service Fabric haciendo clic en **datos basándose en los últimos 7 días** en parte superior de hello del panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="e55ab-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="e55ab-199">También puede mostrar los eventos generados en hello últimos siete días, un día o seis horas.</span><span class="sxs-lookup"><span data-stu-id="e55ab-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="e55ab-200">O bien, puede seleccionar **personalizado** toospecify un intervalo de fechas personalizado.</span><span class="sxs-lookup"><span data-stu-id="e55ab-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e55ab-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e55ab-201">Next steps</span></span>

* <span data-ttu-id="e55ab-202">Use [búsquedas de registros de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de eventos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e55ab-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
