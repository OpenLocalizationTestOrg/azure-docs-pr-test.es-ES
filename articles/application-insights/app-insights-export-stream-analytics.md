---
title: "aaaExport mediante el análisis de transmisiones de Azure Application Insights | Documentos de Microsoft"
description: "Análisis de transmisiones de forma continua puede transformar, filtrar y enrutar datos hello que exporta de Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Usar análisis de transmisiones tooprocess datos exportados de Application Insights
[Análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) es Hola herramienta ideal para procesar datos [exportada desde Application Insights](app-insights-export-telemetry.md). Stream Analytics puede extraer datos de una variedad de orígenes. Puede transformar y filtrar los datos de hello y, a continuación, distribuirlo tooa diversos receptores.

En este ejemplo, vamos a crear un adaptador que toma datos de Application Insights, cambia el nombre y procesa algunos de los campos de Hola y lo canaliza en Power BI.

> [!WARNING]
> Hay mucho mejor y más sencillo [formas recomendadas toodisplay datos de Application Insights en Power BI](app-insights-export-power-bi.md). ruta de acceso se ilustra a continuación Hello es simplemente una tooillustrate de ejemplo cómo tooprocess exportan datos.
> 
> 

![Diagrama de bloques para la exportación a través de SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Creación de almacenamiento en Azure
Exportación continua siempre genera cuenta de almacenamiento de Azure de tooan de datos, por lo que necesita almacenamiento de hello toocreate en primer lugar.

1. Crear una cuenta de almacenamiento "clásico" en su suscripción en hello [portal de Azure](https://portal.azure.com).
   
   ![En el portal de Azure, elija Nuevo, Datos, Almacenamiento.](./media/app-insights-export-stream-analytics/030.png)
2. Crear un contenedor
   
    ![En un almacenamiento nuevo hello, seleccionar contenedores, haga clic en el icono de contenedores de hello y, a continuación, agregar](./media/app-insights-export-stream-analytics/040.png)
3. Copie la clave de acceso de almacenamiento de Hola
   
    Necesitará pronto tooset seguridad de servicio de análisis de secuencia de entrada toohello Hola.
   
    ![En el almacenamiento de hello, abra la configuración, claves y realizar una copia de la clave de acceso principal de Hola](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>Iniciar exportación continua tooAzure almacenamiento
[exportación continua](app-insights-export-telemetry.md) transfiere los datos de Application Insights al almacenamiento de Azure.

1. Hola portal de Azure, examinar recursos de Application Insights toohello que creó para la aplicación.
   
    ![Elija Examinar, Application Insights, su aplicación.](./media/app-insights-export-stream-analytics/050.png)
2. Cree una exportación continua.
   
    ![Elija Configuración, Exportación continua, Agregar.](./media/app-insights-export-stream-analytics/060.png)

    Seleccione la cuenta de almacenamiento de Hola que creó anteriormente:

    ![Establecer el destino de la exportación de Hola](./media/app-insights-export-stream-analytics/070.png)

    Establecer a tipos de evento de hello que desea toosee:

    ![Elija los tipos de evento.](./media/app-insights-export-stream-analytics/080.png)

1. Permita que se acumulen algunos datos. Póngase cómo y deje que los usuarios usen su aplicación durante un tiempo. Así, aparecerá la telemetría y verá gráficos estadísticos en el [explorador de métricas](app-insights-metrics-explorer.md) y eventos individuales en la [búsqueda de diagnóstico](app-insights-diagnostic-search.md). 
   
    Y además, los datos de hello exportará tooyour almacenamiento. 
2. Inspeccionar los datos de hello exportado. En Visual Studio, elija **Ver/Cloud Explorer** y abra Azure/Almacenamiento. (Si no tiene esta opción de menú, necesita tooinstall hello Azure SDK: abra el cuadro de diálogo de proyecto nuevo de Hola y abra Visual C# / nube / obtener Microsoft Azure SDK para. NET.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Tome nota de la parte común de Hola de nombre de ruta de acceso de hello, que se deriva de la clave de nombre e instrumentación de la aplicación hello. 

eventos de Hola se escriben tooblob archivos en formato JSON. Cada archivo puede contener uno o varios eventos. Por lo que nos gustaría datos de eventos de tooread hello y filtrar campos Hola que queremos. Hay todo tipo de cosas, que podríamos hacer con los datos de hello, pero nuestro plan hoy en día es toouse análisis de transmisiones toopipe Hola datos tooPower BI.

## <a name="create-an-azure-stream-analytics-instance"></a>Creación de una instancia de Análisis de transmisiones de Azure
De hello [Portal de Azure clásico](https://manage.windowsazure.com/), seleccione servicio de análisis de transmisiones de Azure de Hola y crear un nuevo trabajo de análisis de transmisiones:

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Cuando se crea el nuevo trabajo de hello, expandir los detalles:

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Establecimiento de la ubicación del blob
Establézcalo tootake entrada desde el blob exportar continua:

![](./media/app-insights-export-stream-analytics/120.png)

Ahora deberá Hola clave de acceso principal de la cuenta de almacenamiento, que se ha indicado anteriormente. Utilizar esta configuración como Hola clave de la cuenta de almacenamiento.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Establecimiento del patrón del prefijo de la ruta de acceso
![](./media/app-insights-export-stream-analytics/140.png)

**Ser seguro tooset Hola formato de fecha tooYYYY-MM-DD (con guiones).**

Hola modelo de prefijo de ruta de acceso especifica que análisis de transmisiones busca archivos de entrada de hello en el almacenamiento de Hola. Necesita tooset se toohow toocorrespond exportar continua almacena los datos de Hola. Configúrelo como este caso que se muestra a continuación:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

En este ejemplo:

* `webapplication27`es Hola nombre de recurso de Application Insights hello **todas las minúsculas**.
* `1234...`es la clave de instrumentación de Hola de hello recurso de Application Insights, **omitir guiones**. 
* `PageViews`es el tipo de saludo de datos que desee tooanalyze. los tipos disponibles de Hello dependen de filtro de Hola que se establezca en Exportar continua. Examinar Hola Hola de toosee de los datos exportados en otros tipos disponibles y ver hello [Exportar modelo de datos](app-insights-export-data-model.md).
* `/{date}/{time}` es un patrón escrito literalmente.

> [!NOTE]
> Inspeccionar hello toomake de almacenamiento seguro de que obtener una ruta de acceso de hello derecho.
> 
> 

### <a name="finish-initial-setup"></a>Finalización de la instalación inicial
Confirme el formato de serialización de hello:

![Confirme y cierre el asistente.](./media/app-insights-export-stream-analytics/150.png)

Cerrar el Asistente de Hola y espere Hola el programa de instalación toocomplete.

> [!TIP]
> Utilice toodownload de comando de ejemplo de Hola algunos datos. Guardarla como un toodebug de ejemplo de prueba de la consulta.
> 
> 

## <a name="set-hello-output"></a>Salida de hello de conjunto
Ahora seleccione el trabajo y establezca la salida de hello.

![Seleccione nuevo canal de hello, haga clic en salidas, agregar, Power BI](./media/app-insights-export-stream-analytics/160.png)

Proporcionar la **cuenta profesional o educativa** tooauthorize tooaccess de análisis de transmisiones el recurso de Power BI. A continuación, inventar un nombre para la salida de Hola y de tabla y el conjunto de datos de hello destino Power BI.

![Invente tres nombres](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>Consulta de conjunto Hola
consulta de Hello rige la traducción de Hola de entrada toooutput.

![Seleccione el trabajo de Hola y haga clic en la consulta. Pegue el siguiente ejemplo de Hola.](./media/app-insights-export-stream-analytics/180.png)

Utilice Hola prueba función toocheck que se obtiene un resultado de hello derecho. Proporciona datos de ejemplo de Hola que tardó en página de entradas de Hola. 

### <a name="query-toodisplay-counts-of-events"></a>Consulta toodisplay recuentos de eventos
Pegue esta consulta:

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* entrada de exportación es alias Hola asignamos entrada de flujo de toohello
* salida de pbi es alias de salida de hello definimos
* Usamos [externa GetElements aplicar](https://msdn.microsoft.com/library/azure/dn706229.aspx) porque el nombre del evento de hello está en un arrray JSON anidado. A continuación, selecciona seleccione Hola Hola nombre del evento, junto con un recuento del número de Hola de instancias con ese nombre en hello período de tiempo. Hola [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) cláusula agrupa elementos de hello en períodos de tiempo de 1 minuto.

### <a name="query-toodisplay-metric-values"></a>Valores de métrica de toodisplay de consulta
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* Esta consulta obtiene los detalles de la hora del evento Hola métricas telemetría tooget Hola y el valor de métrica de Hola. valores de métrica de Hello quedan dentro de una matriz, por lo que usamos filas de hello externa GetElements aplicar patrón tooextract Hola. "myMetric" es el nombre de Hola de métrica de hello en este caso. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>Consulta tooinclude valores de propiedades de dimensión
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* Esta consulta incluye valores de propiedades de dimensión Hola sin dependiendo de una dimensión determinada está en un índice de matriz de dimensión Hola fijo.

## <a name="run-hello-job"></a>Ejecutar trabajo de Hola
Puede seleccionar una fecha en hello más allá de trabajo de hello toostart desde. 

![Seleccione el trabajo de Hola y haga clic en la consulta. Pegue el siguiente ejemplo de Hola.](./media/app-insights-export-stream-analytics/190.png)

Espere hasta que se ejecuta el trabajo de Hola.

## <a name="see-results-in-power-bi"></a>Visualización de resultados en Power BI
> [!WARNING]
> Hay mucho mejor y más sencillo [formas recomendadas toodisplay datos de Application Insights en Power BI](app-insights-export-power-bi.md). ruta de acceso se ilustra a continuación Hello es simplemente una tooillustrate de ejemplo cómo tooprocess exportan datos.
> 
> 

Abra Power BI con su trabajo o cuenta del centro educativo y Hola seleccione conjunto de datos y tabla que ha definido como salida de hello de trabajo de análisis de transmisiones de Hola.

![En Power BI, seleccione el conjunto de datos y los campos.](./media/app-insights-export-stream-analytics/200.png)

Ahora puede usar este conjunto de datos en informes y paneles de [Power BI](https://powerbi.microsoft.com).

![En Power BI, seleccione el conjunto de datos y los campos.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>¿No hay datos?
* Compruebe que [formato de fecha de conjunto hello](#set-path-prefix-pattern) correctamente tooYYYY-MM-DD (con guiones).

## <a name="video"></a>Vídeo
Noam Ben Zeev muestra cómo tooprocess había exportado mediante el análisis de transmisiones de datos.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Exportación continua](app-insights-export-telemetry.md)
* [Referencia para tipos de propiedad de Hola y valores del modelo de datos detallados.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

