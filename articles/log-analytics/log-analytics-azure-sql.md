---
title: "Solución Azure SQL Analytics de Log Analytics | Microsoft Docs"
description: "La solución Azure SQL Analytics le ayuda a administrar las instancias de Azure SQL Database."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="46526-103">Supervisión de Azure SQL Database mediante Azure SQL Analytics (versión preliminar) en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="46526-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Símbolo de Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="46526-105">La solución Azure SQL Analytics de Azure Log Analytics recopila y muestra métricas de rendimiento importantes de Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="46526-105">The Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="46526-106">Mediante el uso de las métricas que se recopilan con la solución, puede crear alertas y reglas de supervisión personalizadas.</span><span class="sxs-lookup"><span data-stu-id="46526-106">By using the metrics that you collect with the solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="46526-107">Y puede supervisar Azure SQL Database y las métricas de los grupos elásticos de varias suscripciones y grupos elásticos de Azure y visualizarlos.</span><span class="sxs-lookup"><span data-stu-id="46526-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="46526-108">La solución también le ayuda a identificar los problemas de cada nivel de la pila de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="46526-108">The solution also helps you to identify issues at each layer of your application stack.</span></span>  <span data-ttu-id="46526-109">Usa las [métricas de diagnóstico de Azure](log-analytics-azure-storage.md) junto con las vistas de Log Analytics para presentar datos sobre todas sus instancias de Azure SQL Database y sus grupos elásticos en una sola área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="46526-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views to present data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="46526-110">Actualmente, la versión preliminar de esta solución admite hasta 150 000 instancias de Azure SQL Database y 5000 grupos elásticos de SQL por área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="46526-110">Currently, this preview solution supports up to 150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="46526-111">La solución Azure SQL Analytics, al igual que otras disponibles para Log Analytics, le ayuda a supervisar y recibir notificaciones sobre el estado de los recursos de Azure y, en este caso, de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="46526-111">The Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about the health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="46526-112">Microsoft Azure SQL Database es un servicio de base de datos relacional escalable que proporciona funcionalidades conocidas de tipo SQL Server para aplicaciones que se ejecutan en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="46526-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities to applications running in the Azure cloud.</span></span> <span data-ttu-id="46526-113">Log Analytics le ayuda a recopilar, correlacionar y visualizar datos estructurados y no estructurados.</span><span class="sxs-lookup"><span data-stu-id="46526-113">Log Analytics helps you to collect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="46526-114">Orígenes conectados</span><span class="sxs-lookup"><span data-stu-id="46526-114">Connected sources</span></span>

<span data-ttu-id="46526-115">La solución Azure SQL Analytics no usa agentes para conectarse al servicio Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="46526-115">The Azure SQL Analytics solution doesn't use agents to connect to the Log Analytics service.</span></span>

<span data-ttu-id="46526-116">En la tabla siguiente se describen los orígenes conectados que son compatibles con esta solución.</span><span class="sxs-lookup"><span data-stu-id="46526-116">The following table describes the connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="46526-117">Origen conectado</span><span class="sxs-lookup"><span data-stu-id="46526-117">Connected Source</span></span> | <span data-ttu-id="46526-118">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="46526-118">Support</span></span> | <span data-ttu-id="46526-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="46526-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="46526-120">Agentes de Windows</span><span class="sxs-lookup"><span data-stu-id="46526-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="46526-121">No</span><span class="sxs-lookup"><span data-stu-id="46526-121">No</span></span> | <span data-ttu-id="46526-122">La solución no utiliza agentes directos de Windows.</span><span class="sxs-lookup"><span data-stu-id="46526-122">Direct Windows agents are not used by the solution.</span></span> |
| [<span data-ttu-id="46526-123">Agentes de Linux</span><span class="sxs-lookup"><span data-stu-id="46526-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="46526-124">No</span><span class="sxs-lookup"><span data-stu-id="46526-124">No</span></span> | <span data-ttu-id="46526-125">La solución no utiliza agentes directos de Linux.</span><span class="sxs-lookup"><span data-stu-id="46526-125">Direct Linux agents are not used by the solution.</span></span> |
| [<span data-ttu-id="46526-126">Grupo de administración de SCOM</span><span class="sxs-lookup"><span data-stu-id="46526-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="46526-127">No</span><span class="sxs-lookup"><span data-stu-id="46526-127">No</span></span> | <span data-ttu-id="46526-128">La solución no utiliza una conexión directa entre el agente de SCOM y Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="46526-128">A direct connection from the SCOM agent to Log Analytics is not used by the solution.</span></span> |
| [<span data-ttu-id="46526-129">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="46526-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="46526-130">No</span><span class="sxs-lookup"><span data-stu-id="46526-130">No</span></span> | <span data-ttu-id="46526-131">Log Analytics no lee los datos de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="46526-131">Log Analytics does not read the data from a storage account.</span></span> |
| [<span data-ttu-id="46526-132">Diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="46526-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="46526-133">Sí</span><span class="sxs-lookup"><span data-stu-id="46526-133">Yes</span></span> | <span data-ttu-id="46526-134">Azure envía directamente los datos de métricas de Azure a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="46526-134">Azure metric data is sent to Log Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="46526-135">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="46526-135">Prerequisites</span></span>

- <span data-ttu-id="46526-136">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="46526-136">An Azure Subscription.</span></span> <span data-ttu-id="46526-137">Si no tiene ninguna, puede crear una [gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="46526-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="46526-138">Un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="46526-138">A Log Analytics workspace.</span></span> <span data-ttu-id="46526-139">Puede usar una existente, o bien puede [crear una nueva](log-analytics-get-started.md) para empezar a usar esta solución.</span><span class="sxs-lookup"><span data-stu-id="46526-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="46526-140">Habilite Diagnósticos de Azure para sus instancias de Azure SQL Database y para los grupos elásticos y [configúrelo para que envíe sus datos a Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="46526-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them to send their data to Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="46526-141">Configuración</span><span class="sxs-lookup"><span data-stu-id="46526-141">Configuration</span></span>

<span data-ttu-id="46526-142">Realice los pasos siguientes para agregar la solución Azure SQL Analytics al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="46526-142">Perform the following steps to add the Azure SQL Analytics solution to your workspace.</span></span>

1. <span data-ttu-id="46526-143">Agregue la Azure SQL Analytics al área de trabajo desde [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) o mediante el proceso descrito en el artículo sobre [incorporación de soluciones de Log Analytics desde la Galería de soluciones](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="46526-143">Add the Azure SQL Analytics solution to your workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="46526-144">En Azure Portal, haga clic en **Nuevo** (el símbolo +) y, a continuación, en la lista de recursos, seleccione **Supervisión y administración**.</span><span class="sxs-lookup"><span data-stu-id="46526-144">In the Azure portal, click **New** (the + symbol), then in the list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="46526-145">![Supervisión + Administración](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="46526-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="46526-146">En la lista **Supervisión y administración**, haga clic en **Ver todo**.</span><span class="sxs-lookup"><span data-stu-id="46526-146">In the **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="46526-147">En la lista **Recomendado**, haga clic en **Más** y, a continuación, en la nueva lista, busque **Azure SQL Analytics (versión preliminar)** y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="46526-147">In the **Recommended** list, click **More** , and then in the new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="46526-148">![Solución Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="46526-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="46526-149">En la hoja **Azure SQL Analytics (versión preliminar)**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="46526-149">In the **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="46526-150">![Creación](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="46526-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="46526-151">En la hoja **Crear nueva solución**, seleccione el área de trabajo a la que desea agregar la solución y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="46526-151">In the **Create new solution** blade, select the workspace that you want to add the solution to and then click **Create**.</span></span>  
    <span data-ttu-id="46526-152">![Agregar a área de trabajo](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="46526-152">![add to workspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="to-configure-multiple-azure-subscriptions"></a><span data-ttu-id="46526-153">Configuración de varias suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="46526-153">To configure multiple Azure subscriptions</span></span>

<span data-ttu-id="46526-154">Para admitir varias suscripciones, use el script de PowerShell de [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/) (Habilitar registro de métricas de recursos de Azure mediante PowerShell).</span><span class="sxs-lookup"><span data-stu-id="46526-154">To support multiple subscriptions, use the PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="46526-155">Proporcione el identificador de recurso del área de trabajo como un parámetro al ejecutar el script para enviar los datos de diagnóstico de los recursos de una suscripción de Azure a un área de trabajo de otra suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="46526-155">Provide the workspace resource ID as a parameter when executing the script to send diagnostic data from resources in one Azure subscription to a workspace in another Azure subscription.</span></span>

<span data-ttu-id="46526-156">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="46526-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a><span data-ttu-id="46526-157">Uso de la solución</span><span class="sxs-lookup"><span data-stu-id="46526-157">Using the solution</span></span>

<span data-ttu-id="46526-158">Cuando la solución se agrega al área de trabajo, el icono de Azure SQL Analytics se agrega al área de trabajo y aparece en la introducción.</span><span class="sxs-lookup"><span data-stu-id="46526-158">When you add the solution to your workspace, the Azure SQL Analytics tile is added to your workspace, and it appears in Overview.</span></span> <span data-ttu-id="46526-159">El icono muestra el número de bases de datos y grupos elásticos de Azure SQL a los que está conectada la solución.</span><span class="sxs-lookup"><span data-stu-id="46526-159">The tile shows the number of Azure SQL databases and Azure SQL elastic pools that the solution is connected to.</span></span>

![Icono de Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="46526-161">Visualización de los datos de Azure SQL Analytics</span><span class="sxs-lookup"><span data-stu-id="46526-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="46526-162">Haga clic en el icono de **Azure SQL Analytics** para que se abra el panel de Azure SQL Analytics.</span><span class="sxs-lookup"><span data-stu-id="46526-162">Click on the **Azure SQL Analytics** tile to open the Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="46526-163">El panel incluye las hojas detalladas a continuación.</span><span class="sxs-lookup"><span data-stu-id="46526-163">The dashboard includes the blades defined below.</span></span> <span data-ttu-id="46526-164">Cada hoja enumera hasta 15 recursos (suscripción, servidor, grupo elástico y base de datos).</span><span class="sxs-lookup"><span data-stu-id="46526-164">Each blade lists up to 15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="46526-165">Haga clic en cualquiera de los recursos para abrir el panel de ese recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="46526-165">Click any of the resources to open the dashboard for that specific resource.</span></span> <span data-ttu-id="46526-166">Grupo elástico o base de datos contienen los gráficos de métricas de un recurso seleccionado.</span><span class="sxs-lookup"><span data-stu-id="46526-166">Elastic Pool or Database contains the charts with metrics for a selected resource.</span></span> <span data-ttu-id="46526-167">Haga clic en un gráfico para abrir el cuadro de diálogo de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="46526-167">Click a chart to open the Log Search dialog.</span></span>

| <span data-ttu-id="46526-168">Hoja</span><span class="sxs-lookup"><span data-stu-id="46526-168">Blade</span></span> | <span data-ttu-id="46526-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="46526-169">Description</span></span> |
|---|---|
| <span data-ttu-id="46526-170">Suscripciones</span><span class="sxs-lookup"><span data-stu-id="46526-170">Subscriptions</span></span> | <span data-ttu-id="46526-171">Lista de las suscripciones con el número de servidores conectados, los grupos y las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="46526-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="46526-172">Servidores</span><span class="sxs-lookup"><span data-stu-id="46526-172">Servers</span></span> | <span data-ttu-id="46526-173">Lista de servidores con el número de grupos conectados y las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="46526-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="46526-174">Grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="46526-174">Elastic Pools</span></span> | <span data-ttu-id="46526-175">Lista de grupos elásticos conectados con número máximo de GB y eDTU en el período observado.</span><span class="sxs-lookup"><span data-stu-id="46526-175">List of connected elastic pools with maximum GB and eDTU in the observed period.</span></span> |
|<span data-ttu-id="46526-176">Bases de datos</span><span class="sxs-lookup"><span data-stu-id="46526-176">Databases</span></span> | <span data-ttu-id="46526-177">Lista de bases de datos conectadas con GB máximos y DTU en el período observado.</span><span class="sxs-lookup"><span data-stu-id="46526-177">List of connected databases with maximum GB and DTU in the observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="46526-178">Análisis de datos y creación de alertas</span><span class="sxs-lookup"><span data-stu-id="46526-178">Analyze data and create alerts</span></span>

<span data-ttu-id="46526-179">Las alertas se pueden crear fácilmente con los datos procedentes de los recursos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="46526-179">You can easily create alerts with the data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="46526-180">Estas son un par de consultas de [búsqueda de registros](log-analytics-log-searches.md) útiles que puede usar para las alertas:</span><span class="sxs-lookup"><span data-stu-id="46526-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="46526-181">*DTU alta en Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="46526-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="46526-182">*DTU alta en el grupo elástico de Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="46526-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="46526-183">Puede usar estas consultas basadas en alertas para generar alertas sobre umbrales específicos para Azure SQL Database y los grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="46526-183">You can use these alert-based queries to alert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="46526-184">Configuración de una alerta para el área de trabajo de OMS:</span><span class="sxs-lookup"><span data-stu-id="46526-184">To configure an alert for your OMS workspace:</span></span>

#### <a name="to-configure-an-alert-for-your-workspace"></a><span data-ttu-id="46526-185">Configuración de una alerta para el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="46526-185">To configure an alert for your workspace</span></span>

1. <span data-ttu-id="46526-186">Abra el [portal de OMS](http://mms.microsoft.com/) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="46526-186">Go to the [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="46526-187">Abra el área de trabajo que ha configurado para la solución.</span><span class="sxs-lookup"><span data-stu-id="46526-187">Open the workspace that you have configured for the solution.</span></span>
3. <span data-ttu-id="46526-188">En la página Información general, haga clic en el icono de **Azure SQL Analytics (versión preliminar)**.</span><span class="sxs-lookup"><span data-stu-id="46526-188">On the Overview page, click the **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="46526-189">Ejecute una de las consultas de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="46526-189">Run one of the example queries.</span></span>
5. <span data-ttu-id="46526-190">En Búsqueda de registros, haga clic en **Alerta**.</span><span class="sxs-lookup"><span data-stu-id="46526-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="46526-191">![crear alerta en la búsqueda](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="46526-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="46526-192">En la página **Agregar regla de alerta** página, configure las propiedades adecuadas y los umbrales específicos que desee y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="46526-192">On the **Add Alert Rule** page, configure the appropriate properties and the specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="46526-193">![agregar regla de alerta](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="46526-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="46526-194">Actuar sobre los datos de Azure SQL Analytics</span><span class="sxs-lookup"><span data-stu-id="46526-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="46526-195">A modo de ejemplo, una de las consultas más útiles que puede realizar es comparar el uso de DTU de todos los grupos elásticos de Azure SQL de todas sus suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="46526-195">As an example, one of the most useful queries that you can perform is to compare the DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="46526-196">La unidad de rendimiento de base de datos (DTU) proporciona una manera de describir la capacidad relativa de un nivel de rendimiento de las bases de datos y grupos elásticos de los niveles Básico, Estándar y Premium.</span><span class="sxs-lookup"><span data-stu-id="46526-196">Database Throughput Unit (DTU) provides a way to describe the relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="46526-197">Las DTU se basan en una medición combinada de CPU, memoria y número de lecturas y escrituras.</span><span class="sxs-lookup"><span data-stu-id="46526-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="46526-198">A medida que aumentan las DTU, aumenta la capacidad que ofrece el nivel de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="46526-198">As DTUs increase, the power offered by the performance level increases.</span></span> <span data-ttu-id="46526-199">Por ejemplo, un nivel de rendimiento con 5 DTU es cinco veces más potente que un nivel de rendimiento con 1 DTU.</span><span class="sxs-lookup"><span data-stu-id="46526-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="46526-200">Se aplica una cuota máxima de DTU para cada servidor y grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="46526-200">A maximum DTU quota applies to each server and elastic pool.</span></span>

<span data-ttu-id="46526-201">Si ejecuta la siguiente consulta de búsqueda de registros, podrá saber fácilmente si sus grupos elásticos de Azure SQL se están utilizando por debajo de sus posibilidades o en exceso.</span><span class="sxs-lookup"><span data-stu-id="46526-201">By running the following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="46526-202">Si el área de trabajo se ha actualizado al [nuevo lenguaje de consulta de Log Analytics](log-analytics-log-search-upgrade.md), la consulta anterior cambiaría como sigue.</span><span class="sxs-lookup"><span data-stu-id="46526-202">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="46526-203">En el ejemplo siguiente, puede ver que un grupo elástico tiene un uso elevado de casi el 100% de DTU, mientras que otros tienen muy poco uso.</span><span class="sxs-lookup"><span data-stu-id="46526-203">In the following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="46526-204">Puede investigar más en profundidad para solucionar los posibles cambios recientes de su entorno mediante los registros de actividad de Azure.</span><span class="sxs-lookup"><span data-stu-id="46526-204">You can investigate further to troubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Resultados de la búsqueda de registros: uso intensivo](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="46526-206">Consulte también</span><span class="sxs-lookup"><span data-stu-id="46526-206">See also</span></span>

- <span data-ttu-id="46526-207">Use [Búsquedas de registros](log-analytics-log-searches.md) en Log Analytics para ver datos detallados de Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="46526-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed Azure SQL data.</span></span>
- <span data-ttu-id="46526-208">[Cree sus propios paneles](log-analytics-dashboards.md) que muestren datos de Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="46526-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="46526-209">[Cree alertas](log-analytics-alerts.md) cuando se produzcan eventos específicos de Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="46526-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
