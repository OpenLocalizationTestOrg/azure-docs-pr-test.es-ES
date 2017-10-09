---
title: "las métricas de almacenamiento de aaaEnabling Hola portal de Azure | Documentos de Microsoft"
description: "¿Cómo tooenable las métricas de almacenamiento para Hola servicios Blob, cola, tabla y archivo"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="e0b65-103">Habilitar las métricas de almacenamiento de Azure y ver sus datos</span><span class="sxs-lookup"><span data-stu-id="e0b65-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="e0b65-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e0b65-104">Overview</span></span>
<span data-ttu-id="e0b65-105">Las métricas de almacenamiento se habilitan de forma predeterminada al crear una nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0b65-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="e0b65-106">Puede configurar la supervisión a través de hello [portal de Azure](https://portal.azure.com) o Windows PowerShell, o mediante programación a través de una de las bibliotecas de cliente de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="e0b65-107">Puede configurar un período de retención de datos de métricas de hello: este período determina cuánto almacenamiento Hola servicio mantiene las métricas de Hola y cargos de hello espacio necesario toostore ellos.</span><span class="sxs-lookup"><span data-stu-id="e0b65-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="e0b65-108">Por lo general, debe usar un período de retención más corto para métricas por minuto de métricas por hora debido a Hola considerable espacio adicional requerido para las métricas de minuto.</span><span class="sxs-lookup"><span data-stu-id="e0b65-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="e0b65-109">Debe elegir un período de retención de forma que tiene suficiente tiempo tooanalyze Hola datos y descargar todas las métricas que se va tookeep para análisis sin conexión o de elaboración de informes.</span><span class="sxs-lookup"><span data-stu-id="e0b65-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="e0b65-110">Recuerde que también se le facturará por la descarga de los datos de métricas desde su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0b65-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="e0b65-111">Cómo las métricas de tooenable con Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e0b65-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="e0b65-112">Siga estas métricas de tooenable pasos Hola [portal de Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="e0b65-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="e0b65-113">Navegue tooyour cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0b65-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="e0b65-114">Seleccione **diagnósticos** en hello **menú** hoja</span><span class="sxs-lookup"><span data-stu-id="e0b65-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="e0b65-115">Asegúrese de que **estado** se establece demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="e0b65-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="e0b65-116">Las métricas de hello SELECT para los servicios de hello desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e0b65-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="e0b65-117">Especificar un tooindicate de directiva de retención cuánto datos de métricas y registro de tooretain.</span><span class="sxs-lookup"><span data-stu-id="e0b65-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="e0b65-118">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e0b65-118">Select **Save**.</span></span>

<span data-ttu-id="e0b65-119">Tenga en cuenta que hello [portal de Azure](https://portal.azure.com) no permite actualmente tooconfigure métricas por minuto en su cuenta de almacenamiento; debe habilitar las métricas de minuto con PowerShell o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="e0b65-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="e0b65-120">Cómo las métricas de tooenable con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0b65-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="e0b65-121">Puede usar PowerShell en su tooconfigure de máquina local las métricas de almacenamiento en su cuenta de almacenamiento mediante la configuración actual de hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve Hola y Hola cmdlet Configuración actual de Set-AzureStorageServiceMetricsProperty toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="e0b65-122">cmdlets de Hola que controlan las métricas de almacenamiento usan Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0b65-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="e0b65-123">Los valores posibles de MetricsType son Hour y Minute.</span><span class="sxs-lookup"><span data-stu-id="e0b65-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="e0b65-124">Los valores posibles de ServiceType son Blob, Queue y Table.</span><span class="sxs-lookup"><span data-stu-id="e0b65-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="e0b65-125">Los valores posibles de MetricsLevel son None, Service y ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="e0b65-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="e0b65-126">Por ejemplo, hello comando siguiente activa el minuto las métricas para servicio de Blob de hello en su cuenta de almacenamiento predeterminada con el período de retención de hello definir los días de toofive:</span><span class="sxs-lookup"><span data-stu-id="e0b65-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="e0b65-127">Hello comando siguiente recupera Hola actual por hora métricas nivel y retención de los días para servicio de blob de hello en su cuenta de almacenamiento predeterminada:</span><span class="sxs-lookup"><span data-stu-id="e0b65-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="e0b65-128">Para obtener información acerca de cómo tooconfigure hello Azure PowerShell cmdlets toowork con su suscripción de Azure y cómo tooselect Hola almacenamiento predeterminado cuenta toouse, consulte: [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0b65-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="e0b65-129">¿Cómo tooenable las métricas de almacenamiento mediante programación</span><span class="sxs-lookup"><span data-stu-id="e0b65-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="e0b65-130">Hola siguiente fragmento de código C# muestra cómo tooenable métricas y registro para el uso de servicio de Blob de Hola Hola biblioteca cliente de almacenamiento para. NET:</span><span class="sxs-lookup"><span data-stu-id="e0b65-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="e0b65-131">Mostrar Métricas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e0b65-131">Viewing Storage metrics</span></span>
<span data-ttu-id="e0b65-132">Después de configurar la cuenta de almacenamiento toomonitor de métricas de análisis de almacenamiento, el análisis de almacenamiento registra las métricas de hello en un conjunto de tablas conocidas en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0b65-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="e0b65-133">Puede configurar métricas por hora de gráficos tooview Hola [portal de Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="e0b65-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="e0b65-134">Navegar por la cuenta de almacenamiento de tooyour en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0b65-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="e0b65-135">Seleccione **métricas** en hello **menú** hoja para hello servicio cuyas métricas que desee tooview.</span><span class="sxs-lookup"><span data-stu-id="e0b65-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="e0b65-136">Seleccione **editar** en gráfico de hello desea tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="e0b65-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="e0b65-137">Hola **Editar gráfico** hoja, seleccione hello **intervalo de tiempo**, **tipo de gráfico**y las métricas de Hola que desea mostrar en gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="e0b65-138">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e0b65-138">Select **OK**</span></span>

<span data-ttu-id="e0b65-139">Si desea que las métricas de hello toodownload para almacenamiento a largo plazo o tooanalyze ellos localmente, debe:</span><span class="sxs-lookup"><span data-stu-id="e0b65-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="e0b65-140">Utilizar una herramienta que es compatible con estas tablas y se permiten tooview y descargarlos.</span><span class="sxs-lookup"><span data-stu-id="e0b65-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="e0b65-141">Escribir una tooread de aplicación o el script personalizado y almacenar las tablas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="e0b65-142">Muchas herramientas de exploración de almacenamiento de terceros son conscientes de estas tablas y habilitar tooview ellos directamente.</span><span class="sxs-lookup"><span data-stu-id="e0b65-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="e0b65-143">Consulte [Herramientas de cliente de Azure Storage](storage-explorers.md) para obtener una lista de herramientas disponibles.</span><span class="sxs-lookup"><span data-stu-id="e0b65-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="e0b65-144">A partir de la versión 0.8.0 de hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), puede ver y descargar las tablas de métricas de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="e0b65-145">En el análisis de orden tooaccess Hola tablas mediante programación, tenga en cuenta que las tablas de análisis de hello no aparecen si lista todas las tablas de hello en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0b65-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="e0b65-146">Puede tener acceso a ellos directamente por su nombre, o usar hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) Hola .NET cliente biblioteca tooquery hello en nombres de tabla.</span><span class="sxs-lookup"><span data-stu-id="e0b65-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="e0b65-147">Métricas por hora</span><span class="sxs-lookup"><span data-stu-id="e0b65-147">Hourly metrics</span></span>
* <span data-ttu-id="e0b65-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="e0b65-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="e0b65-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="e0b65-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="e0b65-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="e0b65-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="e0b65-151">Métricas por minuto</span><span class="sxs-lookup"><span data-stu-id="e0b65-151">Minute metrics</span></span>
* <span data-ttu-id="e0b65-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="e0b65-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="e0b65-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="e0b65-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="e0b65-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="e0b65-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="e0b65-155">Capacity</span><span class="sxs-lookup"><span data-stu-id="e0b65-155">Capacity</span></span>
* <span data-ttu-id="e0b65-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="e0b65-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="e0b65-157">Puede encontrar detalles completos de los esquemas de Hola para estas tablas en [esquema de tabla de métricas de análisis de almacenamiento](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0b65-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="e0b65-158">filas de ejemplo de Hola a continuación muestran solo un subconjunto de columnas de hello disponibles, pero ilustran algunas características importantes de manera hello que las métricas de almacenamiento guardan estas métricas:</span><span class="sxs-lookup"><span data-stu-id="e0b65-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="e0b65-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="e0b65-159">PartitionKey</span></span> | <span data-ttu-id="e0b65-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="e0b65-160">RowKey</span></span> | <span data-ttu-id="e0b65-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="e0b65-161">Timestamp</span></span> | <span data-ttu-id="e0b65-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="e0b65-162">TotalRequests</span></span> | <span data-ttu-id="e0b65-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="e0b65-163">TotalBillableRequests</span></span> | <span data-ttu-id="e0b65-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="e0b65-164">TotalIngress</span></span> | <span data-ttu-id="e0b65-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="e0b65-165">TotalEgress</span></span> | <span data-ttu-id="e0b65-166">Disponibilidad</span><span class="sxs-lookup"><span data-stu-id="e0b65-166">Availability</span></span> | <span data-ttu-id="e0b65-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="e0b65-167">AverageE2ELatency</span></span> | <span data-ttu-id="e0b65-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="e0b65-168">AverageServerLatency</span></span> | <span data-ttu-id="e0b65-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="e0b65-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e0b65-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e0b65-170">20140522T1100</span></span> |<span data-ttu-id="e0b65-171">user;All</span><span class="sxs-lookup"><span data-stu-id="e0b65-171">user;All</span></span> |<span data-ttu-id="e0b65-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e0b65-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e0b65-173">7</span><span class="sxs-lookup"><span data-stu-id="e0b65-173">7</span></span> |<span data-ttu-id="e0b65-174">7</span><span class="sxs-lookup"><span data-stu-id="e0b65-174">7</span></span> |<span data-ttu-id="e0b65-175">4003</span><span class="sxs-lookup"><span data-stu-id="e0b65-175">4003</span></span> |<span data-ttu-id="e0b65-176">46801</span><span class="sxs-lookup"><span data-stu-id="e0b65-176">46801</span></span> |<span data-ttu-id="e0b65-177">100</span><span class="sxs-lookup"><span data-stu-id="e0b65-177">100</span></span> |<span data-ttu-id="e0b65-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="e0b65-178">104.4286</span></span> |<span data-ttu-id="e0b65-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="e0b65-179">6.857143</span></span> |<span data-ttu-id="e0b65-180">100</span><span class="sxs-lookup"><span data-stu-id="e0b65-180">100</span></span> |
| <span data-ttu-id="e0b65-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e0b65-181">20140522T1100</span></span> |<span data-ttu-id="e0b65-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="e0b65-182">user;QueryEntities</span></span> |<span data-ttu-id="e0b65-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="e0b65-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="e0b65-184">5</span><span class="sxs-lookup"><span data-stu-id="e0b65-184">5</span></span> |<span data-ttu-id="e0b65-185">5</span><span class="sxs-lookup"><span data-stu-id="e0b65-185">5</span></span> |<span data-ttu-id="e0b65-186">2694</span><span class="sxs-lookup"><span data-stu-id="e0b65-186">2694</span></span> |<span data-ttu-id="e0b65-187">45951</span><span class="sxs-lookup"><span data-stu-id="e0b65-187">45951</span></span> |<span data-ttu-id="e0b65-188">100</span><span class="sxs-lookup"><span data-stu-id="e0b65-188">100</span></span> |<span data-ttu-id="e0b65-189">143.8</span><span class="sxs-lookup"><span data-stu-id="e0b65-189">143.8</span></span> |<span data-ttu-id="e0b65-190">7.8</span><span class="sxs-lookup"><span data-stu-id="e0b65-190">7.8</span></span> |<span data-ttu-id="e0b65-191">100</span><span class="sxs-lookup"><span data-stu-id="e0b65-191">100</span></span> |
| <span data-ttu-id="e0b65-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e0b65-192">20140522T1100</span></span> |<span data-ttu-id="e0b65-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="e0b65-193">user;QueryEntity</span></span> |<span data-ttu-id="e0b65-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e0b65-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e0b65-195">1</span><span class="sxs-lookup"><span data-stu-id="e0b65-195">1</span></span> |<span data-ttu-id="e0b65-196">1</span><span class="sxs-lookup"><span data-stu-id="e0b65-196">1</span></span> |<span data-ttu-id="e0b65-197">538</span><span class="sxs-lookup"><span data-stu-id="e0b65-197">538</span></span> |<span data-ttu-id="e0b65-198">633</span><span class="sxs-lookup"><span data-stu-id="e0b65-198">633</span></span> |<span data-ttu-id="e0b65-199">100</span><span class="sxs-lookup"><span data-stu-id="e0b65-199">100</span></span> |<span data-ttu-id="e0b65-200">3</span><span class="sxs-lookup"><span data-stu-id="e0b65-200">3</span></span> |<span data-ttu-id="e0b65-201">3</span><span class="sxs-lookup"><span data-stu-id="e0b65-201">3</span></span> |<span data-ttu-id="e0b65-202">100</span><span class="sxs-lookup"><span data-stu-id="e0b65-202">100</span></span> |
| <span data-ttu-id="e0b65-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e0b65-203">20140522T1100</span></span> |<span data-ttu-id="e0b65-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="e0b65-204">user;UpdateEntity</span></span> |<span data-ttu-id="e0b65-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e0b65-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e0b65-206">1</span><span class="sxs-lookup"><span data-stu-id="e0b65-206">1</span></span> |<span data-ttu-id="e0b65-207">1</span><span class="sxs-lookup"><span data-stu-id="e0b65-207">1</span></span> |<span data-ttu-id="e0b65-208">771</span><span class="sxs-lookup"><span data-stu-id="e0b65-208">771</span></span> |<span data-ttu-id="e0b65-209">217</span><span class="sxs-lookup"><span data-stu-id="e0b65-209">217</span></span> |<span data-ttu-id="e0b65-210">100</span><span class="sxs-lookup"><span data-stu-id="e0b65-210">100</span></span> |<span data-ttu-id="e0b65-211">9</span><span class="sxs-lookup"><span data-stu-id="e0b65-211">9</span></span> |<span data-ttu-id="e0b65-212">6</span><span class="sxs-lookup"><span data-stu-id="e0b65-212">6</span></span> |<span data-ttu-id="e0b65-213">100</span><span class="sxs-lookup"><span data-stu-id="e0b65-213">100</span></span> |

<span data-ttu-id="e0b65-214">En estos datos de métricas por minuto de ejemplo, clave de partición de hello usa tiempo de hello en la resolución de minutos.</span><span class="sxs-lookup"><span data-stu-id="e0b65-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="e0b65-215">clave de fila de Hello identifica el tipo de Hola de información que se almacena en la fila de Hola y se compone de dos partes de información, el tipo de acceso de Hola y el tipo de solicitud de hello:</span><span class="sxs-lookup"><span data-stu-id="e0b65-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="e0b65-216">tipo de acceso de Hello es el usuario o del sistema, donde usuario refiere a servicio de almacenamiento de toohello de las solicitudes de usuario de tooall y sistema toorequests realizadas por el análisis de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0b65-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="e0b65-217">tipo de solicitud de Hello es todo, en cuyo caso es una línea de resumen, o identifica Hola API específica como QueryEntity o UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="e0b65-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="e0b65-218">datos de ejemplo de Hola anterior muestra que Hola a todos los registra para un solo minuto (empezando a las 11:00 A.M.), por lo que Hola número de solicitudes de QueryEntities más hello número de solicitudes de QueryEntity junto con hello número de solicitudes de UpdateEntity suma tooseven, que es Hola total se muestra en fila de Hello user: All.</span><span class="sxs-lookup"><span data-stu-id="e0b65-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="e0b65-219">De forma similar, puede derivar Hola promedio-to-end de latencia 104,4286 en fila de user: All Hola calculando ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="e0b65-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="e0b65-220">Alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="e0b65-220">Metrics alerts</span></span>
<span data-ttu-id="e0b65-221">Puede configurar alertas en hello [portal de Azure](https://portal.azure.com) para las métricas de almacenamiento puedan notificarle automáticamente de los cambios importantes en el comportamiento de Hola de los servicios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0b65-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="e0b65-222">Si usas un toodownload de herramienta del explorador de almacenamiento estos datos de métricas en un formato delimitado, puede usar datos de Microsoft Excel tooanalyze Hola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="e0b65-223">Consulte [Herramientas de cliente de Azure Storage](storage-explorers.md) para ver una lista de las herramientas del explorador de almacenamiento disponible.</span><span class="sxs-lookup"><span data-stu-id="e0b65-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="e0b65-224">Puede configurar alertas de hello **reglas de alerta** hoja, accesible mediante **supervisión** en la hoja de menú de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0b65-225">Puede haber un retraso entre un evento de almacenamiento y cuándo se registra la Hola correspondiente datos de métricas por hora o minuto.</span><span class="sxs-lookup"><span data-stu-id="e0b65-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="e0b65-226">En caso de hello de métricas por minuto, varios minutos de datos se puede escribir al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="e0b65-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="e0b65-227">Esto puede provocar tootransactions de minutos anteriores se agregan en la transacción de Hola para hello minuto actual.</span><span class="sxs-lookup"><span data-stu-id="e0b65-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="e0b65-228">Cuando esto sucede, alerta de hello servicio no puede tener todos los datos de métricas disponibles para hello configurado intervalo de alerta, lo que puede provocar tooalerts desencadenar de forma inesperada.</span><span class="sxs-lookup"><span data-stu-id="e0b65-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="e0b65-229">Acceso a los datos de métricas mediante programación</span><span class="sxs-lookup"><span data-stu-id="e0b65-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="e0b65-230">Hello listado siguiente muestra código C# muestra que tiene acceso a las métricas de minuto de Hola para un intervalo de minutos y muestra los resultados de hello en una ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="e0b65-231">Usa hello Azure Storage Library versión 4 que incluye Hola clase CloudAnalyticsClient que simplifica el acceso a tablas de métricas de hello en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0b65-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="e0b65-232">¿Qué se le facturará cuando habilite las métricas de almacenamiento?</span><span class="sxs-lookup"><span data-stu-id="e0b65-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="e0b65-233">Escribir solicitudes toocreate entidades de tabla para las métricas se cobran con operaciones de almacenamiento de Azure de hello las tarifas estándar tooall aplicables.</span><span class="sxs-lookup"><span data-stu-id="e0b65-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="e0b65-234">Las solicitudes de lectura y eliminación por una toometrics de datos de cliente son facturables con las tarifas estándares.</span><span class="sxs-lookup"><span data-stu-id="e0b65-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="e0b65-235">Si ha configurado una directiva de retención de datos, no se le cobrará cuando Almacenamiento de Azure elimine datos de métricas antiguos.</span><span class="sxs-lookup"><span data-stu-id="e0b65-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="e0b65-236">Sin embargo, si elimina datos de análisis, la cuenta se cobra por las operaciones de eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0b65-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="e0b65-237">capacidad de Hello usado por las tablas de métricas de hello también es facturable: puede usar Hola después de la cantidad de hello tooestimate de capacidad se utiliza para almacenar datos de métricas:</span><span class="sxs-lookup"><span data-stu-id="e0b65-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="e0b65-238">Si cada hora un servicio utiliza todas las API en todos los servicios, aproximadamente 148KB de datos se almacena cada hora en tablas de transacciones de métricas de hello si ha habilitado el servicio y el resumen de nivel de API.</span><span class="sxs-lookup"><span data-stu-id="e0b65-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="e0b65-239">Si cada hora un servicio utiliza todas las API en todos los servicios, aproximadamente 12KB de datos se almacena cada hora en tablas de transacciones de métricas de hello si ha habilitado el nivel de servicio simplemente resumen.</span><span class="sxs-lookup"><span data-stu-id="e0b65-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="e0b65-240">tabla de capacidad para los blobs Hello tiene dos filas agregadas al día (proporcionado por el usuario haya optado por los registros): Esto implica que cada día Hola tamaño de esta tabla aumenta en una tooapproximately 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="e0b65-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0b65-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0b65-241">Next steps</span></span>
[<span data-ttu-id="e0b65-242">Habilitar el registro de almacenamiento y acceso a los datos del registro</span><span class="sxs-lookup"><span data-stu-id="e0b65-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
