---
title: "Métricas y registros de diagnóstico de Azure SQL Database | Microsoft Docs"
description: "Aprenda a configurar el recurso Azure SQL Database para almacenar estadísticas de uso de recursos, conectividad y ejecución de consultas."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: bf41aa530c68ea0e94a09d1dab63237c6f42bce7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="3544c-103">Métricas y registros de diagnóstico de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3544c-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="3544c-104">Azure SQL Database puede emitir métricas y registros de diagnóstico para facilitar la supervisión.</span><span class="sxs-lookup"><span data-stu-id="3544c-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="3544c-105">Azure SQL Database se puede configurar para que almacene el uso de recursos, los trabajadores y las sesiones y la conectividad en uno de estos recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="3544c-105">You can configure Azure SQL Database to store resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="3544c-106">**Azure Storage**: para archivar grandes cantidades de telemetría a un pequeño precio</span><span class="sxs-lookup"><span data-stu-id="3544c-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="3544c-107">**Centro de eventos de Azure**: para integrar la telemetría de Azure SQL Database con la solución de supervisión personalizada o las canalizaciones activas</span><span class="sxs-lookup"><span data-stu-id="3544c-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="3544c-108">**Azure Log Analytics**: para la solución de supervisión integrada con funcionalidades de generación de informes, alertas y mitigación</span><span class="sxs-lookup"><span data-stu-id="3544c-108">**Azure Log Analytics**: For out of the box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![arquitectura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="3544c-110">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="3544c-110">Enable logging</span></span>

<span data-ttu-id="3544c-111">Las métricas y los registros de diagnóstico no están habilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3544c-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="3544c-112">Puede habilitar y administrar las métricas y los registros de diagnóstico con uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3544c-112">You can enable and manage metrics and diagnostics logging using one of the following methods:</span></span>
- <span data-ttu-id="3544c-113">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3544c-113">Azure portal</span></span>
- <span data-ttu-id="3544c-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3544c-114">PowerShell</span></span>
- <span data-ttu-id="3544c-115">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3544c-115">Azure CLI</span></span>
- <span data-ttu-id="3544c-116">API de REST</span><span class="sxs-lookup"><span data-stu-id="3544c-116">REST API</span></span> 
- <span data-ttu-id="3544c-117">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3544c-117">Resource Manager template</span></span>

<span data-ttu-id="3544c-118">Al habilitar las métricas y los registros de diagnóstico, debe especificar el recurso de Azure donde se recopilan los datos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="3544c-118">When you enable metrics and diagnostics logging, you need to specify the Azure resource where selected data is collected.</span></span> <span data-ttu-id="3544c-119">Opciones disponibles:</span><span class="sxs-lookup"><span data-stu-id="3544c-119">Options available:</span></span>
- <span data-ttu-id="3544c-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3544c-120">Log analytics</span></span>
- <span data-ttu-id="3544c-121">Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="3544c-121">Event Hub</span></span>
- <span data-ttu-id="3544c-122">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="3544c-122">Azure Storage</span></span> 

<span data-ttu-id="3544c-123">Puede aprovisionar un nuevo recurso de Azure o seleccionar uno existente.</span><span class="sxs-lookup"><span data-stu-id="3544c-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="3544c-124">Después de seleccionar el recurso de almacenamiento, debe especificar qué datos se van a recopilar.</span><span class="sxs-lookup"><span data-stu-id="3544c-124">After selecting the storage resource, you need to specify which data to collect.</span></span> <span data-ttu-id="3544c-125">Las opciones disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="3544c-125">Options available include:</span></span>

- <span data-ttu-id="3544c-126">**[Métricas de 1 minuto](sql-database-metrics-diag-logging.md#1-minute-metrics)**: contiene porcentaje de DTU; límite de DTU; porcentaje de CPU; porcentaje de lectura de datos físicos; porcentaje de escritura en registro; conexiones correctas, erróneas o bloqueadas por el firewall; porcentaje de sesiones; porcentaje de trabajadores; almacenamiento; porcentaje de almacenamiento y porcentaje de almacenamiento de XTP.</span><span class="sxs-lookup"><span data-stu-id="3544c-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="3544c-127">Si especifica una cuenta de Centro de eventos o Azure Storage, puede indicar una directiva de retención para especificar que los datos que sean más antiguos que un período de tiempo seleccionado se eliminen.</span><span class="sxs-lookup"><span data-stu-id="3544c-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy to specify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="3544c-128">Si especifica Log Analytics, la directiva de retención depende del plan de tarifa seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3544c-128">If you specify Log Analytics, the retention policy depends on the selected pricing tier.</span></span> <span data-ttu-id="3544c-129">Más información sobre [Log Analytics Precios](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="3544c-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="3544c-130">Se recomienda leer los artículos [Información general sobre las métricas en Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [Información general sobre los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) para comprender no solo cómo habilitar los registros, sino también las categorías de métricas y registro que admiten los distintos servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="3544c-130">We recommend that you read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="3544c-131">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3544c-131">Azure portal</span></span>

<span data-ttu-id="3544c-132">Para habilitar la recopilación de métricas y registros de diagnóstico en Azure Portal, vaya a la página de Azure SQL Database o del grupo elástico y haga clic en **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="3544c-132">To enable metrics and diagnostic logs collection in the Azure portal, navigate to your Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![habilitar en Azure Portal](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="3544c-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3544c-134">PowerShell</span></span>

<span data-ttu-id="3544c-135">Para habilitar las métricas y los registros de diagnóstico con PowerShell, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3544c-135">To enable metrics and diagnostics logging using PowerShell, use the following commands:</span></span>

- <span data-ttu-id="3544c-136">Para habilitar el almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="3544c-136">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="3544c-137">El identificador de la cuenta de almacenamiento es el identificador de recurso para la cuenta de almacenamiento a la que desea enviar los registros.</span><span class="sxs-lookup"><span data-stu-id="3544c-137">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="3544c-138">Para habilitar el streaming de registros de diagnóstico a un centro de eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="3544c-138">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="3544c-139">El id. de regla de bus de servicio es una cadena con este formato:</span><span class="sxs-lookup"><span data-stu-id="3544c-139">The Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="3544c-140">Para habilitar el envío de registros de diagnóstico a un área de trabajo de Log Analytics, use este comando:</span><span class="sxs-lookup"><span data-stu-id="3544c-140">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="3544c-141">Puede obtener el identificador de recurso de su área de trabajo de Log Analytics con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="3544c-141">You can obtain the resource id of your Log Analytics workspace using the following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="3544c-142">Puede combinar estos parámetros para habilitar varias opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="3544c-142">You can combine these parameters to enable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="3544c-143">CLI</span><span class="sxs-lookup"><span data-stu-id="3544c-143">CLI</span></span>

<span data-ttu-id="3544c-144">Para habilitar las métricas y los registros de diagnóstico con CLI de Azure, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3544c-144">To enable metrics and diagnostics logging using the Azure CLI, use the following commands:</span></span>

- <span data-ttu-id="3544c-145">Para habilitar el almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="3544c-145">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="3544c-146">El identificador de la cuenta de almacenamiento es el identificador de recurso para la cuenta de almacenamiento a la que desea enviar los registros.</span><span class="sxs-lookup"><span data-stu-id="3544c-146">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="3544c-147">Para habilitar el streaming de registros de diagnóstico a un centro de eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="3544c-147">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="3544c-148">El id. de regla de bus de servicio es una cadena con este formato:</span><span class="sxs-lookup"><span data-stu-id="3544c-148">The Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="3544c-149">Para habilitar el envío de registros de diagnóstico a un área de trabajo de Log Analytics, use este comando:</span><span class="sxs-lookup"><span data-stu-id="3544c-149">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

<span data-ttu-id="3544c-150">Puede combinar estos parámetros para habilitar varias opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="3544c-150">You can combine these parameters to enable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="3544c-151">API de REST</span><span class="sxs-lookup"><span data-stu-id="3544c-151">REST API</span></span>

<span data-ttu-id="3544c-152">Lea sobre cómo [cambiar la configuración de diagnóstico con la API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="3544c-152">Read about how to [change Diagnostic settings using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="3544c-153">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3544c-153">Resource Manager template</span></span>

<span data-ttu-id="3544c-154">Lea sobre cómo [habilitar la configuración de diagnóstico al crear recursos con la plantilla de Resource Manager](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="3544c-154">Read about how to [enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="3544c-155">Transmisión a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3544c-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="3544c-156">Las métricas y los registros de diagnóstico de Azure SQL Database se pueden transmitir a Log Analytics mediante la opción integrada "Enviar a Log Analytics" del portal o al habilitar Log Analytics en una configuración de diagnóstico por medio de cmdlets de Azure PowerShell, CLI de Azure o API de REST de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="3544c-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using the built-in “Send to Log Analytics” option in the portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="3544c-157">Introducción a la instalación</span><span class="sxs-lookup"><span data-stu-id="3544c-157">Installation overview</span></span>

<span data-ttu-id="3544c-158">La supervisión de la línea de Azure SQL Database es sencilla con Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3544c-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="3544c-159">Se necesitan tres pasos:</span><span class="sxs-lookup"><span data-stu-id="3544c-159">Three steps are required:</span></span>

1.  <span data-ttu-id="3544c-160">Crear el recurso Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3544c-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="3544c-161">Configurar bases de datos para registrar las métricas y los registros de diagnóstico en el recurso Log Analytics creado</span><span class="sxs-lookup"><span data-stu-id="3544c-161">Configure databases to record metrics and diagnostic logs into the created Log Analytics</span></span>
3.  <span data-ttu-id="3544c-162">Instalar la solución **Azure SQL Analytics** desde la galería en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3544c-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="3544c-163">Crear el recurso Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3544c-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="3544c-164">Haga clic en **Nuevo** en el menú del lateral izquierdo.</span><span class="sxs-lookup"><span data-stu-id="3544c-164">Click **New** in the left-hand menu.</span></span>
2. <span data-ttu-id="3544c-165">Haga clic en **Supervisión y administración**.</span><span class="sxs-lookup"><span data-stu-id="3544c-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="3544c-166">Haga clic en **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3544c-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="3544c-167">Rellene el formulario de Log Analytics con la información adicional necesaria: nombre de área de trabajo, suscripción, grupo de recursos, ubicación y plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="3544c-167">Fill in the Log Analytics form with the additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-to-record-metrics-and-diagnostic-logs"></a><span data-ttu-id="3544c-169">Configurar bases de datos para registrar las métricas y los registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="3544c-169">Configure databases to record metrics and diagnostic logs</span></span>

<span data-ttu-id="3544c-170">La manera más sencilla de configurar la ubicación en que las bases de datos registran sus métricas es mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3544c-170">The easiest way to configure where databases record their metrics is through the Azure portal.</span></span> <span data-ttu-id="3544c-171">En Azure Portal, vaya al recurso Azure SQL Database y haga clic en **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="3544c-171">In the Azure portal, navigate to your Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-the-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="3544c-172">Instalar la solución Azure SQL Analytics desde la galería</span><span class="sxs-lookup"><span data-stu-id="3544c-172">Install the Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="3544c-173">Una vez que el recurso Log Analytics se ha creado y que los datos están llegando a él, instale la solución Azure SQL Analytics.</span><span class="sxs-lookup"><span data-stu-id="3544c-173">Once the Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="3544c-174">Puede hacerlo mediante la **Galería de soluciones**, que encontrará en la página principal de OMS y en el menú lateral.</span><span class="sxs-lookup"><span data-stu-id="3544c-174">This can be done through the **Solutions Gallery** that you can find on the OMS homepage and in the side menu.</span></span> <span data-ttu-id="3544c-175">En la galería, busque y haga clic en la solución **Azure SQL Analytics** y luego en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3544c-175">In the gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![solución de supervisión](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="3544c-177">En la página principal de OMS aparece un nuevo icono llamado **Azure SQL Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3544c-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="3544c-178">Al seleccionar este icono se abre el panel de Azure SQL Analytics.</span><span class="sxs-lookup"><span data-stu-id="3544c-178">Selecting this tile opens the Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="3544c-179">Uso de la solución Azure SQL Analytics</span><span class="sxs-lookup"><span data-stu-id="3544c-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="3544c-180">Azure SQL Analytics es un panel jerárquico que permite navegar por la jerarquía de recursos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3544c-180">Azure SQL Analytics is a hierarchical dashboard that allows you to navigate through the hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="3544c-181">Esta capacidad permite realizar supervisión de alto nivel y además limitar la supervisión a solo el conjunto adecuado de recursos.</span><span class="sxs-lookup"><span data-stu-id="3544c-181">This capability enables you to do high-level monitoring but it also enables you to scope your monitoring to just the right set of resources.</span></span>
<span data-ttu-id="3544c-182">El panel contiene las listas de los recursos incluidos en el recurso seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3544c-182">Dashboard contains the lists of different resources under the selected resource.</span></span> <span data-ttu-id="3544c-183">Por ejemplo, en una suscripción seleccionada puede ver todos los servidores, los grupos elásticos y las bases de datos que pertenecen a esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="3544c-183">For example, for a selected subscription you can see the all servers, elastic pools and databases that belong to the selected subscription.</span></span> <span data-ttu-id="3544c-184">Además, en los grupos elásticos y las bases de datos puede ver las métricas de uso de ese recurso.</span><span class="sxs-lookup"><span data-stu-id="3544c-184">Additionally, for Elastic Pools and databases, you can see the resource usage metrics of that resource.</span></span> <span data-ttu-id="3544c-185">Esto incluye gráficos de DTU, CPU, E/S, registro, sesiones, trabajadores, conexiones y almacenamiento en GB.</span><span class="sxs-lookup"><span data-stu-id="3544c-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="3544c-186">Transmisión al Centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="3544c-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="3544c-187">Las métricas y los registros de diagnóstico de Azure SQL Database se pueden transmitir al Centro de eventos mediante la opción integrada "Transmitir a un centro de eventos" del portal o al habilitar el id. de regla de bus de servicio en una configuración de diagnóstico por medio de cmdlets de Azure PowerShell, CLI de Azure o API de REST de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="3544c-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using the built-in “Stream to an event hub” option in the portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-to-do-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="3544c-188">Utilidad de las métricas y los registros de diagnóstico del Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="3544c-188">What to do with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="3544c-189">Una vez que los datos seleccionados se transmiten al Centro de eventos, está un paso más cerca de habilitar escenarios de supervisión avanzados.</span><span class="sxs-lookup"><span data-stu-id="3544c-189">Once the selected data is streamed into Event Hub, you are one step closer to enabling advanced monitoring scenarios.</span></span> <span data-ttu-id="3544c-190">Centros de eventos actúa como la "puerta principal" de una canalización de eventos y, una vez que los datos se recopilan en un Centro de eventos, se pueden transformar y almacenar con cualquier proveedor de análisis en tiempo real o adaptadores de procesamiento por lotes/almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3544c-190">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="3544c-191">Centros de eventos desacopla la producción de un flujo de eventos desde el consumo de los eventos, para que los consumidores de eventos pueden tener acceso a los eventos según su propia programación.</span><span class="sxs-lookup"><span data-stu-id="3544c-191">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span> <span data-ttu-id="3544c-192">Para más información sobre el Centro de eventos, vea:</span><span class="sxs-lookup"><span data-stu-id="3544c-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="3544c-193">[¿Qué es Azure Event Hubs?](../event-hubs/event-hubs-what-is-event-hubs.md)</span><span class="sxs-lookup"><span data-stu-id="3544c-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="3544c-194">Introducción a Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3544c-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="3544c-195">Estas son solo algunas formas en que se podría usar la funcionalidad de transmisión:</span><span class="sxs-lookup"><span data-stu-id="3544c-195">Here are just a few ways you might use the streaming capability:</span></span>

-   <span data-ttu-id="3544c-196">Visualización del estado del servicio mediante la transmisión de datos de "ruta de acceso activa" a PowerBI: con Event Hubs, Stream Analytics y Power BI, puede transformar fácilmente las métricas y los datos de diagnóstico en información prácticamente en tiempo real sobre los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="3544c-196">View service health by streaming “hot path” data to PowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="3544c-197">Para obtener una introducción sobre cómo configurar Event Hubs, procesar datos con Stream Analytics y usar Power BI como salida, vea [Stream Analytics y Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="3544c-197">For an overview of how to set up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="3544c-198">Transmisión de registros a registros de terceros y flujos de telemetría: con la transmisión de Event Hubs puede enviar las métricas y los registros de diagnóstico a distintas soluciones de supervisión y análisis de registros de terceros.</span><span class="sxs-lookup"><span data-stu-id="3544c-198">Stream logs to third-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in to different third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="3544c-199">Creación de una plataforma personalizada de registro y telemetría: si ya tiene una plataforma de telemetría personalizada o está pensando en crear una, la naturaleza altamente escalable de suscripción y publicación de Event Hubs permite introducir registros de diagnóstico de manera flexible.</span><span class="sxs-lookup"><span data-stu-id="3544c-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="3544c-200">Vea la [guía de Dan Rosanova para usar Event Hubs en una plataforma de telemetría de escala global](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="3544c-200">See [Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="3544c-201">Transmisión a Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3544c-201">Stream into Azure Storage</span></span>

<span data-ttu-id="3544c-202">Las métricas y los registros de diagnóstico de Azure SQL Database se pueden almacenar en Azure Storage mediante la opción integrada "Archivar en una cuenta de almacenamiento" de Azure Portal o al habilitar Azure Storage en una configuración de diagnóstico por medio de cmdlets de Azure PowerShell, CLI de Azure o API de REST de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="3544c-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using the built-in "Archive to a storage account” option in the Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="3544c-203">Esquema de métricas y registros de diagnóstico en la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3544c-203">Schema of metrics and diagnostic logs in the storage account</span></span>

<span data-ttu-id="3544c-204">Una vez que ha configurado la recopilación de métricas y los registros de diagnóstico, se crea un contenedor de almacenamiento en la cuenta de almacenamiento seleccionada cuando las primeras filas de datos están disponibles.</span><span class="sxs-lookup"><span data-stu-id="3544c-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in the storage account you selected when the first rows of data are available.</span></span> <span data-ttu-id="3544c-205">La estructura de estos blobs es:</span><span class="sxs-lookup"><span data-stu-id="3544c-205">The structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="3544c-206">O, sencillamente:</span><span class="sxs-lookup"><span data-stu-id="3544c-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="3544c-207">Por ejemplo, un nombre de blob para métricas de 1 minuto podría ser:</span><span class="sxs-lookup"><span data-stu-id="3544c-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="3544c-208">Si quiere registrar los datos del grupo elástico, el nombre de blob es un poco distinto:</span><span class="sxs-lookup"><span data-stu-id="3544c-208">In case you want to record the data from the Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="3544c-209">Descargar métricas y registros de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3544c-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="3544c-210">Vea [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) (Descargar métricas y registros de diagnóstico de Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="3544c-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="3544c-211">métricas de 1 minuto</span><span class="sxs-lookup"><span data-stu-id="3544c-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="3544c-212">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="3544c-212">**Resource**</span></span>|<span data-ttu-id="3544c-213">**Métricas**</span><span class="sxs-lookup"><span data-stu-id="3544c-213">**Metrics**</span></span>|
|<span data-ttu-id="3544c-214">Base de datos</span><span class="sxs-lookup"><span data-stu-id="3544c-214">Database</span></span>|<span data-ttu-id="3544c-215">Porcentaje de DTU; DTU usada; límite de DTU; porcentaje de CPU; porcentaje de lectura de datos físicos; porcentaje de escritura en registro; conexiones correctas, erróneas o bloqueadas por el firewall; porcentaje de sesiones; porcentaje de trabajadores; almacenamiento; porcentaje de almacenamiento; porcentaje de almacenamiento de XTP e interbloqueos</span><span class="sxs-lookup"><span data-stu-id="3544c-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="3544c-216">Grupo elástico</span><span class="sxs-lookup"><span data-stu-id="3544c-216">Elastic pool</span></span>|<span data-ttu-id="3544c-217">porcentaje de eDTU; eDTUusada; límite de eDTU; porcentaje de CPU; porcentaje de lectura de datos físicos; porcentaje de escritura en registro; porcentaje de sesiones; porcentaje de trabajadores; almacenamiento; porcentaje de almacenamiento; límite de almacenamiento y porcentaje de almacenamiento de XTP</span><span class="sxs-lookup"><span data-stu-id="3544c-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3544c-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3544c-218">Next steps</span></span>

- <span data-ttu-id="3544c-219">Lea los artículos [Información general sobre las métricas en Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [Información general sobre los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) para comprender no solo cómo habilitar los registros, sino también las categorías de métricas y registro que admiten los distintos servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="3544c-219">Read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>
- <span data-ttu-id="3544c-220">Lea estos artículos para obtener información sobre Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="3544c-220">Read these articles to learn about event hubs:</span></span>
   - <span data-ttu-id="3544c-221">[¿Qué es Azure Event Hubs?](../event-hubs/event-hubs-what-is-event-hubs.md)</span><span class="sxs-lookup"><span data-stu-id="3544c-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="3544c-222">Introducción a Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3544c-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="3544c-223">Vea [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) (Descargar métricas y registros de diagnóstico de Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="3544c-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
