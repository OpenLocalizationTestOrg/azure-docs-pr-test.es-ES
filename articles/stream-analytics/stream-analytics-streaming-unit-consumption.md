---
title: "Azure Stream Analytics: optimización del trabajo para usar unidades de streaming de forma efectiva | Microsoft Docs"
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
ms.openlocfilehash: 1441a5df4fd92abf85763ca9a1512503b1a0da56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-your-job-to-use-streaming-units-efficiently"></a>Optimización del trabajo para usar unidades de streaming de forma eficaz

Azure Stream Analytics agrega el "peso" de rendimiento de ejecutar un trabajo en unidades de streaming (SU). Las SU representan los recursos informáticos que se usan para ejecutar un trabajo. Las SU proporcionan una forma de describir la capacidad de procesamiento del evento relativo en función de una medida que combina la CPU, la memoria y las tasas de lectura y escritura. Esta capacidad le permite centrarse en la lógica de consulta y elimina la necesidad de conocer las consideraciones de rendimiento de los niveles de almacenamiento, de asignar memoria para su trabajo manualmente y de aproximar el número de núcleos de CPU para ejecutar su trabajo de manera oportuna.

## <a name="how-many-sus-are-required-for-a-job"></a>¿Cuántas SU son necesarias para un trabajo?

La elección del número de SU necesarias para un trabajo determinado depende de la configuración de particiones de las entradas y de la consulta definida dentro del trabajo. La hoja **Escala** le permite establecer el número correcto de SU. Es recomendable asignar más unidades de streaming de las necesarias. El motor de procesamiento de Stream Analytics se optimiza para la latencia y el rendimiento, a costa de asignar memoria adicional.

En general, el procedimiento recomendado es comenzar con 6 SU para consultas que no usen *PARTITION BY*. Luego, determine el punto favorable mediante un método de prueba y error en el que modifica el número de SU después de pasar las cantidades de datos representativas y examinar la métrica de porcentaje de uso de SU.

Azure Stream Analytics mantiene los eventos en una ventana llamada "búfer de reordenación" antes de comenzar cualquier procesamiento. Los eventos se ordenan dentro de la ventana de reordenación por hora y las operaciones posteriores se realizan en los eventos ordenados temporalmente. La reordenación de eventos por hora garantiza que el operador tiene visibilidad sobre los tres eventos en el período de tiempo estipulado. También permite al operador realizar el procesamiento de requisitos y generar una salida. Un efecto secundario de este mecanismo es que el procesamiento se retrasa el tiempo que dura la ventana de reorganización. La superficie de memoria del trabajo (que afecta al consumo de la unidad de streaming) es una función del tamaño de esta ventana de reordenación y el número de eventos que contiene.

> [!NOTE]
> Cuando el número de lectores cambia durante las actualizaciones de trabajos, se escriben advertencias transitorias en registros de auditoría. Los trabajos de Stream Analytics se recuperan automáticamente de estos problemas transitorios.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>Causas comunes de memoria alta por el uso elevado de SU para la ejecución de trabajos

### <a name="high-cardinality-for-group-by"></a>Alta cardinalidad para GROUP BY

La cardinalidad de los eventos de entrada determina el uso de memoria para el trabajo.

Por ejemplo, en `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, el número asociado con **clustered** es la cardinalidad de la consulta.

Para mitigar los problemas ocasionados por una cardinalidad alta, escale horizontalmente la consulta aumentando las particiones con **PARTITION BY**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

Aquí, el número de *clustered* es la cardinalidad de GROUP BY.

Una vez que la consulta está particionada, se extiende por varios nodos. Como resultado, el número de eventos que entra en cada nodo se reduce, lo que a su vez disminuye el tamaño del búfer de reordenación. También debe particionar las particiones de centro de eventos mediante partitionid.

### <a name="high-unmatched-event-count-for-join"></a>Recuento alto de eventos no coincidentes para JOIN

El número de eventos no coincidentes en JOIN afecta a la utilización de memoria de la consulta. Por ejemplo, imagine una consulta que busca encontrar el número de impresiones de anuncios que generan clics:

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

En este escenario, es posible que se muestren muchos anuncios y se generen pocos clics. Un resultado de este tipo podría requerir que el trabajo mantuviera todos los eventos dentro de la ventana de tiempo. La cantidad de memoria consumida es proporcional al tamaño de ventana y la tasa de eventos. 

Para mitigar esta situación, escale horizontalmente la consulta aumentando las particiones mediante PARTITION BY. 

Después de particionar la consulta, se distribuye entre varios nodos de procesamiento. Como resultado, el número de eventos que entra en cada nodo se reduce, lo que a su vez disminuye el tamaño del búfer de reordenación.

### <a name="large-number-of-out-of-order-events"></a>Gran número de eventos desordenados 

Un gran número de eventos desordenados en una ventana de tiempo grande hace que el tamaño del "búfer de reordenación" sea mayor. Para mitigar esta situación, escale la consulta aumentando las particiones mediante PARTITION BY. Una vez que la consulta está particionada, se extiende por varios nodos. Como resultado, el número de eventos que entra en cada nodo se reduce, lo que a su vez disminuye el tamaño del búfer de reordenación. 


## <a name="get-help"></a>Obtener ayuda
Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción a Azure Stream Analytics](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
