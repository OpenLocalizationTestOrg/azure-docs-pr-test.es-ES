---
title: "aaaDebug análisis de transmisiones de Azure con receptores de eventos de base de datos central | Documentos de Microsoft"
description: "Prácticas recomendadas de consulta para la consideración de grupos de consumidores de Event Hubs en trabajos de Stream Analytics."
keywords: "límite de centro de eventos, grupo de consumidores"
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Depuración de Azure Stream Analytics con receptores de Event Hubs

Puede usar los centros de eventos de Azure en los datos de análisis de transmisiones de Azure tooingest o la salida de un trabajo. Una práctica recomendada para el uso de los centros de eventos es toouse varios grupos de consumidores, escalabilidad de trabajo tooensure. Una razón es que número Hola de lectores en el trabajo de análisis de transmisiones de Hola para una entrada específica afecta al número de Hola de lectores en un grupo único consumidor. número exacto de Hola de destinatarios se basa en los detalles de implementación internos para la lógica de la topología de ampliación de Hola. número de Hola de destinatarios no se expone externamente. número de Hola de lectores puede cambiar en tiempo de inicio del trabajo de Hola o durante las actualizaciones del trabajo.

> [!NOTE]
> Cuando se cambia el número de Hola de lectores durante la actualización del trabajo, las advertencias transitorias se escriben registros tooaudit. Los trabajos de Stream Analytics se recuperan automáticamente de estos problemas transitorios.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>El número de lectores por partición supera el límite de Event Hubs de cinco

Escenarios de en qué Hola número de lectores por partición supera el límite de los centros de eventos de Hola de cinco Hola siguientes:

* Varias instrucciones SELECT: si usa varias instrucciones SELECT que hacen referencia demasiado**mismo** concentrador de eventos de entrada, cada instrucción SELECT hace que un nuevo toobe de receptor creado.
* Unión: Cuando se utiliza una unión, es posible toohave varias entradas que hacen referencia toohello **mismo** grupo de concentrador y consumidor de eventos.
* AUTOCOMBINACIÓN: Cuando se usa una operación JOIN de AUTOSERVICIO, es posible toorefer toohello **mismo** concentrador de eventos varias veces.

## <a name="solution"></a>Solución

Hello siguientes prácticas recomendadas pueden ayudar a mitigar escenarios en qué Hola número de lectores por partición supera el límite de los centros de eventos de Hola de cinco.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>División de la consulta en varios pasos mediante una cláusula WITH

cláusula WITH de Hello especifica un conjunto de resultados temporal indicado que puede hacer referencia a una cláusula FROM en consulta Hola. Definir cláusula WITH de hello en el ámbito de ejecución de Hola de una sola instrucción SELECT.

Por ejemplo, en lugar de esta consulta:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Utilice esta consulta:

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Asegúrese de que las entradas enlazan grupos de consumidores toodifferent

Para las consultas en el que tres o más entradas están conectado toohello mismo consumidor de los centros de eventos de grupo, cree grupos de consumidores independientes. Esto requiere la creación de hello de entradas de análisis de transmisiones adicionales.


## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooStream análisis](stream-analytics-introduction.md)
* [Introducción a Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalado de trabajos de Stream Analytics](stream-analytics-scale-jobs.md)
* [Referencia de lenguaje de consulta de Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
