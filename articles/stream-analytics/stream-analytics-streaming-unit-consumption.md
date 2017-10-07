---
title: "Análisis de transmisiones de Azure: Optimizar su unidades de transmisión por secuencias de trabajo toouse eficazmente | Documentos de Microsoft"
description: Procedimientos de consulta recomendados para escalado y rendimiento en Azure Stream Analytics.
keywords: unidad de streaming, rendimiento de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>Optimizar eficazmente la toouse trabajo unidades de transmisión por secuencias

Análisis de transmisiones de Azure agrega rendimiento Hola "peso" de la ejecución de un trabajo en unidades de transmisión por secuencias (SUs). SUs representan recursos informáticos Hola que son consumido tooexecute un trabajo. SUs proporcionan una manera toodescribe Hola relativa de eventos basándose en una medición mezclada de CPU, memoria, la capacidad de procesamiento y se leen y escriben las tasas. Esta capacidad le permite centrarse en la lógica de la consulta de Hola y quita también de la necesidad de consideraciones de rendimiento de nivel de almacenamiento de tooknow, asignar memoria para el trabajo manualmente y aproximado Hola CPU core-recuento necesario toorun su trabajo de manera oportuna.

## <a name="how-many-sus-are-required-for-a-job"></a>¿Cuántas SU son necesarias para un trabajo?

Elegir número Hola de SUs necesarias para un trabajo determinado depende de la configuración de partición de Hola para las entradas de Hola y consulta de Hola que se define en el trabajo de Hola. Hola **escala** hoja permite tooset Hola derecha número de SUs. Es una práctica recomendada tooallocate SUs más de los necesarios. motor de procesamiento de análisis de transmisiones de Hola se optimiza para la latencia y rendimiento en el costo de Hola de asignar memoria adicional.

En general, se recomienda hello es toostart con 6 SUs para consultas que no utilizan *PARTITION BY*. A continuación, determine Hola idóneo mediante un método de prueba y error en el que modifican número Hola de SUs después de pasar representativos cantidades de datos y examine la métrica de uso de hello SU %.

Análisis de transmisiones de Azure mantiene eventos en una ventana que se denomina hello "volver a ordenar búfer" antes de iniciar cualquier procesamiento. Eventos se ordenan dentro de la ventana de hello volver a ordenar por hora y operaciones siguientes se realizan en los eventos de hello temporalmente ordenado. Reordenación de eventos por hora se asegura de que el operador de hello tiene visibilidad en todos los eventos de Hola Hola estipulada período de tiempo. Operador de Hola también permite realizar el procesamiento necesario hello y generar un resultado. Un efecto secundario de este mecanismo es que se retrasa el procesamiento por duración Hola de ventana de hello volver a ordenar. superficie de memoria de Hola de trabajo de hello (lo que afecta al consumo de SU) es una función del tamaño de Hola de este número de hello y ventana de volver a ordenar de eventos incluidos en él.

> [!NOTE]
> Cuando se cambia el número de Hola de lectores durante las actualizaciones del trabajo, las advertencias transitorias se escriben registros tooaudit. Los trabajos de Stream Analytics se recuperan automáticamente de estos problemas transitorios.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>Causas comunes de memoria alta por el uso elevado de SU para la ejecución de trabajos

### <a name="high-cardinality-for-group-by"></a>Alta cardinalidad para GROUP BY

cardinalidad de Hola de eventos de entrada dicta el uso de memoria de trabajo de Hola.

Por ejemplo, en `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, Hola número asociado con **agrupado** es cardinalidad Hola de consulta de Hola.

toomitigate problemas causados por una cardinalidad alta, escalar horizontalmente consultas Hola aumentando las particiones que usan **PARTITION BY**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

Hola número de *agrupado* es la cardinalidad de Hola de GROUP BY aquí.

Después de crear particiones consulta hello, se extiende a través de varios nodos. Como resultado, se reduce número Hola de eventos que entran en cada nodo, que a su vez reduce el tamaño de hello del búfer de hello volver a ordenar. También debe particionar las particiones de centro de eventos mediante partitionid.

### <a name="high-unmatched-event-count-for-join"></a>Recuento alto de eventos no coincidentes para JOIN

número de Hola de eventos no coincidentes en una combinación afecta al uso de memoria de Hola de consulta de Hola. Por ejemplo, realizar una consulta que se examina el número de hello toofind de impresiones de ad que genera clics:

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

En este escenario, es posible que se muestren muchos anuncios y se generen pocos clics. Un resultado de este tipo requeriría Hola trabajo tookeep todos los eventos de Hola de ventana de tiempo de Hola. cantidad de Hola de memoria consumida es la tasa de tamaño y eventos de la ventana de toohello proporcional. 

toomitigate crea particiones de esta situación, el escalado horizontal consulta Hola aumentando mediante PARTITION BY. 

Después de crear particiones consulta hello, se extiende a través de varios nodos de procesamiento. Como resultado, se reduce número Hola de eventos que entran en cada nodo, que a su vez reduce el tamaño de hello del búfer de hello volver a ordenar.

### <a name="large-number-of-out-of-order-events"></a>Gran número de eventos desordenados 

Un gran número de eventos desordenados dentro de un período de tiempo grandes hace tamaño Hola de toobe de "reordenar búfer" del Hola mayor. toomitigate crea particiones de esta situación, consultas de escala Hola aumentando mediante PARTITION BY. Después de crear particiones consulta hello, se extiende a través de varios nodos. Como resultado, se reduce número Hola de eventos que entran en cada nodo, que a su vez reduce el tamaño de hello del búfer de hello volver a ordenar. 


## <a name="get-help"></a>Obtener ayuda
Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
