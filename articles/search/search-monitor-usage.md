---
title: "Supervisión del uso y estadísticas en un servicio Azure Search | Microsoft Docs"
description: "Realice el seguimiento del consumo de recursos y el tamaño de índice para Azure Search, un servicio de búsqueda hospedado en la nube en Microsoft Azure."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: 16cb5a1e16a59200f0e731622398efcf24c3f777
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-an-azure-search-service"></a><span data-ttu-id="b75fa-103">Supervisión de un servicio de Azure Search</span><span class="sxs-lookup"><span data-stu-id="b75fa-103">Monitoring an Azure Search service</span></span>

<span data-ttu-id="b75fa-104">Azure Search ofrece varios recursos para realizar el seguimiento del uso y rendimiento de los servicios de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b75fa-104">Azure Search offers various resources for tracking usage and performance of search services.</span></span> <span data-ttu-id="b75fa-105">Proporciona acceso a métricas, registros, estadísticas de índices y funcionalidades de supervisión extendidas en Power BI.</span><span class="sxs-lookup"><span data-stu-id="b75fa-105">It gives you access to metrics, logs, index statistics, and extended monitoring capabilities on Power BI.</span></span> <span data-ttu-id="b75fa-106">En este artículo se describe cómo habilitar las diferentes estrategias de supervisión y cómo interpretar los datos resultantes.</span><span class="sxs-lookup"><span data-stu-id="b75fa-106">This article describes how to enable the different monitoring strategies and how to interpret the resulting data.</span></span>

## <a name="azure-search-metrics"></a><span data-ttu-id="b75fa-107">Métricas de Azure Search</span><span class="sxs-lookup"><span data-stu-id="b75fa-107">Azure Search metrics</span></span>
<span data-ttu-id="b75fa-108">Las métricas ofrecen visibilidad casi en tiempo real de cualquier servicio de búsqueda y están disponibles para todos los servicios, no es preciso realizar ningún tipo de configuración adicional.</span><span class="sxs-lookup"><span data-stu-id="b75fa-108">Metrics give you near real-time visibility into your search service and are available for every service, with no additional setup.</span></span> <span data-ttu-id="b75fa-109">Le permiten realizar el seguimiento del rendimiento del servicio durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="b75fa-109">They let you track the performance of your service for up to 30 days.</span></span>

<span data-ttu-id="b75fa-110">Azure Search recopila datos de tres métricas diferentes:</span><span class="sxs-lookup"><span data-stu-id="b75fa-110">Azure Search collects data for three different metrics:</span></span>

* <span data-ttu-id="b75fa-111">Latencia de búsqueda: tiempo que ha necesitado el servicio de búsqueda para procesar las consultas de búsqueda, agregadas por minuto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-111">Search latency: Time the search service needed to process search queries, aggregated per minute.</span></span>
* <span data-ttu-id="b75fa-112">Consultas de búsqueda por segundo (QPS): número de consultas de búsqueda recibidas por segundo, agregadas por minuto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-112">Search queries per second (QPS): Number of search queries received per second, aggregated per minute.</span></span>
* <span data-ttu-id="b75fa-113">Porcentaje de consultas de búsqueda limitadas: porcentaje de consultas de búsqueda que se han limitado, agregadas por minuto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-113">Throttled search queries percentage: Percentage of search queries that were throttled, aggregated per minute.</span></span>

![Captura de pantalla de la actividad de QPS][1]

### <a name="set-up-alerts"></a><span data-ttu-id="b75fa-115">Configuración de alertas</span><span class="sxs-lookup"><span data-stu-id="b75fa-115">Set up alerts</span></span>
<span data-ttu-id="b75fa-116">En la página de detalles de la métrica puede configurar alertas para desencadenar una notificación por correo electrónico o una acción automática cuando una métrica supera un umbral definido.</span><span class="sxs-lookup"><span data-stu-id="b75fa-116">From the metric detail page, you can configure alerts to trigger an email notification or an automated action when a metric crosses a threshold that you have defined.</span></span>

<span data-ttu-id="b75fa-117">Para más información acerca de las métricas, consulte la documentación completa de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="b75fa-117">For more information about metrics, check the full documentation on Azure Monitor.</span></span>  

## <a name="how-to-track-resource-usage"></a><span data-ttu-id="b75fa-118">Realización del seguimiento del uso de los recursos</span><span class="sxs-lookup"><span data-stu-id="b75fa-118">How to track resource usage</span></span>
<span data-ttu-id="b75fa-119">Llevar un seguimiento del crecimiento de los índices y el tamaño de los documentos puede ayudarle a ajustar la capacidad de forma proactiva antes de alcanzar el límite superior que haya establecido para el servicio.</span><span class="sxs-lookup"><span data-stu-id="b75fa-119">Tracking the growth of indexes and document size can help you proactively adjust capacity before hitting the upper limit you've established for your service.</span></span> <span data-ttu-id="b75fa-120">También puede hacerlo en el portal o mediante programación con la API de REST.</span><span class="sxs-lookup"><span data-stu-id="b75fa-120">You can do this on the portal or programmatically using the REST API.</span></span>

### <a name="using-the-portal"></a><span data-ttu-id="b75fa-121">Uso del portal</span><span class="sxs-lookup"><span data-stu-id="b75fa-121">Using the portal</span></span>

<span data-ttu-id="b75fa-122">Para supervisar el uso de recursos, y ver los recuentos y las estadísticas del servicio en el [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b75fa-122">To monitor resource usage, view the counts and statistics for your service in the [portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="b75fa-123">Inicie sesión en el [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b75fa-123">Sign in to the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b75fa-124">Abra el panel del servicio Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b75fa-124">Open the service dashboard of your Azure Search service.</span></span> <span data-ttu-id="b75fa-125">Puede buscar los mosaicos del servicio en la página principal, o puede desplazarse hasta el servicio usando Explorar, en la barra de salto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-125">Tiles for the service can be found on the Home page, or you can browse to the service from Browse on the JumpBar.</span></span>

<span data-ttu-id="b75fa-126">La sección Uso incluye un medidor que indica la parte de los recursos disponibles que está en uso.</span><span class="sxs-lookup"><span data-stu-id="b75fa-126">The Usage section includes a meter that tells you what portion of available resources are currently in use.</span></span> <span data-ttu-id="b75fa-127">Para más información sobre los límites de cada servicio en cuanto a índices, documentos y almacenamiento, consulte [Límites de servicio](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="b75fa-127">For information on per-service limits for indexes, documents, and storage, see [Service limits](search-limits-quotas-capacity.md).</span></span>

  ![Icono de Uso][2]

> [!NOTE]
> <span data-ttu-id="b75fa-129">La captura de pantalla anterior es del servicio Gratuito, que tiene como máximo una réplica y una partición y solo puede hospedar 3 índices, 10 000 documentos o 50 MB de datos, lo que ocurra primero.</span><span class="sxs-lookup"><span data-stu-id="b75fa-129">The screenshot above is for the Free service, which has a maximum of one replica and partition each, and can only host 3 indexes, 10,000 documents, or 50 MB of data, whichever comes first.</span></span> <span data-ttu-id="b75fa-130">Los servicios creados en un nivel Básico o Estándar tienen límites de servicio mucho mayores.</span><span class="sxs-lookup"><span data-stu-id="b75fa-130">Services created at a Basic or Standard tier have much larger service limits.</span></span> <span data-ttu-id="b75fa-131">Para más información sobre cómo elegir un nivel, consulte [Selección de un nivel o una SKU](search-sku-tier.md).</span><span class="sxs-lookup"><span data-stu-id="b75fa-131">For more information on choosing a tier, see [Choose a tier or SKU](search-sku-tier.md).</span></span>
>
>

### <a name="using-the-rest-api"></a><span data-ttu-id="b75fa-132">Uso de la API de REST</span><span class="sxs-lookup"><span data-stu-id="b75fa-132">Using the REST API</span></span>
<span data-ttu-id="b75fa-133">La API de REST de Azure Search y el SDK para .NET proporcionan acceso mediante programación a las métricas del servicio.</span><span class="sxs-lookup"><span data-stu-id="b75fa-133">Both the Azure Search REST API and the .NET SDK provide programmatic access to service metrics.</span></span>  <span data-ttu-id="b75fa-134">Si está utilizando [indexadores](https://msdn.microsoft.com/library/azure/dn946891.aspx) para cargar un índice desde Azure SQL Database o desde Azure Cosmos DB, está disponible una API adicional para obtener las cifras que necesita.</span><span class="sxs-lookup"><span data-stu-id="b75fa-134">If you are using [indexers](https://msdn.microsoft.com/library/azure/dn946891.aspx) to load an index from Azure SQL Database or Azure Cosmos DB, an additional API is available to get the numbers you require.</span></span>

* [<span data-ttu-id="b75fa-135">Obtención de estadísticas de índice</span><span class="sxs-lookup"><span data-stu-id="b75fa-135">Get Index Statistics</span></span>](/rest/api/searchservice/get-index-statistics)
* [<span data-ttu-id="b75fa-136">Recuento de documentos</span><span class="sxs-lookup"><span data-stu-id="b75fa-136">Count Documents</span></span>](/rest/api/searchservice/count-documents)
* [<span data-ttu-id="b75fa-137">Obtención del estado del indizador</span><span class="sxs-lookup"><span data-stu-id="b75fa-137">Get Indexer Status</span></span>](/rest/api/searchservice/get-indexer-status)

## <a name="how-to-export-logs-and-metrics"></a><span data-ttu-id="b75fa-138">Exportación de registros y métricas</span><span class="sxs-lookup"><span data-stu-id="b75fa-138">How to export logs and metrics</span></span>

<span data-ttu-id="b75fa-139">Puede exportar los registros de operaciones de un servicio y los datos sin procesar de las métricas que se describen en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="b75fa-139">You can export the operation logs for your service and the raw data for the metrics described in the preceding section.</span></span> <span data-ttu-id="b75fa-140">Los registros de operaciones le permiten saber cómo se utiliza el servicio y se pueden consumir desde Power BI cuando se copian datos en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b75fa-140">Operation logs let you know how the service is being used and can be consumed from Power BI when data is copied to a storage account.</span></span> <span data-ttu-id="b75fa-141">Azure Search proporciona un paquete de contenido de supervisión de Power BI para este fin.</span><span class="sxs-lookup"><span data-stu-id="b75fa-141">Azure search provides a monitoring Power BI content pack for this purpose.</span></span>


### <a name="enabling-monitoring"></a><span data-ttu-id="b75fa-142">Habilitación de la supervisión</span><span class="sxs-lookup"><span data-stu-id="b75fa-142">Enabling monitoring</span></span>
<span data-ttu-id="b75fa-143">Abra el servicio Azure Search en [Azure Portal](http://portal.azure.com), en la opción Habilitar supervisión.</span><span class="sxs-lookup"><span data-stu-id="b75fa-143">Open your Azure Search service in the [Azure portal](http://portal.azure.com) under the Enable Monitoring option.</span></span>

<span data-ttu-id="b75fa-144">Elija los datos que desea exportar: registros, métricas o ambos.</span><span class="sxs-lookup"><span data-stu-id="b75fa-144">Choose the data you want to export: Logs, Metrics or both.</span></span> <span data-ttu-id="b75fa-145">Puede copiarlos en una cuenta de almacenamiento, enviarlos a un centro de eventos o exportarlo a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b75fa-145">You can copy it to a storage account, send it to an event hub or export it to Log Analytics.</span></span>

![Habilitación de la supervisión en el portal][3]

<span data-ttu-id="b75fa-147">Para habilitar el uso de PowerShell o la CLI de Azure, consulte la documentación [aquí](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="b75fa-147">To enable using PowerShell or the Azure CLI, see the documentation [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).</span></span>

### <a name="logs-and-metrics-schemas"></a><span data-ttu-id="b75fa-148">Registros y esquemas de métricas</span><span class="sxs-lookup"><span data-stu-id="b75fa-148">Logs and metrics schemas</span></span>
<span data-ttu-id="b75fa-149">Cuando los datos se copian en una cuenta de almacenamiento, adoptan el formato JSON y se colocan en dos contenedores:</span><span class="sxs-lookup"><span data-stu-id="b75fa-149">When the data is copied to a storage account, the data is formatted as JSON and it's place in two containers:</span></span>

* <span data-ttu-id="b75fa-150">insights-logs-operationlogs: para los registros del tráfico de búsqueda</span><span class="sxs-lookup"><span data-stu-id="b75fa-150">insights-logs-operationlogs: for search traffic logs</span></span>
* <span data-ttu-id="b75fa-151">insights-metrics-pt1m: para las métricas</span><span class="sxs-lookup"><span data-stu-id="b75fa-151">insights-metrics-pt1m: for metrics</span></span>

<span data-ttu-id="b75fa-152">Hay un blob, por hora y por contenedor.</span><span class="sxs-lookup"><span data-stu-id="b75fa-152">There is one blob, per hour, per container.</span></span>

<span data-ttu-id="b75fa-153">Ruta de acceso de ejemplo: `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="b75fa-153">Example path: `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`</span></span>

#### <a name="log-schema"></a><span data-ttu-id="b75fa-154">Esquema de registro</span><span class="sxs-lookup"><span data-stu-id="b75fa-154">Log schema</span></span>
<span data-ttu-id="b75fa-155">Los blobs de registros contienen los registros de tráfico del servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b75fa-155">The logs blobs contain your search service traffic logs.</span></span>
<span data-ttu-id="b75fa-156">Cada blob tiene un objeto raíz llamado **registros** que contiene una matriz de objetos de registro.</span><span class="sxs-lookup"><span data-stu-id="b75fa-156">Each blob has one root object called **records** that contains an array of log objects.</span></span>
<span data-ttu-id="b75fa-157">Cada blob tiene registros en todas las operaciones que tuvieron lugar durante la misma hora.</span><span class="sxs-lookup"><span data-stu-id="b75fa-157">Each blob has records on all the operation that took place during the same hour.</span></span>

| <span data-ttu-id="b75fa-158">Nombre</span><span class="sxs-lookup"><span data-stu-id="b75fa-158">Name</span></span> | <span data-ttu-id="b75fa-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="b75fa-159">Type</span></span> | <span data-ttu-id="b75fa-160">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="b75fa-160">Example</span></span> | <span data-ttu-id="b75fa-161">Notas</span><span class="sxs-lookup"><span data-stu-id="b75fa-161">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b75fa-162">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="b75fa-162">time</span></span> |<span data-ttu-id="b75fa-163">datetime</span><span class="sxs-lookup"><span data-stu-id="b75fa-163">datetime</span></span> |<span data-ttu-id="b75fa-164">"2015-12-07T00:00:43.6872559Z"</span><span class="sxs-lookup"><span data-stu-id="b75fa-164">"2015-12-07T00:00:43.6872559Z"</span></span> |<span data-ttu-id="b75fa-165">Marca de tiempo de la operación</span><span class="sxs-lookup"><span data-stu-id="b75fa-165">Timestamp of the operation</span></span> |
| <span data-ttu-id="b75fa-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="b75fa-166">resourceId</span></span> |<span data-ttu-id="b75fa-167">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-167">string</span></span> |<span data-ttu-id="b75fa-168">"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/</span><span class="sxs-lookup"><span data-stu-id="b75fa-168">"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/</span></span><br/><span data-ttu-id="b75fa-169">RESOURCEGROUPS/DEFAULT/PROVIDERS/</span><span class="sxs-lookup"><span data-stu-id="b75fa-169">RESOURCEGROUPS/DEFAULT/PROVIDERS/</span></span><br/> <span data-ttu-id="b75fa-170">MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE"</span><span class="sxs-lookup"><span data-stu-id="b75fa-170">MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE"</span></span> |<span data-ttu-id="b75fa-171">Su ResourceId</span><span class="sxs-lookup"><span data-stu-id="b75fa-171">Your ResourceId</span></span> |
| <span data-ttu-id="b75fa-172">operationName</span><span class="sxs-lookup"><span data-stu-id="b75fa-172">operationName</span></span> |<span data-ttu-id="b75fa-173">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-173">string</span></span> |<span data-ttu-id="b75fa-174">"Query.Search"</span><span class="sxs-lookup"><span data-stu-id="b75fa-174">"Query.Search"</span></span> |<span data-ttu-id="b75fa-175">El nombre de la operación</span><span class="sxs-lookup"><span data-stu-id="b75fa-175">The name of the operation</span></span> |
| <span data-ttu-id="b75fa-176">operationVersion</span><span class="sxs-lookup"><span data-stu-id="b75fa-176">operationVersion</span></span> |<span data-ttu-id="b75fa-177">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-177">string</span></span> |<span data-ttu-id="b75fa-178">"2015-02-28"</span><span class="sxs-lookup"><span data-stu-id="b75fa-178">"2015-02-28"</span></span> |<span data-ttu-id="b75fa-179">La versión de la API usada</span><span class="sxs-lookup"><span data-stu-id="b75fa-179">The api-version used</span></span> |
| <span data-ttu-id="b75fa-180">categoría</span><span class="sxs-lookup"><span data-stu-id="b75fa-180">category</span></span> |<span data-ttu-id="b75fa-181">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-181">string</span></span> |<span data-ttu-id="b75fa-182">"OperationLogs"</span><span class="sxs-lookup"><span data-stu-id="b75fa-182">"OperationLogs"</span></span> |<span data-ttu-id="b75fa-183">constant</span><span class="sxs-lookup"><span data-stu-id="b75fa-183">constant</span></span> |
| <span data-ttu-id="b75fa-184">resultType</span><span class="sxs-lookup"><span data-stu-id="b75fa-184">resultType</span></span> |<span data-ttu-id="b75fa-185">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-185">string</span></span> |<span data-ttu-id="b75fa-186">"Success"</span><span class="sxs-lookup"><span data-stu-id="b75fa-186">"Success"</span></span> |<span data-ttu-id="b75fa-187">Valores posibles: Success o Failure</span><span class="sxs-lookup"><span data-stu-id="b75fa-187">Possible values: Success or Failure</span></span> |
| <span data-ttu-id="b75fa-188">resultSignature</span><span class="sxs-lookup"><span data-stu-id="b75fa-188">resultSignature</span></span> |<span data-ttu-id="b75fa-189">int</span><span class="sxs-lookup"><span data-stu-id="b75fa-189">int</span></span> |<span data-ttu-id="b75fa-190">200</span><span class="sxs-lookup"><span data-stu-id="b75fa-190">200</span></span> |<span data-ttu-id="b75fa-191">Código de resultado HTTP</span><span class="sxs-lookup"><span data-stu-id="b75fa-191">HTTP result code</span></span> |
| <span data-ttu-id="b75fa-192">durationMS</span><span class="sxs-lookup"><span data-stu-id="b75fa-192">durationMS</span></span> |<span data-ttu-id="b75fa-193">int</span><span class="sxs-lookup"><span data-stu-id="b75fa-193">int</span></span> |<span data-ttu-id="b75fa-194">50</span><span class="sxs-lookup"><span data-stu-id="b75fa-194">50</span></span> |<span data-ttu-id="b75fa-195">Duración de la operación en milisegundos</span><span class="sxs-lookup"><span data-stu-id="b75fa-195">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="b75fa-196">propiedades</span><span class="sxs-lookup"><span data-stu-id="b75fa-196">properties</span></span> |<span data-ttu-id="b75fa-197">objeto</span><span class="sxs-lookup"><span data-stu-id="b75fa-197">object</span></span> |<span data-ttu-id="b75fa-198">consulte la tabla siguiente</span><span class="sxs-lookup"><span data-stu-id="b75fa-198">see the following table</span></span> |<span data-ttu-id="b75fa-199">Objeto que contiene datos específicos de la operación</span><span class="sxs-lookup"><span data-stu-id="b75fa-199">Object containing operation-specific data</span></span> |

<span data-ttu-id="b75fa-200">**Esquema de propiedades**</span><span class="sxs-lookup"><span data-stu-id="b75fa-200">**Properties schema**</span></span>
| <span data-ttu-id="b75fa-201">Nombre</span><span class="sxs-lookup"><span data-stu-id="b75fa-201">Name</span></span> | <span data-ttu-id="b75fa-202">Tipo</span><span class="sxs-lookup"><span data-stu-id="b75fa-202">Type</span></span> | <span data-ttu-id="b75fa-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="b75fa-203">Example</span></span> | <span data-ttu-id="b75fa-204">Notas</span><span class="sxs-lookup"><span data-stu-id="b75fa-204">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b75fa-205">Description</span><span class="sxs-lookup"><span data-stu-id="b75fa-205">Description</span></span> |<span data-ttu-id="b75fa-206">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-206">string</span></span> |<span data-ttu-id="b75fa-207">"GET /indexes('content')/docs"</span><span class="sxs-lookup"><span data-stu-id="b75fa-207">"GET /indexes('content')/docs"</span></span> |<span data-ttu-id="b75fa-208">Punto de conexión de la operación</span><span class="sxs-lookup"><span data-stu-id="b75fa-208">The operation's endpoint</span></span> |
| <span data-ttu-id="b75fa-209">Consultar</span><span class="sxs-lookup"><span data-stu-id="b75fa-209">Query</span></span> |<span data-ttu-id="b75fa-210">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-210">string</span></span> |<span data-ttu-id="b75fa-211">"?search=AzureSearch&$count=true&api-version=2015-02-28"</span><span class="sxs-lookup"><span data-stu-id="b75fa-211">"?search=AzureSearch&$count=true&api-version=2015-02-28"</span></span> |<span data-ttu-id="b75fa-212">Los parámetros de consulta</span><span class="sxs-lookup"><span data-stu-id="b75fa-212">The query parameters</span></span> |
| <span data-ttu-id="b75fa-213">Documentos</span><span class="sxs-lookup"><span data-stu-id="b75fa-213">Documents</span></span> |<span data-ttu-id="b75fa-214">int</span><span class="sxs-lookup"><span data-stu-id="b75fa-214">int</span></span> |<span data-ttu-id="b75fa-215">42</span><span class="sxs-lookup"><span data-stu-id="b75fa-215">42</span></span> |<span data-ttu-id="b75fa-216">Número de documentos procesados</span><span class="sxs-lookup"><span data-stu-id="b75fa-216">Number of documents processed</span></span> |
| <span data-ttu-id="b75fa-217">IndexName</span><span class="sxs-lookup"><span data-stu-id="b75fa-217">IndexName</span></span> |<span data-ttu-id="b75fa-218">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-218">string</span></span> |<span data-ttu-id="b75fa-219">"testindex"</span><span class="sxs-lookup"><span data-stu-id="b75fa-219">"testindex"</span></span> |<span data-ttu-id="b75fa-220">Nombre del índice asociado a la operación</span><span class="sxs-lookup"><span data-stu-id="b75fa-220">Name of the index associated with the operation</span></span> |

#### <a name="metrics-schema"></a><span data-ttu-id="b75fa-221">Esquema de métricas</span><span class="sxs-lookup"><span data-stu-id="b75fa-221">Metrics schema</span></span>
| <span data-ttu-id="b75fa-222">Nombre</span><span class="sxs-lookup"><span data-stu-id="b75fa-222">Name</span></span> | <span data-ttu-id="b75fa-223">Tipo</span><span class="sxs-lookup"><span data-stu-id="b75fa-223">Type</span></span> | <span data-ttu-id="b75fa-224">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="b75fa-224">Example</span></span> | <span data-ttu-id="b75fa-225">Notas</span><span class="sxs-lookup"><span data-stu-id="b75fa-225">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b75fa-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="b75fa-226">resourceId</span></span> |<span data-ttu-id="b75fa-227">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-227">string</span></span> |<span data-ttu-id="b75fa-228">"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/</span><span class="sxs-lookup"><span data-stu-id="b75fa-228">"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/</span></span><br/><span data-ttu-id="b75fa-229">RESOURCEGROUPS/DEFAULT/PROVIDERS/</span><span class="sxs-lookup"><span data-stu-id="b75fa-229">RESOURCEGROUPS/DEFAULT/PROVIDERS/</span></span><br/><span data-ttu-id="b75fa-230">MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE"</span><span class="sxs-lookup"><span data-stu-id="b75fa-230">MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE"</span></span> |<span data-ttu-id="b75fa-231">el identificador de recurso</span><span class="sxs-lookup"><span data-stu-id="b75fa-231">your resource id</span></span> |
| <span data-ttu-id="b75fa-232">metricName</span><span class="sxs-lookup"><span data-stu-id="b75fa-232">metricName</span></span> |<span data-ttu-id="b75fa-233">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-233">string</span></span> |<span data-ttu-id="b75fa-234">"Latency"</span><span class="sxs-lookup"><span data-stu-id="b75fa-234">"Latency"</span></span> |<span data-ttu-id="b75fa-235">el nombre de la métrica</span><span class="sxs-lookup"><span data-stu-id="b75fa-235">the name of the metric</span></span> |
| <span data-ttu-id="b75fa-236">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="b75fa-236">time</span></span> |<span data-ttu-id="b75fa-237">datetime</span><span class="sxs-lookup"><span data-stu-id="b75fa-237">datetime</span></span> |<span data-ttu-id="b75fa-238">"2015-12-07T00:00:43.6872559Z"</span><span class="sxs-lookup"><span data-stu-id="b75fa-238">"2015-12-07T00:00:43.6872559Z"</span></span> |<span data-ttu-id="b75fa-239">la marca de tiempo de la operación</span><span class="sxs-lookup"><span data-stu-id="b75fa-239">the operation's timestamp</span></span> |
| <span data-ttu-id="b75fa-240">average</span><span class="sxs-lookup"><span data-stu-id="b75fa-240">average</span></span> |<span data-ttu-id="b75fa-241">int</span><span class="sxs-lookup"><span data-stu-id="b75fa-241">int</span></span> |<span data-ttu-id="b75fa-242">64</span><span class="sxs-lookup"><span data-stu-id="b75fa-242">64</span></span> |<span data-ttu-id="b75fa-243">El valor de media de las muestras sin procesar en el intervalo de tiempo de la métrica</span><span class="sxs-lookup"><span data-stu-id="b75fa-243">The average value of the raw samples in the metric time interval</span></span> |
| <span data-ttu-id="b75fa-244">minimum</span><span class="sxs-lookup"><span data-stu-id="b75fa-244">minimum</span></span> |<span data-ttu-id="b75fa-245">int</span><span class="sxs-lookup"><span data-stu-id="b75fa-245">int</span></span> |<span data-ttu-id="b75fa-246">37</span><span class="sxs-lookup"><span data-stu-id="b75fa-246">37</span></span> |<span data-ttu-id="b75fa-247">El valor mínimo de las muestras sin procesar en el intervalo de tiempo de la métrica</span><span class="sxs-lookup"><span data-stu-id="b75fa-247">The minimum value of the raw samples in the metric time interval</span></span> |
| <span data-ttu-id="b75fa-248">maximum</span><span class="sxs-lookup"><span data-stu-id="b75fa-248">maximum</span></span> |<span data-ttu-id="b75fa-249">int</span><span class="sxs-lookup"><span data-stu-id="b75fa-249">int</span></span> |<span data-ttu-id="b75fa-250">78</span><span class="sxs-lookup"><span data-stu-id="b75fa-250">78</span></span> |<span data-ttu-id="b75fa-251">El valor máximo de las muestras sin procesar en el intervalo de tiempo de la métrica</span><span class="sxs-lookup"><span data-stu-id="b75fa-251">The maximum value of the raw samples in the metric time interval</span></span> |
| <span data-ttu-id="b75fa-252">total</span><span class="sxs-lookup"><span data-stu-id="b75fa-252">total</span></span> |<span data-ttu-id="b75fa-253">int</span><span class="sxs-lookup"><span data-stu-id="b75fa-253">int</span></span> |<span data-ttu-id="b75fa-254">258</span><span class="sxs-lookup"><span data-stu-id="b75fa-254">258</span></span> |<span data-ttu-id="b75fa-255">El valor total de las muestras sin procesar en el intervalo de tiempo de la métrica</span><span class="sxs-lookup"><span data-stu-id="b75fa-255">The total value of the raw samples in the metric time interval</span></span> |
| <span data-ttu-id="b75fa-256">count</span><span class="sxs-lookup"><span data-stu-id="b75fa-256">count</span></span> |<span data-ttu-id="b75fa-257">int</span><span class="sxs-lookup"><span data-stu-id="b75fa-257">int</span></span> |<span data-ttu-id="b75fa-258">4</span><span class="sxs-lookup"><span data-stu-id="b75fa-258">4</span></span> |<span data-ttu-id="b75fa-259">El número de muestras sin procesar usadas para generar la métrica</span><span class="sxs-lookup"><span data-stu-id="b75fa-259">The number of raw samples used to generate the metric</span></span> |
| <span data-ttu-id="b75fa-260">timegrain</span><span class="sxs-lookup"><span data-stu-id="b75fa-260">timegrain</span></span> |<span data-ttu-id="b75fa-261">string</span><span class="sxs-lookup"><span data-stu-id="b75fa-261">string</span></span> |<span data-ttu-id="b75fa-262">"PT1M"</span><span class="sxs-lookup"><span data-stu-id="b75fa-262">"PT1M"</span></span> |<span data-ttu-id="b75fa-263">El intervalo de agregación de la métrica en ISO 8601</span><span class="sxs-lookup"><span data-stu-id="b75fa-263">The time grain of the metric in ISO 8601</span></span> |

<span data-ttu-id="b75fa-264">Todas las métricas se notifican en intervalos de un minuto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-264">All metrics are reported in one-minute intervals.</span></span> <span data-ttu-id="b75fa-265">Cada métrica expone los valores mínimo, máximo y promedio por minuto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-265">Every metric exposes minimum, maximum and average values per minute.</span></span>

<span data-ttu-id="b75fa-266">En el caso de la métrica SearchQueriesPerSecond, el mínimo es el valor más bajo de las consultas de búsqueda por segundo que se registró en ese minuto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-266">For the SearchQueriesPerSecond metric, minimum is the lowest value for search queries per second that was registered during that minute.</span></span> <span data-ttu-id="b75fa-267">Lo mismo sucede con el valor máximo.</span><span class="sxs-lookup"><span data-stu-id="b75fa-267">The same applies to the maximum value.</span></span> <span data-ttu-id="b75fa-268">El promedio es el agregado en todo el minuto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-268">Average, is the aggregate across the entire minute.</span></span>
<span data-ttu-id="b75fa-269">Piense en este escenario durante un minuto: un segundo de carga elevada que es el máximo en SearchQueriesPerSecond, seguido de 58 segundos de carga media y, por último, 1 segundo con solo una consulta (que es el mínimo).</span><span class="sxs-lookup"><span data-stu-id="b75fa-269">Think about this scenario during one minute: one second of high load that is the maximum for SearchQueriesPerSecond, followed by 58 seconds of average load, and finally one second with only one query, which is the minimum.</span></span>

<span data-ttu-id="b75fa-270">En el caso de ThrottledSearchQueriesPercentage, el mínimo, máximo, promedio y total tendrán el mismo valor: el porcentaje de consultas de búsqueda con limitaciones, del número total de consultas de búsqueda durante un minuto.</span><span class="sxs-lookup"><span data-stu-id="b75fa-270">For ThrottledSearchQueriesPercentage, minimum, maximum, average and total, all have the same value: the percentage of search queries that were throttled, from the total number of search queries during one minute.</span></span>

## <a name="analyzing-your-data-with-power-bi"></a><span data-ttu-id="b75fa-271">Análisis de datos con Power BI</span><span class="sxs-lookup"><span data-stu-id="b75fa-271">Analyzing your data With Power BI</span></span>

<span data-ttu-id="b75fa-272">Se recomienda usar [Power BI](https://powerbi.microsoft.com) para explorar y visualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="b75fa-272">We recommend using [Power BI](https://powerbi.microsoft.com) to explore and visualize your data.</span></span> <span data-ttu-id="b75fa-273">Se puede conectar fácilmente a su cuenta de Azure Storage y empezar rápidamente a analizar los datos.</span><span class="sxs-lookup"><span data-stu-id="b75fa-273">You can easily connect it to your Azure Storage Account and quickly start analyzing your data.</span></span>

<span data-ttu-id="b75fa-274">Azure Search proporciona un [paquete de contenido de Power BI](https://app.powerbi.com/getdata/services/azure-search) que le permite supervisar y conocer el tráfico de búsqueda con las tablas y gráficos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="b75fa-274">Azure Search provides a [Power BI Content Pack](https://app.powerbi.com/getdata/services/azure-search) that allows you to monitor and understand your search traffic with predefined charts and tables.</span></span> <span data-ttu-id="b75fa-275">Contiene un conjunto de informes de Power BI que se conectan automáticamente a sus datos y proporcionan información visual sobre el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b75fa-275">It contains a set of Power BI reports that automatically connect to your data and provide visual insights about your search service.</span></span> <span data-ttu-id="b75fa-276">Para más información, consulte la [página de ayuda del paquete de contenido](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="b75fa-276">For more information, see the [content pack help page](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).</span></span>

![Panel de Power BI para Azure Search][4]

## <a name="next-steps"></a><span data-ttu-id="b75fa-278">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b75fa-278">Next steps</span></span>
<span data-ttu-id="b75fa-279">Examine [Escalado de réplicas y particiones](search-limits-quotas-capacity.md) como guía saber cómo equilibrar la asignación de particiones y réplicas para un servicio existente.</span><span class="sxs-lookup"><span data-stu-id="b75fa-279">Review [Scale replicas and partitions](search-limits-quotas-capacity.md) for guidance on how to balance the allocation of partitions and replicas for an existing service.</span></span>

<span data-ttu-id="b75fa-280">Visite [Administración de servicios de Azure Search en Microsoft Azure](search-manage.md) para más información sobre la administración de servicios, o [Rendimiento y optimización](search-performance-optimization.md) para que le sirva de guía de ajuste.</span><span class="sxs-lookup"><span data-stu-id="b75fa-280">Visit [Manage your Search service on Microsoft Azure](search-manage.md) for more information on service administration, or [Performance and optimization](search-performance-optimization.md) for tuning guidance.</span></span>

<span data-ttu-id="b75fa-281">Obtenga más información sobre cómo crear informes increíbles.</span><span class="sxs-lookup"><span data-stu-id="b75fa-281">Learn more about creating amazing reports.</span></span> <span data-ttu-id="b75fa-282">Consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/) para obtener más información</span><span class="sxs-lookup"><span data-stu-id="b75fa-282">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png