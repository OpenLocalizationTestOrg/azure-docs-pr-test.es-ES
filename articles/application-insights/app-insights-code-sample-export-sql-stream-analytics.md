---
title: "Exportar tooSQL de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Exportar continuamente tooSQL de datos de Application Insights mediante el análisis de transmisiones."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>Tutorial: Exportar tooSQL de Application Insights mediante el análisis de transmisiones
Este artículo se muestra cómo toomove los datos de telemetría de [Azure Application Insights] [ start] en una base de datos de SQL Azure mediante el uso de [exportar continua] [ export] y [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/). 

La Exportación continua traslada los datos de telemetría a Almacenamiento de Azure en formato JSON. Comenzaremos analizar objetos JSON de hello mediante el análisis de transmisiones de Azure y crear filas en una tabla de base de datos.

(Por lo general, exportar continua es Hola forma toodo su propio análisis de telemetría de hello las aplicaciones enviar tooApplication visión. Se pueden adaptar este toodo de ejemplo de código otras cosas con la telemetría Hola exportado, como la agregación de datos.)

Comenzaremos con la suposición de Hola que ya tiene la aplicación hello desea toomonitor.

En este ejemplo, vamos a usar datos de vista de página de hello, pero hello mismo patrón se puede ampliar fácilmente los tipos de datos de tooother como eventos personalizados y las excepciones. 

## <a name="add-application-insights-tooyour-application"></a>Agregar Application Insights tooyour aplicación
tooget iniciado:

1. [Configure Application Insights para sus páginas web](app-insights-javascript.md). 
   
    (En este ejemplo, nos centraremos en el procesamiento de datos de la vista de página de los exploradores de cliente hello, pero también puede configurar Application Insights para el lado del servidor hello de su [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md) solicitud de aplicación y el proceso dependencia y otro servidor de telemetría.)
2. Publique la aplicación y vea los datos de telemetría que aparecen en el recurso de Application Insights.

## <a name="create-storage-in-azure"></a>Creación de almacenamiento en Azure
Exportación continua siempre genera cuenta de almacenamiento de Azure de tooan de datos, por lo que necesita almacenamiento de hello toocreate en primer lugar.

1. Crear una cuenta de almacenamiento en su suscripción en hello [portal de Azure][portal].
   
    ![En el portal de Azure, elija Nuevo, Datos, Almacenamiento. Seleccione Clásico y elija Crear. Proporcione un nombre de almacenamiento.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Crear un contenedor
   
    ![En un almacenamiento nuevo hello, seleccionar contenedores, haga clic en el icono de contenedores de hello y, a continuación, agregar](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Copie la clave de acceso de almacenamiento de Hola
   
    Necesitará pronto tooset seguridad de servicio de análisis de secuencia de entrada toohello Hola.
   
    ![En el almacenamiento de hello, abra la configuración, claves y realizar una copia de la clave de acceso principal de Hola](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Iniciar exportación continua tooAzure almacenamiento
1. Hola portal de Azure, examinar recursos de Application Insights toohello que creó para la aplicación.
   
    ![Elija Examinar, Application Insights, su aplicación.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Cree una exportación continua.
   
    ![Elija Configuración, Exportación continua, Agregar.](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Seleccione la cuenta de almacenamiento de Hola que creó anteriormente:

    ![Establecer el destino de la exportación de Hola](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    Establecer a tipos de evento de hello que desea toosee:

    ![Elija los tipos de evento.](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Permita que se acumulen algunos datos. Póngase cómo y deje que los usuarios usen su aplicación durante un tiempo. Así, aparecerá la telemetría y verá gráficos estadísticos en el [explorador de métricas](app-insights-metrics-explorer.md) y eventos individuales en la [búsqueda de diagnóstico](app-insights-diagnostic-search.md). 
   
    Y además, los datos de hello exportará tooyour almacenamiento. 
2. Inspeccionar los datos de hello exportado, ya sea en el portal de hello - elegir **examinar**, seleccione la cuenta de almacenamiento y, a continuación, **contenedores** - o en Visual Studio. En Visual Studio, elija **Ver/Cloud Explorer** y abra Azure/Almacenamiento. (Si no tiene esta opción de menú, necesita tooinstall hello Azure SDK: abra el cuadro de diálogo de proyecto nuevo de Hola y abra Visual C# / nube / obtener Microsoft Azure SDK para. NET.)
   
    ![En Visual Studio, abra Explorador de servidores, Azure, Almacenamiento.](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Tome nota de la parte común de Hola de nombre de ruta de acceso de hello, que se deriva de la clave de nombre e instrumentación de la aplicación hello. 

eventos de Hola se escriben tooblob archivos en formato JSON. Cada archivo puede contener uno o varios eventos. Por lo que nos gustaría datos de eventos de tooread hello y filtrar campos Hola que queremos. Hay todo tipo de cosas, que podríamos hacer con los datos de hello, pero nuestro plan hoy en día es toouse análisis de transmisiones toomove Hola datos tooa base de datos SQL. Que le resultará fácil toorun una gran cantidad de consultas interesantes.

## <a name="create-an-azure-sql-database"></a>Creación de una Base de datos SQL de Azure
Una vez más a partir de su suscripción en [portal de Azure][portal], crear base de datos de hello (y un servidor nuevo, a menos que ya tiene uno) toowhich escribirá los datos de Hola.

![Nuevo, Datos, SQL.](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Asegúrese de que ese servidor de base de datos de hello permite acceso a los servicios de tooAzure:

![Examinar, los servidores, el servidor, configuración, Firewall, permitir el acceso a tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Creación de una tabla en la base de datos SQL de Azure
Conectar la base de datos de toohello creada en la sección anterior de hello con la herramienta de administración preferido. En este tutorial, usaremos [Herramientas de administración de SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Cree una nueva consulta y ejecute hello después de T-SQL:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

En este ejemplo, usamos datos de vistas de página. toosee Hola otros datos disponibles, inspeccionar la salida JSON y vea hello [Exportar modelo de datos](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Creación de una instancia de Análisis de transmisiones de Azure
De hello [Portal de Azure clásico](https://manage.windowsazure.com/), seleccione servicio de análisis de transmisiones de Azure de Hola y crear un nuevo trabajo de análisis de transmisiones:

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Cuando se crea el nuevo trabajo de hello, expandir los detalles:

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Establecimiento de la ubicación del blob
Establézcalo tootake entrada desde el blob exportar continua:

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

Ahora deberá Hola clave de acceso principal de la cuenta de almacenamiento, que se ha indicado anteriormente. Utilizar esta configuración como Hola clave de la cuenta de almacenamiento.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Establecimiento del patrón del prefijo de la ruta de acceso
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

Sea seguro tooset Hola formato de fecha demasiado**aaaa-MM-DD** (con **guiones**).

Hola modelo de prefijo de ruta de acceso especifica cómo el análisis de transmisiones encuentra archivos de entrada de hello en el almacenamiento de Hola. Necesita tooset se toohow toocorrespond exportar continua almacena los datos de Hola. Configúrelo como este caso que se muestra a continuación:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

En este ejemplo:

* `webapplication27`es Hola nombre de recurso de Application Insights, hello **todo en minúsculas**. 
* `1234...`es la clave de instrumentación Hola de hello recursos de Application Insights **con guiones quitados**. 
* `PageViews`es el tipo de saludo de datos que deseamos tooanalyze. los tipos disponibles de Hello dependen de filtro de Hola que se establezca en Exportar continua. Examinar Hola Hola de toosee de los datos exportados en otros tipos disponibles y ver hello [Exportar modelo de datos](app-insights-export-data-model.md).
* `/{date}/{time}` es un patrón escrito literalmente.

nombre de hello tooget y iKey de su recurso de Application Insights, abra Essentials en su página de información general, o abra la configuración.

#### <a name="finish-initial-setup"></a>Finalización de la instalación inicial
Confirme el formato de serialización de hello:

![Confirme y cierre el asistente.](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Cerrar el Asistente de Hola y espere Hola el programa de instalación toocomplete.

> [!TIP]
> Utilice toocheck de función de ejemplo Hola que ha establecido correctamente ruta de acceso de entrada de Hola. Si se produce un error: Compruebe que hay datos en el almacenamiento de hello para el intervalo de tiempo de ejemplo de Hola que eligió. Editar definición de entrada de Hola y compruebe que establece la cuenta de almacenamiento de hello, el prefijo de ruta de acceso y correctamente el formato de fecha.
> 
> 

## <a name="set-query"></a>Establecimiento de la consulta
Abra la sección de la consulta de hello:

![En Análisis de transmisiones, seleccione Consulta.](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Reemplace la consulta predeterminada de hello con:

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

Tenga en cuenta que primero Hola algunas propiedades son datos de la vista de toopage específico. Las exportaciones de otros tipos de telemetría tendrán diferentes propiedades. Vea hello [detallada de la referencia del modelo de datos para los valores y tipos de propiedad Hola.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Configurar la salida toodatabase
Seleccionar SQL como salida de hello.

![En Análisis de transmisiones, seleccione Salidas.](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Especifique la base de datos SQL de Hola.

![Rellene los detalles de saludo de la base de datos](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Cierre el Asistente de Hola y espere a que una notificación que se configuró la salida de hello.

## <a name="start-processing"></a>Inicio del procesamiento
Iniciar el trabajo de Hola desde la barra de acciones de hello:

![En Stream Analytics, haga clic en Inicio.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

Puede elegir si el procesamiento de toostart Hola datos a partir de ahora o toostart con los datos anteriores. Hola este último resulta útil si han tenido exportar continua ya ejecutando durante algún tiempo.

![En Stream Analytics, haga clic en Inicio.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Después de unos minutos, vuelva atrás tooSQL herramientas de administración de servidor y ver Hola datos que fluyen en. Por ejemplo, utilice una consulta como esta:

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>Artículos relacionados
* [Exportar tooPowerBI mediante el análisis de transmisiones](app-insights-export-power-bi.md)
* [Referencia para tipos de propiedad de Hola y valores del modelo de datos detallados.](app-insights-export-data-model.md)
* [Exportación continua en Application Insights](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

