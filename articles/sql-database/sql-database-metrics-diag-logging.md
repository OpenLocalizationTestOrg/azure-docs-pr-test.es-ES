---
title: "las métricas y registro de diagnósticos de base de datos SQL aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo configurar el uso de recursos de toostore de recursos de base de datos de SQL Azure, conectividad y las estadísticas de ejecución de consulta."
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
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Métricas y registros de diagnóstico de Azure SQL Database 
Azure SQL Database puede emitir métricas y registros de diagnóstico para facilitar la supervisión. Puede configurar el uso de recursos de base de datos de SQL Azure toostore, los trabajadores y sesiones y conectividad en uno de estos recursos de Azure:
- **Azure Storage**: para archivar grandes cantidades de telemetría a un pequeño precio
- **Centro de eventos de Azure**: para integrar la telemetría de Azure SQL Database con la solución de supervisión personalizada o las canalizaciones activas
- **Análisis de registros de Azure**: para fuera del cuadro de hello solución con informes, alertas y mitigar las capacidades de supervisión 

    ![arquitectura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a>Habilitación del registro

Las métricas y los registros de diagnóstico no están habilitados de forma predeterminada. Puede habilitar y administrar las métricas y registro de diagnóstico mediante uno de los siguientes métodos de hello:
- Azure Portal
- PowerShell
- Azure CLI
- API de REST 
- Plantilla de Resource Manager

Al habilitar las métricas y registro de diagnósticos, deberá toospecify Hola recursos de Azure donde se recopilan los datos seleccionados. Opciones disponibles:
- Log Analytics
- Centro de eventos
- Almacenamiento de Azure 

Puede aprovisionar un nuevo recurso de Azure o seleccionar uno existente. Después de seleccionar el recurso de almacenamiento de hello, deberá toospecify qué toocollect de datos. Las opciones disponibles incluyen:

- **[Métricas de 1 minuto](sql-database-metrics-diag-logging.md#1-minute-metrics)**: contiene porcentaje de DTU; límite de DTU; porcentaje de CPU; porcentaje de lectura de datos físicos; porcentaje de escritura en registro; conexiones correctas, erróneas o bloqueadas por el firewall; porcentaje de sesiones; porcentaje de trabajadores; almacenamiento; porcentaje de almacenamiento y porcentaje de almacenamiento de XTP.

Si especifica una cuenta de AzureStorage o concentrador de eventos, puede especificar un toospecify de directiva de retención que los datos que es más antiguos de período de tiempo seleccionada se elimina. Si especifica el análisis de registros, directiva de retención de hello depende de tarifa seleccionado Hola. Más información sobre [Log Analytics Precios](https://azure.microsoft.com/pricing/details/log-analytics/). 

Le recomendamos que lea ambos hello [información general sobre las métricas en Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) y [información general de Azure registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículos toogain entender no solo cómo tooenable el registro, pero Hola categorías de registro y métricas admiten Hola varios servicios de Azure.

### <a name="azure-portal"></a>Azure Portal

las métricas de tooenable colección de registros de diagnóstico en hello portal de Azure, navegue tooyour base de datos de SQL Azure o la página de grupo elástico y, a continuación, haga clic en **configuración de diagnóstico**.

   ![Habilitar Hola portal de Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a>PowerShell

tooenable métricas y registro de diagnósticos con PowerShell, usan Hola siguientes comandos:

- tooenable almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   Hola Id. de cuenta de almacenamiento es el identificador de recurso de Hola para los registros de hello almacenamiento cuenta toowhich desea toosend Hola de.

- tooenable transmisión por secuencias de registros de diagnóstico tooan concentrador de eventos, use este comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   Hola Id. de regla de Bus de servicio es una cadena con este formato:

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- enviar tooenable del área de trabajo de análisis de registros de tooa registros de diagnóstico, use este comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- Puede obtener el identificador de recurso de Hola de su área de trabajo de análisis de registros mediante Hola siguiente comando:

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

Puede combinar estos parámetros tooenable varias opciones de salida.

### <a name="cli"></a>CLI

tooenable métricas y registro de diagnóstico con Hola CLI de Azure, Hola de uso siguientes comandos:

- tooenable almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   Hola Id. de cuenta de almacenamiento es el identificador de recurso de Hola para los registros de hello almacenamiento cuenta toowhich desea toosend Hola de.

- tooenable transmisión por secuencias de registros de diagnóstico tooan concentrador de eventos, use este comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   Hola Id. de regla de Bus de servicio es una cadena con este formato:

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- enviar tooenable del área de trabajo de análisis de registros de tooa registros de diagnóstico, use este comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

Puede combinar estos parámetros tooenable varias opciones de salida.

### <a name="rest-api"></a>API de REST

Leer acerca de cómo demasiado[cambiar la configuración de diagnóstico mediante API de REST de Azure Monitor hello](https://msdn.microsoft.com/library/azure/dn931931.aspx). 

### <a name="resource-manager-template"></a>Plantilla de Resource Manager

Leer acerca de cómo demasiado[habilitar la configuración de diagnóstico en la creación de recursos mediante el Administrador de recursos plantilla](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md). 

## <a name="stream-into-log-analytics"></a>Transmisión a Log Analytics 
Métricas de base de datos de SQL Azure y registros de diagnóstico se pueden transmitir en análisis de registros mediante la opción de "Enviar tooLog análisis" integradas de hello en el portal de Hola o al habilitar el análisis de registros en una configuración de diagnóstico a través de los cmdlets de PowerShell de Azure, CLI de Azure o Azure Monitor REST API.

### <a name="installation-overview"></a>Introducción a la instalación

La supervisión de la línea de Azure SQL Database es sencilla con Log Analytics. Se necesitan tres pasos:

1.  Crear el recurso Log Analytics
2.  Configurar las métricas de toorecord de las bases de datos y registros de diagnóstico en hello creado análisis de registros
3.  Instalar la solución **Azure SQL Analytics** desde la galería en Log Analytics

### <a name="create-log-analytics-resource"></a>Crear el recurso Log Analytics

1. Haga clic en **New** en el menú izquierdo Hola.
2. Haga clic en **Supervisión y administración**.
3. Haga clic en **Log Analytics**.
4. Rellenar en forma de análisis de registros de hello con información adicional de hello necesaria: nombre de área de trabajo, suscripción, grupo de recursos, la ubicación y nivel de precios.

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a>Configurar las métricas de toorecord de las bases de datos y registros de diagnóstico

tooconfigure Hola de manera más fácil en las bases de datos registran sus métricas es a través de hello portal de Azure. En Hola portal de Azure, vaya tooyour recursos de base de datos de SQL Azure y haga clic en **configuración de diagnóstico**. 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a>Instalar soluciones de análisis de SQL Azure Hola desde la Galería  

1. Una vez que se crea Hola recursos de análisis de registros y los datos se envíen en él, instale la solución de análisis de SQL Azure. Esto puede realizarse a través de hello **Galería de soluciones** que se puede encontrar en la página principal OMS de Hola y en los menús de lado de Hola. En la Galería de hello, busque y haga clic en **el análisis de SQL Azure** solución y haga clic en **agregar**.

   ![solución de supervisión](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. En la página principal de OMS aparece un nuevo icono llamado **Azure SQL Analytics**. Al seleccionar este icono abre el panel de análisis de SQL de Azure de Hola.

### <a name="using-azure-sql-analytics-solution"></a>Uso de la solución Azure SQL Analytics

Análisis de SQL Azure es un panel jerárquico que permite toonavigate a través de la jerarquía de Hola de recursos de base de datos de SQL Azure. Esto permite que capacidad toodo alto nivel de supervisión pero también le permite tooscope su supervisión Hola de toojust derecho conjunto de recursos.
Panel contiene listas de Hola de varios recursos en recursos de hello seleccionado. Por ejemplo, para una suscripción seleccionada puede ver Hola todos los servidores, grupos elásticos y las bases de datos que pertenecen toohello seleccionan la suscripción. Además, para los grupos elásticos y bases de datos, puede ver métricas de uso de recursos de Hola de ese recurso. Esto incluye gráficos de DTU, CPU, E/S, registro, sesiones, trabajadores, conexiones y almacenamiento en GB.

## <a name="stream-into-azure-event-hub"></a>Transmisión al Centro de eventos de Azure

Métricas de base de datos de SQL Azure y registros de diagnóstico se pueden transmitir en Centro de eventos mediante la opción de integrados "flujo tooan concentrador de eventos" hello en el portal de Hola o habilitando el Id. de regla de Bus de servicio en una configuración de diagnóstico mediante Cmdlets de PowerShell de Azure, CLI de Azure o Azure Monitor REST API. 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a>¿Qué toodo con métricas y registros de diagnóstico de concentrador de eventos?
Una vez que se transmite por secuencias datos Hola seleccionado en el concentrador de eventos, están un paso tooenabling más cerca de escenarios de supervisión avanzados. Los concentradores de eventos actúa como Hola "puerta principal" para una canalización de eventos, y una vez que se recopilan los datos en un centro de eventos, se pueden transformar y almacenado con cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento y procesamiento por lotes. Los concentradores de eventos desacopla producción de hello de una secuencia de eventos de consumo de Hola de esos eventos, para que los consumidores de eventos pueden tener acceso a los eventos de hello en su propia programación. Para más información sobre el Centro de eventos, vea:

- [¿Qué es Azure Event Hubs?](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Introducción a Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


Aquí se muestran unos pocos maneras puede usar Hola capacidad de streaming:

-   Ver el estado del servicio mediante el streaming de datos "ruta de acceso activa" tooPowerBI - utilizando y centros de eventos, análisis de transmisiones, Power BI, puede transformar fácilmente los datos de métricas y diagnósticos en cerca de la información en tiempo real en los servicios de Azure. Para obtener información general de cómo procesar datos con análisis de transmisiones tooset seguridad un centros de eventos y usar Power BI como salida, consulte [análisis de transmisiones y Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).
-   Secuencia registros toothird terceros registro y telemetría secuencias: centros de eventos mediante transmisión por secuencias pueden obtener la métrica y registros de diagnóstico en toodifferent soluciones de análisis de registro y supervisión de aplicaciones de terceros. 
-   Compilar una telemetría personalizada y una plataforma de registro: si ya dispone de una plataforma de telemetría personalizadas o son solo pensar en uno, Hola altamente escalable publicación / suscripción de edificio naturaleza de los centros de eventos permite tooflexibly recopilar registros de diagnóstico. Vea [toousing de guía de Dan Rosanova centros de eventos en una plataforma de telemetría de escala global](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="stream-into-azure-storage"></a>Transmisión a Azure Storage

Métricas de base de datos de SQL Azure y registros de diagnóstico que pueden almacenarse en el almacenamiento de Azure con la opción "Archivar la cuenta de almacenamiento tooa" incorporada de Hola Hola portal de Azure, o al habilitar el almacenamiento de Azure en una configuración de diagnóstico mediante Cmdlets de PowerShell de Azure, CLI de Azure o Azure API de REST de monitor.

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a>Esquema de las métricas y los registros de diagnóstico de la cuenta de almacenamiento de Hola

Una vez haya configurado las métricas y la colección de registros de diagnóstico, se crea un contenedor de almacenamiento de cuenta de almacenamiento de hello seleccionado cuando están disponibles las primeras filas de Hola de datos. estructura de Hola de estos blobs es:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
O, sencillamente:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

Por ejemplo, un nombre de blob para métricas de 1 minuto podría ser:

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

En caso de que desee toorecord datos Hola Hola grupo elástico, nombre de blob es un poco diferente:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a>Descargar métricas y registros de Azure Storage

Vea [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) (Descargar métricas y registros de diagnóstico de Azure Storage).

## <a name="1-minute-metrics"></a>métricas de 1 minuto

| |  |
|---|---|
|**Recurso**|**Métricas**|
|Base de datos|Porcentaje de DTU; DTU usada; límite de DTU; porcentaje de CPU; porcentaje de lectura de datos físicos; porcentaje de escritura en registro; conexiones correctas, erróneas o bloqueadas por el firewall; porcentaje de sesiones; porcentaje de trabajadores; almacenamiento; porcentaje de almacenamiento; porcentaje de almacenamiento de XTP e interbloqueos |
|Grupo elástico|porcentaje de eDTU; eDTUusada; límite de eDTU; porcentaje de CPU; porcentaje de lectura de datos físicos; porcentaje de escritura en registro; porcentaje de sesiones; porcentaje de trabajadores; almacenamiento; porcentaje de almacenamiento; límite de almacenamiento y porcentaje de almacenamiento de XTP |
|||

## <a name="next-steps"></a>Pasos siguientes

- Leer ambos hello [información general sobre las métricas en Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) y [información general de Azure registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain la descripción de no sólo la forma tooenable registro, pero las métricas de Hola y categorías de registro de los artículos admite Hola varios servicios de Azure.
- Lea estas toolearn artículos acerca de los centros de eventos:
   - [¿Qué es Azure Event Hubs?](../event-hubs/event-hubs-what-is-event-hubs.md)
   - [Introducción a Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- Vea [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) (Descargar métricas y registros de diagnóstico de Azure Storage).
