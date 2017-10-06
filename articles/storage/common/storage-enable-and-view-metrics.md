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
ms.openlocfilehash: f157dbdf9a256da7ab186f80db746b91d1a9beb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a>Habilitar las métricas de almacenamiento de Azure y ver sus datos
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Información general
Las métricas de almacenamiento se habilitan de forma predeterminada al crear una nueva cuenta de almacenamiento. Puede configurar la supervisión a través de hello [portal de Azure](https://portal.azure.com) o Windows PowerShell, o mediante programación a través de una de las bibliotecas de cliente de almacenamiento de Hola.

Puede configurar un período de retención de datos de métricas de hello: este período determina cuánto almacenamiento Hola servicio mantiene las métricas de Hola y cargos de hello espacio necesario toostore ellos. Por lo general, debe usar un período de retención más corto para métricas por minuto de métricas por hora debido a Hola considerable espacio adicional requerido para las métricas de minuto. Debe elegir un período de retención de forma que tiene suficiente tiempo tooanalyze Hola datos y descargar todas las métricas que se va tookeep para análisis sin conexión o de elaboración de informes. Recuerde que también se le facturará por la descarga de los datos de métricas desde su cuenta de almacenamiento.

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a>Cómo las métricas de tooenable con Hola portal de Azure
Siga estas métricas de tooenable pasos Hola [portal de Azure](https://portal.azure.com):

1. Navegue tooyour cuenta de almacenamiento.
1. Seleccione **diagnósticos** en hello **menú** hoja
1. Asegúrese de que **estado** se establece demasiado**en**.
1. Las métricas de hello SELECT para los servicios de hello desea toomonitor.
1. Especificar un tooindicate de directiva de retención cuánto datos de métricas y registro de tooretain.
1. Seleccione **Guardar**.

Tenga en cuenta que hello [portal de Azure](https://portal.azure.com) no permite actualmente tooconfigure métricas por minuto en su cuenta de almacenamiento; debe habilitar las métricas de minuto con PowerShell o mediante programación.

## <a name="how-tooenable-metrics-using-powershell"></a>Cómo las métricas de tooenable con PowerShell
Puede usar PowerShell en su tooconfigure de máquina local las métricas de almacenamiento en su cuenta de almacenamiento mediante la configuración actual de hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve Hola y Hola cmdlet Configuración actual de Set-AzureStorageServiceMetricsProperty toochange Hola.

cmdlets de Hola que controlan las métricas de almacenamiento usan Hola parámetros siguientes:

* Los valores posibles de MetricsType son Hour y Minute.
* Los valores posibles de ServiceType son Blob, Queue y Table.
* Los valores posibles de MetricsLevel son None, Service y ServiceAndApi.

Por ejemplo, hello comando siguiente activa el minuto las métricas para servicio de Blob de hello en su cuenta de almacenamiento predeterminada con el período de retención de hello definir los días de toofive:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

Hello comando siguiente recupera Hola actual por hora métricas nivel y retención de los días para servicio de blob de hello en su cuenta de almacenamiento predeterminada:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

Para obtener información acerca de cómo tooconfigure hello Azure PowerShell cmdlets toowork con su suscripción de Azure y cómo tooselect Hola almacenamiento predeterminado cuenta toouse, consulte: [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>¿Cómo tooenable las métricas de almacenamiento mediante programación
Hola siguiente fragmento de código C# muestra cómo tooenable métricas y registro para el uso de servicio de Blob de Hola Hola biblioteca cliente de almacenamiento para. NET:

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

## <a name="viewing-storage-metrics"></a>Mostrar Métricas de almacenamiento
Después de configurar la cuenta de almacenamiento toomonitor de métricas de análisis de almacenamiento, el análisis de almacenamiento registra las métricas de hello en un conjunto de tablas conocidas en su cuenta de almacenamiento. Puede configurar métricas por hora de gráficos tooview Hola [portal de Azure](https://portal.azure.com):

1. Navegar por la cuenta de almacenamiento de tooyour en hello [portal de Azure](https://portal.azure.com).
1. Seleccione **métricas** en hello **menú** hoja para hello servicio cuyas métricas que desee tooview.
1. Seleccione **editar** en gráfico de hello desea tooconfigure.
1. Hola **Editar gráfico** hoja, seleccione hello **intervalo de tiempo**, **tipo de gráfico**y las métricas de Hola que desea mostrar en gráfico de Hola.
1. Seleccione **Aceptar**.

Si desea que las métricas de hello toodownload para almacenamiento a largo plazo o tooanalyze ellos localmente, debe:

* Utilizar una herramienta que es compatible con estas tablas y se permiten tooview y descargarlos.
* Escribir una tooread de aplicación o el script personalizado y almacenar las tablas de Hola.

Muchas herramientas de exploración de almacenamiento de terceros son conscientes de estas tablas y habilitar tooview ellos directamente.
Consulte [Herramientas de cliente de Azure Storage](storage-explorers.md) para obtener una lista de herramientas disponibles.

> [!NOTE]
> A partir de la versión 0.8.0 de hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), puede ver y descargar las tablas de métricas de análisis de Hola.
> 
> 

En el análisis de orden tooaccess Hola tablas mediante programación, tenga en cuenta que las tablas de análisis de hello no aparecen si lista todas las tablas de hello en su cuenta de almacenamiento. Puede tener acceso a ellos directamente por su nombre, o usar hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) Hola .NET cliente biblioteca tooquery hello en nombres de tabla.

### <a name="hourly-metrics"></a>Métricas por hora
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Métricas por minuto
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Capacity
* $MetricsCapacityBlob

Puede encontrar detalles completos de los esquemas de Hola para estas tablas en [esquema de tabla de métricas de análisis de almacenamiento](https://msdn.microsoft.com/library/azure/hh343264.aspx). filas de ejemplo de Hola a continuación muestran solo un subconjunto de columnas de hello disponibles, pero ilustran algunas características importantes de manera hello que las métricas de almacenamiento guardan estas métricas:

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Disponibilidad | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |user;All |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |user;QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |user;QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |user;UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

En estos datos de métricas por minuto de ejemplo, clave de partición de hello usa tiempo de hello en la resolución de minutos. clave de fila de Hello identifica el tipo de Hola de información que se almacena en la fila de Hola y se compone de dos partes de información, el tipo de acceso de Hola y el tipo de solicitud de hello:

* tipo de acceso de Hello es el usuario o del sistema, donde usuario refiere a servicio de almacenamiento de toohello de las solicitudes de usuario de tooall y sistema toorequests realizadas por el análisis de almacenamiento.
* tipo de solicitud de Hello es todo, en cuyo caso es una línea de resumen, o identifica Hola API específica como QueryEntity o UpdateEntity.

datos de ejemplo de Hola anterior muestra que Hola a todos los registra para un solo minuto (empezando a las 11:00 A.M.), por lo que Hola número de solicitudes de QueryEntities más hello número de solicitudes de QueryEntity junto con hello número de solicitudes de UpdateEntity suma tooseven, que es Hola total se muestra en fila de Hello user: All. De forma similar, puede derivar Hola promedio-to-end de latencia 104,4286 en fila de user: All Hola calculando ((143.8 * 5) + 3 + 9) / 7.

## <a name="metrics-alerts"></a>Alertas de métricas
Puede configurar alertas en hello [portal de Azure](https://portal.azure.com) para las métricas de almacenamiento puedan notificarle automáticamente de los cambios importantes en el comportamiento de Hola de los servicios de almacenamiento. Si usas un toodownload de herramienta del explorador de almacenamiento estos datos de métricas en un formato delimitado, puede usar datos de Microsoft Excel tooanalyze Hola. Consulte [Herramientas de cliente de Azure Storage](storage-explorers.md) para ver una lista de las herramientas del explorador de almacenamiento disponible. Puede configurar alertas de hello **reglas de alerta** hoja, accesible mediante **supervisión** en la hoja de menú de cuenta de almacenamiento de Hola.

> [!IMPORTANT]
> Puede haber un retraso entre un evento de almacenamiento y cuándo se registra la Hola correspondiente datos de métricas por hora o minuto. En caso de hello de métricas por minuto, varios minutos de datos se puede escribir al mismo tiempo. Esto puede provocar tootransactions de minutos anteriores se agregan en la transacción de Hola para hello minuto actual. Cuando esto sucede, alerta de hello servicio no puede tener todos los datos de métricas disponibles para hello configurado intervalo de alerta, lo que puede provocar tooalerts desencadenar de forma inesperada.
>

## <a name="accessing-metrics-data-programmatically"></a>Acceso a los datos de métricas mediante programación
Hello listado siguiente muestra código C# muestra que tiene acceso a las métricas de minuto de Hola para un intervalo de minutos y muestra los resultados de hello en una ventana de consola. Usa hello Azure Storage Library versión 4 que incluye Hola clase CloudAnalyticsClient que simplifica el acceso a tablas de métricas de hello en el almacenamiento.

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>¿Qué se le facturará cuando habilite las métricas de almacenamiento?
Escribir solicitudes toocreate entidades de tabla para las métricas se cobran con operaciones de almacenamiento de Azure de hello las tarifas estándar tooall aplicables.

Las solicitudes de lectura y eliminación por una toometrics de datos de cliente son facturables con las tarifas estándares. Si ha configurado una directiva de retención de datos, no se le cobrará cuando Almacenamiento de Azure elimine datos de métricas antiguos. Sin embargo, si elimina datos de análisis, la cuenta se cobra por las operaciones de eliminación de Hola.

capacidad de Hello usado por las tablas de métricas de hello también es facturable: puede usar Hola después de la cantidad de hello tooestimate de capacidad se utiliza para almacenar datos de métricas:

* Si cada hora un servicio utiliza todas las API en todos los servicios, aproximadamente 148KB de datos se almacena cada hora en tablas de transacciones de métricas de hello si ha habilitado el servicio y el resumen de nivel de API.
* Si cada hora un servicio utiliza todas las API en todos los servicios, aproximadamente 12KB de datos se almacena cada hora en tablas de transacciones de métricas de hello si ha habilitado el nivel de servicio simplemente resumen.
* tabla de capacidad para los blobs Hello tiene dos filas agregadas al día (proporcionado por el usuario haya optado por los registros): Esto implica que cada día Hola tamaño de esta tabla aumenta en una tooapproximately 300 bytes.

## <a name="next-steps"></a>Pasos siguientes
[Habilitar el registro de almacenamiento y acceso a los datos del registro](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
