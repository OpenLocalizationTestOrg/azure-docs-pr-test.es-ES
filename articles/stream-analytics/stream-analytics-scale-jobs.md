---
title: "rendimiento de tooincrease de trabajos de análisis de transmisiones de aaaScale | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale los trabajos de análisis de transmisiones por configurar particiones de entrada, la definición de la consulta de hello para la optimización y la configuración del trabajo unidades de streaming."
keywords: "datos de streaming, procesamiento de datos de streaming, optimización del análisis"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>Rendimiento de procesamiento de datos de escala análisis de transmisiones de Azure trabajos tooincrease stream
Este artículo muestra cómo tootune un análisis de transmisiones de consultar el rendimiento tooincrease para trabajos de análisis de transmisión por secuencias. Obtener información sobre cómo trabajos tooscale análisis de transmisiones mediante la configuración de particiones de entrada, definición de la consulta de análisis de optimización hello y calcular y la configuración del trabajo *unidades de streaming* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>¿Qué partes de Hola de un trabajo de análisis de transmisiones?
Una definición de trabajo de Análisis de transmisiones incluye entradas, una consulta y la salida. Las entradas son donde trabajo Hola lee el flujo de datos de Hola de. consulta Hello es flujo de entrada de datos de hello tootransform usado, y salida de hello es donde trabajo Hola envía los resultados del trabajo de Hola a.  

Un trabajo requiere al menos un origen de entrada de streaming de datos. Hello origen de entrada de flujo de datos puede almacenarse en un centro de eventos de Azure o en el almacenamiento de blobs de Azure. Para obtener más información, consulte [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md) y [Introducción al uso de análisis de transmisiones de Azure](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Particiones en Event Hubs y Azure Storage
Ajuste de escala en un trabajo de análisis de transmisiones aprovecha las ventajas de las particiones de hello entrada o salida. La creación de particiones permite dividir los datos en subconjuntos en función de una clave de partición. Un proceso que consume datos de hello (por ejemplo, un trabajo de análisis de transmisión por secuencias) puede consumir y escribir diferentes particiones en paralelo, lo que aumenta el rendimiento. Si trabaja con Stream Analytics, puede aprovechar las ventajas de las particiones en Event Hubs y Blob Storage. 

Para obtener más información acerca de las particiones, vea Hola siguientes artículos:

* [Información general de las características de Event Hubs](../event-hubs/event-hubs-features.md#partitions)
* [Creación de particiones de datos](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Unidades de streaming (SU)
Transmisión por secuencias unidades (SUs) representan Hola recursos y capacidad de ejecución que son necesarios en orden tooexecute un trabajo de análisis de transmisiones de Azure. SUs proporcionan una manera toodescribe Hola relativa de eventos basándose en una medición mezclada de CPU, memoria, la capacidad de procesamiento y se leen y escriben las tasas. Cada SU corresponde tooroughly 1 MB/segundo de rendimiento. 

Elegir SUs cuántos son necesarios para un trabajo determinado depende en configuración de la partición de Hola para las entradas de Hola y de consulta de hello definida para el trabajo de Hola. Puede seleccionar una cuota de tooyour en SUs para un trabajo. De forma predeterminada, cada suscripción de Azure tiene una cuota de seguridad de SUs too50 para todos los trabajos de análisis de hello en una región específica. tooincrease SUs para las suscripciones más allá de esta cuota, póngase en contacto con [Microsoft Support](http://support.microsoft.com). Los valores válidos para unidades de streaming por trabajo son 1, 3, 6 y más en incrementos de 6.

## <a name="embarrassingly-parallel-jobs"></a>Trabajos embarazosamente paralelos
Un *embarazosamente paralelas* trabajo es el escenario más escalable Hola tenemos en análisis de transmisiones de Azure. Se conecta a una partición de la instancia de entrada tooone Hola de partición de tooone Hola consulta de salida de hello. Este paralelismo tiene Hola según los requisitos:

1. Si la lógica de la consulta depende de hello misma clave que se va a procesar por hello misma consulta instancia, debe asegurarse de que los eventos de hello van toohello misma partición de los datos especificados. Los centros de eventos, esto significa que los datos de eventos de hello deben tener hello **PartitionKey** valor establecido. También puede usar remitentes con particiones. Para el almacenamiento de blobs, esto significa que se envían eventos de hello toohello carpeta de la misma partición. Si la lógica de la consulta no requiere Hola misma clave toobe procesado por hello misma consulta instancia, puede pasar por alto este requisito. Un ejemplo de esta lógica sería una sencilla consulta select-project-filter.  

2. Una vez que se distribuyen los datos de hello en lado de entrada de hello, debe asegurarse de que la consulta tiene particiones. Para ello, deberá toouse **Partition By** en todos los pasos de Hola. Se permiten varios pasos, pero todas ellas deben tener particiones por hello misma clave. Actualmente, se debe establecer Hola particiones clave demasiado**PartitionId** en orden para hello trabajo toobe totalmente paralela.  

3. Solo Event Hubs y Blob Storage admiten en este momento salidas con particiones. Para la salida del concentrador de eventos, debe configurar toobe clave de partición de hello **PartitionId**. Para la salida de almacenamiento de blobs, no tiene toodo nada.  

4. número de Hola de particiones de entrada debe ser igual a número Hola de particiones de salida. La salida de Blob Storage no admite en este momento la creación de particiones. Pero no importa, porque hereda Hola esquema de consulta de nivel superior de Hola de particiones. Vea ejemplos de valores de partición que permiten un trabajo totalmente paralelo:  

   * Ocho particiones de entrada de Event Hubs y ocho particiones de salida de Event Hubs
   * Ocho particiones de entrada de Event Hubs y salida de Blob Storage  
   * Ocho particiones de entrada de Blob Storage y salida de Blob Storage  
   * Ocho particiones de entrada de Blob Storage y ocho particiones de salida de Event Hubs  

Hello las secciones siguientes describen algunos escenarios de ejemplo que son embarazosamente paralelas.

### <a name="simple-query"></a>Consulta sencilla

* Entrada: Event Hubs con ocho particiones
* Salida: Event Hubs con ocho particiones

Consulta:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

Esta consulta es un filtro sencillo. Por lo tanto, no es necesario tooworry acerca de las particiones de entrada de Hola que se están enviando toohello concentrador de eventos. Tenga en cuenta que consultan Hola incluye **partición por PartitionId**, por lo que cumple el requisito #2 de antes. Para la salida de hello, necesitamos salida del concentrador de eventos tooconfigure hello en el conjunto de claves de la partición de Hola de hello trabajo toohave demasiado**PartitionId**. Una última comprobación es toomake asegurarse de que el número de Hola de particiones de entrada es igual toohello número de particiones de salida.

### <a name="query-with-a-grouping-key"></a>Consulta con una clave de agrupación

* Entrada: Event Hubs con ocho particiones
* Salida: Blob Storage

Consulta:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Esta consulta tiene una clave de agrupación. Por lo tanto, Hola mismo toobe necesidades clave procesado por hello misma consulta instancias, lo que significa que los eventos se deben enviar toohello concentrador de eventos de manera con particiones. ¿Pero qué clave debe usarse? **PartitionId** es un concepto de lógica de trabajos. clave Hola nos preocupamos por realmente es **TollBoothId**, tan Hola **PartitionKey** debe ser el valor de los datos de evento de hello **TollBoothId**. Para ello en la consulta de hello estableciendo **Partition By** demasiado**PartitionId**. Puesto que la salida de hello es el almacenamiento de blobs, no es necesario tooworry acerca de cómo configurar un valor de clave de partición, según el requisito #4.

### <a name="multi-step-query-with-a-grouping-key"></a>Consulta de varios pasos con una clave de agrupación
* Entrada: Event Hubs con ocho particiones
* Salida: instancia de Event Hubs con ocho particiones

Consulta:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Esta consulta tiene una clave de agrupación, Hola así mismo toobe necesidades clave procesado por hello misma instancia de consulta. Podemos usar Hola misma estrategia como en el ejemplo anterior de Hola. En este caso, la consulta de hello tiene varios pasos. ¿Cada paso tiene **Partition By PartitionId**? Sí, por lo que la consulta de hello cumple el requisito #3. Para la salida de hello, necesitamos clave de partición de hello tooset demasiado**PartitionId**, tal y como se explicó anteriormente. También podemos ver que tiene Hola mismo número de particiones como entrada de Hola.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Escenarios de ejemplo que *no* son embarazosamente paralelos

En la sección anterior de hello, mostramos algunos escenarios embarazosamente paralelas. En esta sección, se tratan los escenarios que no cumplen todos los requisitos toobe de hello embarazosamente paralelas. 

### <a name="mismatched-partition-count"></a>Recuento de particiones no coincidente
* Entrada: Event Hubs con ocho particiones
* Salida: Event Hubs con 32 particiones

En este caso, no importa qué consulta hello es. Si el recuento de particiones de entrada de hello no coincide con recuento de particiones de salida de hello, topología hello no embarazosamente paralela.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>No se usa Event Hubs ni Blob Storage como salida
* Entrada: Event Hubs con ocho particiones
* Salida: PowerBI

La salida de PowerBI no admite en este momento la creación de particiones. Por consiguiente, este escenario no es embarazosamente paralelo.

### <a name="multi-step-query-with-different-partition-by-values"></a>Consulta de varios pasos con diferentes valores de Partition By
* Entrada: Event Hubs con ocho particiones
* Salida: Event Hubs con ocho particiones

Consulta:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Como puede ver, Hola segundo paso utiliza **TollBoothId** como Hola clave de partición. Este paso es Hola mismo no como primer paso de hello y, por lo tanto, requiere nos toodo un orden aleatorio. 

Hello ejemplos anteriores muestran algunos trabajos de análisis de transmisiones que se ajustan demasiado (o no) en una topología embarazosamente paralela. Si cumple, tienen el potencial de Hola para maximizar su alcance. En el caso de los trabajos que no se ajustan a uno de estos perfiles, habrá una guía de escalado disponible en futuras actualizaciones. Por ahora, use instrucciones generales de Hola de hello las secciones siguientes.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>Calcular la capacidad máxima de transmisión por secuencias Hola de un trabajo
número total de Hola de unidades de streaming que puede usarse en un trabajo de análisis de transmisiones depende de número de Hola de pasos en la consulta de hello definido para el trabajo de Hola y el número de Hola de particiones para cada paso.

### <a name="steps-in-a-query"></a>Pasos de una consulta
Una consulta puede tener uno o varios pasos. Cada paso es una subconsulta definida por hello **WITH** palabra clave. consulta de Hola que está fuera de hello **WITH** palabra clave (sólo una consulta) también se considera como un paso, como hello **seleccione** instrucción Hola después de consulta:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

Esta consulta tiene dos pasos.

> [!NOTE]
> Esta consulta se explica con más detalle más adelante en el artículo de Hola.
>  

### <a name="partition-a-step"></a>Posicionamiento de un paso
Un paso de creación de particiones requiere Hola condiciones siguientes:

* origen de entrada de Hello debe estar particionado. 
* Hola **seleccione** debe leer la instrucción de consulta de Hola desde un origen de entrada con particiones.
* consulta de Hello en el paso de Hola debe tener hello **Partition By** palabra clave.

Cuando una consulta tiene particiones, los eventos de entrada de hello son grupos de procesado y se agregan en partición independiente y salidas de eventos se generan para cada uno de los grupos de Hola. Si desea un agregado combinado, debe crear un segundo tooaggregate paso sin particiones.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Calcular el número máximo de hello unidades para un trabajo de streaming
Juntos, todos los pasos de particiones no pueden escalar un toosix unidades (SUs) para un trabajo de análisis de transmisiones de streaming. deben estar particionados SUs tooadd, un paso. Cada partición puede tener seis unidades de streaming.

<table border="1">
<tr><th>Consultar</th><th>SUs máximo para el trabajo de Hola</th></td>

<tr><td>
<ul>
<li>consulta de Hello contiene un solo paso.</li>
<li>paso de Hello no tiene particiones.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>flujo de datos de entrada de Hola se particiona por 3.</li>
<li>consulta de Hello contiene un solo paso.</li>
<li>paso de Hello tiene particiones.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>consulta de Hello incluye dos pasos.</li>
<li>Ninguno de los pasos de hello tiene particiones.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>flujo de datos de entrada de Hola se particiona por 3.</li>
<li>consulta de Hello incluye dos pasos. paso de entrada de Hola se divide y no es el segundo paso de Hola.</li>
<li>Hola <strong>seleccione</strong> instrucción lee de la entrada de hello con particiones.</li>
</ul>
</td>
<td>24 (18 para los pasos particionados y 6 para los pasos no particionados)</td></tr>
</table>

### <a name="examples-of-scaling"></a>Ejemplos de escalado

Hello siguiente consulta calcula Hola número de automóviles dentro de una ventana de tres minutos que se va a través de una estación de peaje que tiene tres casetas de cuota. Esta consulta se puede ampliar SUs toosix.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

toouse más SUs para Hola consulta, ambos Hola flujo de datos de entrada y consulta de hello debe estar particionado. Como partición de flujo de datos de Hola se establece too3, hello siguiente consulta modificada se puede ampliar SUs too18:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Cuando una consulta tiene particiones, los eventos de entrada de Hola se procesan y se agregan en grupos de partición independiente. También se genera el evento de salida para cada uno de los grupos de Hola. Creación de particiones puede provocar algunos resultados inesperados cuando hello **GROUP BY** campo no es de clave de partición de hello en el flujo de datos de entrada de Hola. Por ejemplo, hello **TollBoothId** campo de consulta anterior hello no es clave de partición de Hola de **Entrada1**. resultado de Hello es ese hello datos entre cabinas #1 pueden propagarse en varias particiones.

Cada uno de hello **Entrada1** particiones se procesarán por separado mediante análisis de transmisiones. Como resultado, varios registros de recuento de automóvil Hola para Hola mismo cabinas Hola se creará la misma ventana de saltos de tamaño constante. Si no se puede cambiar la clave de partición de entrada de hello, puede solucionar este problema mediante la adición de un paso de partición que no es, como en el siguiente ejemplo de Hola:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Esta consulta puede ser SUs too24 escalado.

> [!NOTE]
> Si va a unir dos flujos, asegúrese de que secuencias Hola se dividen en particiones por clave de partición de Hola de columna de Hola que usar toocreate Hola combinaciones. También asegúrese de que dispone de hello mismo número de particiones en ambas secuencias.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Configuración de las unidades de streaming de Stream Analytics

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En lista de Hola de recursos, busque el trabajo de análisis de transmisiones de Hola que desee tooscale y, a continuación, vuelva a abrirlo.
3. Hola trabajo hoja, en **configurar**, haga clic en **escala**.

    ![Configuración del trabajo de Stream Analytics en Azure Portal][img.stream.analytics.preview.portal.settings.scale]

4. Use Hola control deslizante tooset Hola SUs trabajo Hola. Observe que son valores de SU toospecific limitado.


## <a name="monitor-job-performance"></a>Supervisión del rendimiento del trabajo
Con hello portal de Azure, puede seguir el rendimiento de un trabajo hello:

![Trabajos de supervisión de Análisis de transmisiones de Azure][img.stream.analytics.monitor.job]

Calcular el rendimiento de hello esperada de carga de trabajo de Hola. Si el rendimiento de hello es inferior a lo esperado, optimizar partición entrada hello, optimizar la consulta de Hola y agregar SUs tooyour trabajo.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>Visualizar el rendimiento de análisis de transmisiones a escala: escenario de frambuesa Pi Hola
toohelp que comprender cómo escalar trabajos de análisis de transmisiones, se ha realizado un experimento basado en la entrada desde un dispositivo de frambuesa Pi. Este experimento nos permite ver el efecto de hello en el rendimiento de varias particiones y unidades de transmisión por secuencias.

En este escenario, el dispositivo de hello envía concentrador de eventos de tooan de sensor datos (clientes). Análisis de transmisión por secuencias procesa los datos de Hola y envía una alerta o estadísticas como un concentrador de eventos de tooanother de salida. 

cliente de Hello envía los datos de sensor en formato JSON. salida de datos de Hello también está en formato JSON. datos de Hello tiene el siguiente aspecto:

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

Hola después de consulta es toosend usa una alerta cuando se desactiva una luz:

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Medición de la capacidad de procesamiento

En este contexto, el rendimiento es la cantidad de Hola de datos de entrada procesados por el análisis de transmisiones en una cantidad fija de tiempo. (Se mide durante 10 minutos). tooachieve Hola mejor procesamiento de rendimiento para hello los datos de entrada, ambos Hola flujo entrada y consulta Hola se divide en particiones. Hemos incluido **COUNT()** en hello consulta toomeasure se han procesado la cantidad de eventos de entrada. trabajo de hello seguro toomake no estaba esperando simplemente toocome de eventos de entrada, cada partición del concentrador de eventos de entrada de Hola se haya cargado previamente con unos 300 MB de datos de entrada.

Hello tabla siguiente muestra los resultados de hello que vimos cuando aumentamos número Hola de unidades de streaming y recuentos de partición correspondiente hello en los centros de eventos.  

<table border="1">
<tr><th>Particiones de entrada</th><th>Particiones de salida</th><th>Unidades de streaming</th><th>Capacidad de procesamiento sostenida
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4,06 MB/s</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8,06 MB/s</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38,32 MB/s</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172,67 MB/s</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454,27 MB/s</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609,69 MB/s</td>
</tr>
</table>

Y hello gráfico siguiente muestra una visualización de relación de hello entre SUs y rendimiento.

![IMG.Stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Obtener ayuda
Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

