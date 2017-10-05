---
title: "Evaluación de aplicaciones de Service Fabric con Log Analytics en Azure Portal | Microsoft Docs"
description: "Puede usar la solución de Service Fabric con Log Analytics en Azure Portal para evaluar el riesgo y el estado de las aplicaciones, los microservicios, los nodos y los clústeres de Service Fabric."
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
ms.openlocfilehash: 8c564c0dcbb2f9be286917b2f4d8a40da5406fae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-the-azure-portal"></a><span data-ttu-id="2bd0c-103">Evaluación de aplicaciones y microservicios de Service Fabric con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2bd0c-103">Assess Service Fabric applications and micro-services with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2bd0c-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2bd0c-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="2bd0c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bd0c-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Símbolo de Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="2bd0c-107">En este artículo se describe cómo utilizar la solución de Service Fabric en Log Analytics para ayudar a identificar y solucionar problemas en su clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="2bd0c-108">La solución de Service Fabric utiliza datos de Diagnósticos de Azure de las máquinas virtuales de Service Fabric recopilando estos datos de las tablas WAD de Azure.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-108">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="2bd0c-109">Posteriormente, Log Analytics lee los eventos del marco de Service Fabric, incluidos los **eventos de servicios de confianza**, los **eventos de actor**, los **eventos operativos** y los **eventos ETW personalizados**.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="2bd0c-110">Con el panel de la solución, se pueden ver los eventos pertinentes y problemas importantes de su entorno de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-110">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="2bd0c-111">Para empezar a trabajar con la solución, debe conectar su clúster de Service Fabric a un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-111">To get started with the solution, you need to connect your Service Fabric cluster to a Log Analytics workspace.</span></span> <span data-ttu-id="2bd0c-112">Hay tres escenarios principales que se han de tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-112">Here are three scenarios to consider:</span></span>

1. <span data-ttu-id="2bd0c-113">Si no ha implementado su clúster de Service Fabric, siga los pasos del artículo sobre cómo ***implementar un clúster de Service Fabric conectado a un área de trabajo de Log Analytics*** para implementar un nuevo clúster y configúrelo para que envíe informes a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-113">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span></span>
2. <span data-ttu-id="2bd0c-114">Si tiene que recopilar contadores de rendimiento de los hosts para usar otras soluciones de OMS como la de seguridad en su clúster de Service Fabric, siga los pasos del artículo sobre cómo ***implementar un clúster de Service Fabric conectado a un área de trabajo de Log Analytics con la extensión de máquina virtual instalada***.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-114">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="2bd0c-115">Si ya ha implementado el clúster de Service Fabric y quiere conectarse a Log Analytics, siga los pasos del artículo sobre cómo ***agregar una cuenta de almacenamiento existente a Log Analytics***.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-115">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace"></a><span data-ttu-id="2bd0c-116">Implemente un clúster de Service Fabric conectado a un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-116">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span></span>
<span data-ttu-id="2bd0c-117">Esta plantilla hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-117">This template does the following:</span></span>

1. <span data-ttu-id="2bd0c-118">Implementa un clúster de Service Fabric de Azure ya conectado a un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-118">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="2bd0c-119">Tiene la opción de crear una nueva área de trabajo durante la implementación de la plantilla, o especificar el nombre de un área de trabajo de Log Analytics ya existente.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-119">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="2bd0c-120">Agrega la cuenta de almacenamiento de información de diagnóstico al área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-120">Adds the diagnostic storage account to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="2bd0c-121">Permite usar la solución de Service Fabric en el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-121">Enables the Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="2bd0c-122">[![Implementación en Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2bd0c-122">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="2bd0c-123">Cuando selecciona el botón Implementar anterior, Azure Portal se abre con parámetros que puede editar.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-123">Once you select the deploy button above, the Azure portal opens with parameters for you to edit.</span></span> <span data-ttu-id="2bd0c-124">Asegúrese de crear un nuevo grupo de recursos si escribe un nuevo nombre de área de trabajo de Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-124">Be sure to create a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="2bd0c-127">Acepte los términos legales y haga clic en **Crear** para iniciar la implementación.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-127">Accept the legal terms and click **Create** to start the deployment.</span></span> <span data-ttu-id="2bd0c-128">Una vez completada la implementación, debería ver la nueva área de trabajo y el clúster creado, así como las tablas WADServiceFabric*Event, WADWindowsEventLogs y WADETWEvent agregadas:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-128">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="2bd0c-130">Implemente un clúster de Service Fabric conectado a un área de trabajo de Log Analytics con la extensión de máquina virtual instalada.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-130">Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="2bd0c-131">Esta plantilla hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-131">This template does the following:</span></span>

1. <span data-ttu-id="2bd0c-132">Implementa un clúster de Service Fabric de Azure ya conectado a un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-132">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="2bd0c-133">Puede crear una tabla o usar una existente.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="2bd0c-134">Agrega las cuentas de almacenamiento de información de diagnóstico al área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-134">Adds the diagnostic storage accounts to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="2bd0c-135">Permite usar la solución de Service Fabric en el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-135">Enables the Service Fabric solution in the Log Analytics workspace.</span></span>
4. <span data-ttu-id="2bd0c-136">Instala la extensión del agente de MMA en cada conjunto de escalado de máquinas virtuales del clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-136">Installs the MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="2bd0c-137">Con el agente de MMA instalado, puede ver las métricas de rendimiento de los nodos.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-137">With the MMA agent installed, you are able to view performance metrics about your nodes.</span></span>

<span data-ttu-id="2bd0c-138">[![Implementación en Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2bd0c-138">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="2bd0c-139">Siguiendo los mismos pasos, escriba los parámetros necesarios e inicie una implementación.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-139">Following the same steps above, input the necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="2bd0c-140">De nuevo, verá creados la nueva área de trabajo, el clúster y las tablas WAD:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-140">Once again you should see the new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="2bd0c-142">Visualización de datos de rendimiento</span><span class="sxs-lookup"><span data-stu-id="2bd0c-142">Viewing Performance Data</span></span>

<span data-ttu-id="2bd0c-143">Para ver datos de rendimiento de los nodos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-143">To view Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="2bd0c-144">Inicie el área de trabajo de Log Analytics desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-144">Launch the Log Analytics workspace from the Azure portal.</span></span>
  <span data-ttu-id="2bd0c-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="2bd0c-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="2bd0c-146">Vaya a la configuración del panel izquierdo y seleccione Datos >> Contadores de rendimiento de Windows >> Agregar los contadores de rendimiento seleccionados: ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="2bd0c-146">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="2bd0c-147">En Búsqueda de registros, utilice las siguientes consultas para profundizar en las métricas clave de los nodos:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-147">In Log Search, use the following queries to delve into key metrics about your nodes:</span></span>

    <span data-ttu-id="2bd0c-148">a.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-148">a.</span></span> <span data-ttu-id="2bd0c-149">Compare el uso medio de CPU en todos los nodos en la última hora para ver los que tienen problemas y el intervalo de tiempo en que un nodo tenía un pico:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-149">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="2bd0c-151">b.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-151">b.</span></span> <span data-ttu-id="2bd0c-152">Vea gráficos de líneas similares para la memoria disponible en cada nodo con esta consulta:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="2bd0c-153">Para ver una lista de todos los nodos, que muestra el valor medio exacto de MB disponibles para cada nodo, utilice esta consulta:</span><span class="sxs-lookup"><span data-stu-id="2bd0c-153">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="2bd0c-155">c.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-155">c.</span></span> <span data-ttu-id="2bd0c-156">En el caso de que desee ver los detalles de un nodo específico examinando el promedio mínimo, máximo y percentil 75 por hora de uso de CPU, puede hacerlo mediante esta consulta (sustituya el campo Equipo):</span><span class="sxs-lookup"><span data-stu-id="2bd0c-156">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="2bd0c-158">Lea más información sobre las métricas de rendimiento de Log Analytics en el [blog de Operations Management Suite](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="2bd0c-158">Read more information about performance metrics in Log Analytics at the [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-to-log-analytics"></a><span data-ttu-id="2bd0c-159">Adición de una cuenta de almacenamiento existente a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2bd0c-159">Adding an existing storage account to Log Analytics</span></span>

<span data-ttu-id="2bd0c-160">Esta plantilla simplemente agrega las cuentas de almacenamiento existentes a un área de trabajo de Log Analytics nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-160">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="2bd0c-161">[![Implementación en Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2bd0c-161">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="2bd0c-162">Al seleccionar un grupo de recursos, si está trabajando con un área de trabajo de Log Analytics ya existente, seleccione "Usar existente" y busque el grupo de recursos que contiene el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for the resource group containing the Log Analytics workspace.</span></span> <span data-ttu-id="2bd0c-163">En caso contrario, cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="2bd0c-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="2bd0c-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="2bd0c-165">Una vez implementada esta plantilla, podrá ver la cuenta de almacenamiento conectada a su área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-165">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span></span> <span data-ttu-id="2bd0c-166">En este caso, agregamos otra cuenta de almacenamiento al área de trabajo de Exchange que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-166">In this instance, I added one more storage account to the Exchange workspace I created above.</span></span>
<span data-ttu-id="2bd0c-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="2bd0c-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="2bd0c-168">Visualización de eventos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2bd0c-168">View Service Fabric events</span></span>

<span data-ttu-id="2bd0c-169">Una vez que se completan las implementaciones y se ha habilitado la solución de Service Fabric en el área de trabajo, seleccione el icono de **Service Fabric** en el portal de Log Analytics para iniciar el panel de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-169">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span></span> <span data-ttu-id="2bd0c-170">El panel incluye las columnas de la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-170">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="2bd0c-171">Cada columna muestra los 10 principales eventos por recuento que coinciden con los criterios de esa columna para el intervalo de tiempo especificados.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-171">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="2bd0c-172">Puede ejecutar una búsqueda de registros que proporcione toda la lista haciendo clic en **Ver todo** en la parte inferior derecha de la columna o haciendo clic en el encabezado de columna.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-172">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="2bd0c-173">**Evento de Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="2bd0c-173">**Service Fabric event**</span></span> | <span data-ttu-id="2bd0c-174">**descripción**</span><span class="sxs-lookup"><span data-stu-id="2bd0c-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="2bd0c-175">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="2bd0c-175">Notable Issues</span></span> |<span data-ttu-id="2bd0c-176">Una pantalla con problemas como RunAsyncFailures RunAsynCancellations y nodos inactivos.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="2bd0c-177">Eventos operativos</span><span class="sxs-lookup"><span data-stu-id="2bd0c-177">Operational Events</span></span> |<span data-ttu-id="2bd0c-178">Eventos operativos importantes como implementaciones y actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="2bd0c-179">Eventos de servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="2bd0c-179">Reliable Service Events</span></span> |<span data-ttu-id="2bd0c-180">Eventos de servicios de confianza importantes como Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="2bd0c-181">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="2bd0c-181">Actor Events</span></span> |<span data-ttu-id="2bd0c-182">Eventos de actor importantes generados por los microservicios, como las excepciones que inician un método de actor, activaciones y desactivaciones de actor, etc.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="2bd0c-183">Eventos de aplicación</span><span class="sxs-lookup"><span data-stu-id="2bd0c-183">Application Events</span></span> |<span data-ttu-id="2bd0c-184">Todos los eventos ETW personalizados generados por las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-184">All custom ETW events generated by your applications.</span></span> |

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="2bd0c-187">La siguiente tabla muestra los métodos de recolección de datos y otros detalles sobre cómo se recopilan los datos para Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-187">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="2bd0c-188">plataforma</span><span class="sxs-lookup"><span data-stu-id="2bd0c-188">platform</span></span> | <span data-ttu-id="2bd0c-189">Agente directo</span><span class="sxs-lookup"><span data-stu-id="2bd0c-189">Direct Agent</span></span> | <span data-ttu-id="2bd0c-190">Agente de Operations Manager</span><span class="sxs-lookup"><span data-stu-id="2bd0c-190">Operations Manager agent</span></span> | <span data-ttu-id="2bd0c-191">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="2bd0c-191">Azure Storage</span></span> | <span data-ttu-id="2bd0c-192">¿Se requiere Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="2bd0c-192">Operations Manager required?</span></span> | <span data-ttu-id="2bd0c-193">Se envían los datos del agente de Operations Manager a través del grupo de administración</span><span class="sxs-lookup"><span data-stu-id="2bd0c-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="2bd0c-194">Frecuencia de recopilación</span><span class="sxs-lookup"><span data-stu-id="2bd0c-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2bd0c-195">Windows</span><span class="sxs-lookup"><span data-stu-id="2bd0c-195">Windows</span></span> |  |  | <span data-ttu-id="2bd0c-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2bd0c-196">&#8226;</span></span> |  |  |<span data-ttu-id="2bd0c-197">10 minutos</span><span class="sxs-lookup"><span data-stu-id="2bd0c-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="2bd0c-198">Puede cambiar el ámbito de estos eventos en la solución de Service Fabric haciendo clic **Data based on last 7 days** (Datos basados en los últimos 7 días) en la parte superior del panel.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-198">You can change the scope of these events in the Service Fabric solution by clicking **Data based on last 7 days** at the top of the dashboard.</span></span> <span data-ttu-id="2bd0c-199">También puede mostrar los eventos generados en los últimos 7 días, 1 día o 6 horas,</span><span class="sxs-lookup"><span data-stu-id="2bd0c-199">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="2bd0c-200">o bien seleccionar **Personalizado** y especificar un intervalo de fechas personalizado.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-200">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2bd0c-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2bd0c-201">Next steps</span></span>

* <span data-ttu-id="2bd0c-202">Use [Búsquedas de registros en Log Analytics](log-analytics-log-searches.md) para ver datos detallados sobre los datos de eventos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2bd0c-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
