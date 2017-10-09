---
title: "las consultas aaaDebug análisis de transmisiones de Azure mediante el uso de SELECT INTO | Documentos de Microsoft"
description: Datos de ejemplo de consulta intermedia mediante instrucciones SELECT INTO en Stream Analytics
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Depuración de consultas mediante instrucciones SELECT INTO

En el procesamiento de datos en tiempo real, saber qué datos Hola parece en medio de Hola de hello consulta puede ser útil. Como las entradas o pasos de un trabajo de Azure Stream Analytics se pueden leer muchas veces, puede escribir instrucciones SELECT INTO adicionales. Si lo hace, genera los datos intermedios en el almacenamiento y le permite inspeccionar la exactitud de Hola de datos de hello, al igual que *inspeccionar variables* hace cuando se depura un programa.

## <a name="use-select-into-toocheck-hello-data-stream"></a>Use SELECT INTO toocheck Hola flujo de datos

Hello consulta de ejemplo siguiente en un trabajo de análisis de transmisiones de Azure tiene un flujo entrada, dos entradas de datos de referencia y un almacenamiento de tabla tooAzure de salida. consulta de Hello combina datos de concentrador de eventos de Hola y dos blobs tooget Hola nombre y categoría de información de referencia:

![Ejemplo de consulta SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Tenga en cuenta que se ejecuta el trabajo de hello, pero no se genera ningún evento de salida de hello. En hello **supervisión** icono, se muestra a continuación, puede ver que Hola entrada produce datos, pero no sabe qué paso de hello **UNIR** iniciadas todos Hola toobe de eventos que se quita.

![icono de supervisión de Hola](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
En esta situación, puede agregar algunas instrucciones de SELECT INTO adicionales demasiado "iniciar" hello los resultados intermedios de la combinación y datos de Hola que se leen de la entrada de Hola.

En este ejemplo, hemos agregado dos nuevas "salidas temporales". Estas pueden ser cualquier receptor que desee. Aquí usamos Azure Storage como ejemplo:

![Adición de instrucciones SELECT INTO adicionales](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

A continuación, puede volver a escribir consultas Hola similar al siguiente:

![Consulta SELECT INTO reescrita](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Ahora iniciar nuevo trabajo de Hola y permitir su ejecución durante unos minutos. A continuación, consultar temp1 y temp2 con hello tooproduce de Visual Studio en la nube Explorer las tablas siguientes:

**tabla temp1**
![SELECT INTO tabla temp1](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**tabla temp2**
![SELECT INTO tabla temp2](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Como puede ver, temp1 y temp2 tienen datos y columna de nombre de Hola se rellena correctamente en temp2. Sin embargo, dado que todavía no hay ningún dato en la salida, algo sucede:

![Tabla SELECT INTO output1 sin datos](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Mediante el muestreo de datos de hello, puede estar casi seguro de que el problema de hello está Hola segundo combinación. Puede descargar los datos de referencia de Hola de blob de Hola y eche un vistazo:

![Tabla de referencia de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Como puede ver, formato de Hola de hello GUID en estos datos de referencia es distinto del formato de Hola de hello [columna temp2 from]. Por eso no llegan datos hello en output1 según lo previsto.

Puede corregir el formato de datos de hello, cargar blob tooreference y vuelva a intentarlo:

![Tabla temporal de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

En esta ocasión, datos de hello en la salida de hello formatea y rellena según lo previsto.

![Tabla final de SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Obtener ayuda

Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes

* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

