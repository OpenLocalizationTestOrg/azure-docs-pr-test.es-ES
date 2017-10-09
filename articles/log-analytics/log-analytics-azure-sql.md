---
title: "solución de análisis de SQL de análisis de registros aaaAzure | Documentos de Microsoft"
description: "Hola solución de análisis de SQL Azure le ayuda a administrar las bases de datos de SQL Azure."
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
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="d7f9c-103">Supervisión de Azure SQL Database mediante Azure SQL Analytics (versión preliminar) en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d7f9c-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Símbolo de Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="d7f9c-105">Hola soluciones de análisis de SQL Azure en Azure Log Analytics recopila y muestra las métricas de rendimiento importantes de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="d7f9c-106">Mediante el uso de las métricas de Hola que se recopilan con soluciones de hello, puede crear alertas y reglas de supervisión personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="d7f9c-107">Y puede supervisar Azure SQL Database y las métricas de los grupos elásticos de varias suscripciones y grupos elásticos de Azure y visualizarlos.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="d7f9c-108">solución de Hello también ayuda a problemas de tooidentify en cada nivel de la pila de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="d7f9c-109">Usa [métricas de diagnóstico de Azure](log-analytics-azure-storage.md) junto con el análisis de registros ve toopresent datos sobre todas las bases de datos SQL de Azure y los grupos elásticos en una sola área de trabajo de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="d7f9c-110">Actualmente, esta solución de vista previa admite hasta too150 000 bases de datos de SQL Azure y 5.000 grupos elásticos SQL por área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="d7f9c-111">Hola soluciones de análisis de SQL Azure, al igual que otras personas disponibles para el análisis de registros, le ayuda a supervisar y recibir notificaciones sobre el estado de saludo de los recursos de Azure, en este caso, la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="d7f9c-112">Base de datos de SQL de Microsoft Azure es un servicio de base de datos relacional escalable que ofrece familiarizado tooapplications de capacidades de tipo de servidor de SQL ejecuta Hola nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="d7f9c-113">Análisis de registros permite toocollect, correlacionar y visualizar los datos estructurados y no estructurados.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="d7f9c-114">Orígenes conectados</span><span class="sxs-lookup"><span data-stu-id="d7f9c-114">Connected sources</span></span>

<span data-ttu-id="d7f9c-115">Hola solución de análisis de SQL Azure no usa agentes tooconnect toohello servicio de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="d7f9c-116">Hello en la tabla siguiente describe los orígenes de hello conectado que son compatibles con esta solución.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="d7f9c-117">Origen conectado</span><span class="sxs-lookup"><span data-stu-id="d7f9c-117">Connected Source</span></span> | <span data-ttu-id="d7f9c-118">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="d7f9c-118">Support</span></span> | <span data-ttu-id="d7f9c-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="d7f9c-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="d7f9c-120">Agentes de Windows</span><span class="sxs-lookup"><span data-stu-id="d7f9c-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="d7f9c-121">No</span><span class="sxs-lookup"><span data-stu-id="d7f9c-121">No</span></span> | <span data-ttu-id="d7f9c-122">Solución de hello no se utiliza agentes directa de Windows.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="d7f9c-123">Agentes de Linux</span><span class="sxs-lookup"><span data-stu-id="d7f9c-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="d7f9c-124">No</span><span class="sxs-lookup"><span data-stu-id="d7f9c-124">No</span></span> | <span data-ttu-id="d7f9c-125">No se utilizan agentes Linux directa solución Hola.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="d7f9c-126">Grupo de administración de SCOM</span><span class="sxs-lookup"><span data-stu-id="d7f9c-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="d7f9c-127">No</span><span class="sxs-lookup"><span data-stu-id="d7f9c-127">No</span></span> | <span data-ttu-id="d7f9c-128">No se utiliza una conexión directa de hello SCOM agente tooLog análisis solución Hola.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="d7f9c-129">Cuenta de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d7f9c-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="d7f9c-130">No</span><span class="sxs-lookup"><span data-stu-id="d7f9c-130">No</span></span> | <span data-ttu-id="d7f9c-131">Análisis de registros no leen datos de Hola desde una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="d7f9c-132">Diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="d7f9c-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="d7f9c-133">Sí</span><span class="sxs-lookup"><span data-stu-id="d7f9c-133">Yes</span></span> | <span data-ttu-id="d7f9c-134">Se envían datos de métrica Azure tooLog Analytics directamente en Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="d7f9c-135">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d7f9c-135">Prerequisites</span></span>

- <span data-ttu-id="d7f9c-136">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-136">An Azure Subscription.</span></span> <span data-ttu-id="d7f9c-137">Si no tiene ninguna, puede crear una [gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d7f9c-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="d7f9c-138">Un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-138">A Log Analytics workspace.</span></span> <span data-ttu-id="d7f9c-139">Puede usar una existente, o bien puede [crear una nueva](log-analytics-get-started.md) para empezar a usar esta solución.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="d7f9c-140">Habilitar los diagnósticos de Azure para sus bases de datos SQL de Azure y los grupos elásticos y [configurarlos toosend su análisis de datos tooLog](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="d7f9c-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="d7f9c-141">Configuración</span><span class="sxs-lookup"><span data-stu-id="d7f9c-141">Configuration</span></span>

<span data-ttu-id="d7f9c-142">Realizar Hola después de área de trabajo tooyour de solución de análisis de SQL Azure de pasos tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="d7f9c-143">Agregar área de trabajo de hello análisis de SQL Azure solución tooyour de [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="d7f9c-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="d7f9c-144">Hola portal de Azure, haga clic en **New** (símbolo + hello), a continuación, en lista Hola de recursos, seleccione **supervisión + administración**.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="d7f9c-145">![Supervisión + Administración](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="d7f9c-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="d7f9c-146">Hola **supervisión + administración** lista, haga clic **ver todas**.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="d7f9c-147">Hola **recomendado** lista, haga clic en **más** y, a continuación, en la nueva lista de hello, busque **análisis de SQL Azure (vista previa)** y, a continuación, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="d7f9c-148">![Solución Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="d7f9c-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="d7f9c-149">Hola **análisis de SQL Azure (vista previa)** hoja, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="d7f9c-150">![Creación](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="d7f9c-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="d7f9c-151">Hola **crear nueva solución** hoja, área de trabajo de hello select que desea tooadd Hola solución tooand, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="d7f9c-152">![Agregar tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="d7f9c-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="d7f9c-153">tooconfigure varias suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d7f9c-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="d7f9c-154">toosupport varias suscripciones, use el script de PowerShell de Hola desde [registro de las métricas de recursos de habilitar Azure mediante PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="d7f9c-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="d7f9c-155">Proporcionar Id. de recurso del área de trabajo de Hola como un parámetro al ejecutar los datos de diagnóstico toosend hello secuencia de comandos de recursos del área de trabajo de una suscripción de Azure tooa en otra suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="d7f9c-156">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="d7f9c-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="d7f9c-157">Uso de solución de Hola</span><span class="sxs-lookup"><span data-stu-id="d7f9c-157">Using hello solution</span></span>

<span data-ttu-id="d7f9c-158">Cuando se agrega el área de trabajo de hello solución tooyour, Hola icono de análisis de SQL Azure se agrega el área de trabajo de tooyour y aparece en información general.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="d7f9c-159">icono de Hello muestra hello de bases de datos SQL de Azure y grupos elásticos SQL de Azure que Hola solución está conectada a.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Icono de Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="d7f9c-161">Visualización de los datos de Azure SQL Analytics</span><span class="sxs-lookup"><span data-stu-id="d7f9c-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="d7f9c-162">Haga clic en hello **el análisis de SQL Azure** icono tooopen Hola o panel de análisis de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="d7f9c-163">panel de Hello incluye módulos de hello definidas a continuación.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="d7f9c-164">Cada hoja se enumera los recursos de too15 (suscripción, server, grupo elástico y base de datos).</span><span class="sxs-lookup"><span data-stu-id="d7f9c-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="d7f9c-165">Haga clic en cualquier panel de Hola Hola recursos tooopen para ese recurso específico.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="d7f9c-166">Base de datos o grupo elástico contiene gráficos de hello con métricas para un recurso seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="d7f9c-167">Haga clic en un cuadro de diálogo de búsqueda de registros de gráfico tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="d7f9c-168">Hoja</span><span class="sxs-lookup"><span data-stu-id="d7f9c-168">Blade</span></span> | <span data-ttu-id="d7f9c-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="d7f9c-169">Description</span></span> |
|---|---|
| <span data-ttu-id="d7f9c-170">Suscripciones</span><span class="sxs-lookup"><span data-stu-id="d7f9c-170">Subscriptions</span></span> | <span data-ttu-id="d7f9c-171">Lista de las suscripciones con el número de servidores conectados, los grupos y las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="d7f9c-172">Servidores</span><span class="sxs-lookup"><span data-stu-id="d7f9c-172">Servers</span></span> | <span data-ttu-id="d7f9c-173">Lista de servidores con el número de grupos conectados y las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="d7f9c-174">Grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="d7f9c-174">Elastic Pools</span></span> | <span data-ttu-id="d7f9c-175">Lista de grupos elásticos conectados con máximo GB y eDTU Hola observados período.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="d7f9c-176">Bases de datos</span><span class="sxs-lookup"><span data-stu-id="d7f9c-176">Databases</span></span> | <span data-ttu-id="d7f9c-177">Lista de bases de datos conectadas con máximo GB y DTU en hello observados período.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="d7f9c-178">Análisis de datos y creación de alertas</span><span class="sxs-lookup"><span data-stu-id="d7f9c-178">Analyze data and create alerts</span></span>

<span data-ttu-id="d7f9c-179">Puede crear fácilmente alertas con datos de hello procedentes de recursos de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="d7f9c-180">Estas son un par de consultas de [búsqueda de registros](log-analytics-log-searches.md) útiles que puede usar para las alertas:</span><span class="sxs-lookup"><span data-stu-id="d7f9c-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="d7f9c-181">*DTU alta en Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="d7f9c-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="d7f9c-182">*DTU alta en el grupo elástico de Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="d7f9c-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="d7f9c-183">Puede usar estos tooalert de las consultas basadas en la alerta en umbrales específicos para la base de datos de SQL Azure y grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="d7f9c-184">tooconfigure una alerta para el área de trabajo OMS:</span><span class="sxs-lookup"><span data-stu-id="d7f9c-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="d7f9c-185">tooconfigure una alerta para el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="d7f9c-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="d7f9c-186">Vaya toohello [portal de OMS](http://mms.microsoft.com/) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="d7f9c-187">Abra el área de trabajo de Hola que ha configurado para la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="d7f9c-188">En la página de información general de hello, haga clic en hello **análisis de SQL Azure (vista previa)** icono.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="d7f9c-189">Ejecute una de las consultas de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="d7f9c-190">En Búsqueda de registros, haga clic en **Alerta**.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="d7f9c-191">![crear alerta en la búsqueda](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="d7f9c-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="d7f9c-192">En hello **Agregar regla de alerta** página, configure las propiedades adecuadas de Hola y Hola umbrales específicos que desee y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="d7f9c-193">![agregar regla de alerta](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="d7f9c-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="d7f9c-194">Actuar sobre los datos de Azure SQL Analytics</span><span class="sxs-lookup"><span data-stu-id="d7f9c-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="d7f9c-195">Por ejemplo, una de las consultas más útiles Hola que puede realizar es uso de la DTU toocompare Hola para todos los grupos de elástico de SQL Azure en todas sus suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="d7f9c-196">Unidad de rendimiento de base de datos (DTU) proporciona una manera toodescribe Hola capacidad relativa de un nivel de rendimiento de las bases de datos Basic, Standard y Premium y grupos.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="d7f9c-197">Las DTU se basan en una medición combinada de CPU, memoria y número de lecturas y escrituras.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="d7f9c-198">A medida que aumentan las Dtu, Hola potencia que ofrece aumenta de nivel de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="d7f9c-199">Por ejemplo, un nivel de rendimiento con 5 DTU es cinco veces más potente que un nivel de rendimiento con 1 DTU.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="d7f9c-200">Una cuota DTU máxima aplica tooeach grupo de servidor y flexible.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="d7f9c-201">Al ejecutar Hola después de consulta de búsqueda de registros, puede indicar fácilmente si están utilizando poco o uso en los grupos elásticos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="d7f9c-202">Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de la consulta cambiaría toohello siguiente.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="d7f9c-203">En el siguiente ejemplo de Hola, puede ver que un grupo elástico tiene un uso elevado de casi el 100% DTU mientras que otros tienen muy poco uso.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="d7f9c-204">Puede investigar más tootroubleshoot posibles cambios recientes en su entorno usando los registros de actividad de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Resultados de la búsqueda de registros: uso intensivo](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="d7f9c-206">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d7f9c-206">See also</span></span>

- <span data-ttu-id="d7f9c-207">Use [búsquedas de registros](log-analytics-log-searches.md) en tooview de análisis de registros detallados de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="d7f9c-208">[Cree sus propios paneles](log-analytics-dashboards.md) que muestren datos de Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="d7f9c-209">[Cree alertas](log-analytics-alerts.md) cuando se produzcan eventos específicos de Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="d7f9c-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
