---
title: "ejemplos de patrones de uso comunes de análisis de transmisiones los aaaQuery | Documentos de Microsoft"
description: Patrones de consulta comunes de Azure Stream Analytics
keywords: ejemplos de consultas
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>Ejemplos de consulta para patrones de uso comunes de Stream Analytics
## <a name="introduction"></a>Introducción
Las consultas de Azure Stream Analytics se expresan en un lenguaje de consulta similar a SQL. Estas consultas se documentan en hello [referencia del lenguaje de consulta de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn834998.aspx) guía. Este patrones de consulta común de artículo se describen las soluciones tooseveral, basándose en situaciones del mundo real. Es un trabajo en curso y continúa toobe actualizada con nuevos patrones de forma continuada.

## <a name="query-example-convert-data-types"></a>Ejemplo de consulta: conversión de tipos de datos
**Descripción**: definir tipos de Hola de propiedades en el flujo de entrada de Hola.
Por ejemplo, hello automóvil procede en el flujo de entrada de hello como cadenas y la importancia de necesita toobe convertir demasiado**INT** tooperform **suma** , configúrelo.

**Entrada**:

| Asegúrese | Hora | Peso |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |"1000" |
| Honda |2015-01-01T00:00:02.0000000Z |"2000" |

**Salida**:

| Asegúrese | Peso |
| --- | --- |
| Honda |3000 |

**Solución**:

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Explicación**: Use un **conversión** instrucción Hola **peso** campo toospecify su tipo de datos. Ver lista de Hola de tipos de datos compatibles en [tipos de datos (análisis de transmisiones de Azure)](https://msdn.microsoft.com/library/azure/dn835065.aspx).

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>Ejemplo de consulta: usan Like o Not like toodo coincidencia de patrones
**Descripción**: Compruebe que el valor de un campo en el evento Hola coincide con un patrón determinado.
Por ejemplo, compruebe que el resultado de hello devuelve platos de licencia que comience con una letra y terminar por 9.

**Entrada**:

| Asegúrese | LicensePlate | Hora |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Salida**:

| Asegúrese | LicensePlate | Hora |
| --- | --- | --- |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Solución**:

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**Explicación**: Hola de uso **como** Hola de instrucción toocheck **LicensePlate** valor del campo. Debe comenzar con una A, seguida de cualquier cadena de ceros o más caracteres y terminar en nueve. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>Ejemplo de consulta: especificación de la lógica para los distintos casos/valores (instrucciones CASE)
**Descripción**: proporcione un cálculo diferente para un campo en función de un criterio concreto.
Por ejemplo, proporcione una descripción de cadena para automóviles cuántos de hello igual que pasan, con un caso especial de 1.

**Entrada**:

| Asegúrese | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Salida**:

| CarsPassed | Hora |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:00:10.0000000Z |
| 2 Toyotas |2015-01-01T00:00:10.0000000Z |

**Solución**:

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Explicación**: Hola **caso** cláusula nos permite tooprovide un cálculo diferentes, en función de algunos criterios (en nuestro caso, el recuento de Hola de automóviles hello en la ventana agregado de hello).

## <a name="query-example-send-data-toomultiple-outputs"></a>Ejemplo de consulta: enviar datos toomultiple genera
**Descripción**: enviar datos toomultiple destinos desde un único trabajo de salida.
Por ejemplo, analizar los datos de una alerta basadas en umbrales y todos los eventos tooblob almacenamiento de archivo.

**Entrada**:

| Asegúrese | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Salida1**:

| Asegúrese | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Salida2**:

| Asegúrese | Hora | Recuento |
| --- | --- | --- |
| Toyota |2015-01-01T00:00:10.0000000Z |3 |

**Solución**:

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**Explicación**: Hola **INTO** cláusula indica el análisis de transmisiones que de hello genera toowrite Hola datos toofrom esta instrucción.
Hola primera consulta es un acceso directo de datos de saludo se recibió una salida tooan que se denomina **ArchiveOutput**.
segunda consulta de Hello realiza algunas agregaciones simples y filtrado y lo envía resultados hello tooa sistema de alertas siguen en la cadena.

Tenga en cuenta que también puede reutilizar los resultados de Hola de expresiones de tabla común (CTE) de hello (como **WITH** instrucciones) en varias instrucciones de salida. Esta opción se Hola ventaja adicional de abrir el origen de entrada de toohello de lectores menos.
Por ejemplo: 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>Ejemplo de consulta: recuento de valores únicos
**Descripción**: contar Hola número único de valores de campo que aparecen en la secuencia de hello dentro de un período de tiempo.
Por ejemplo, ¿cuántos único hace que sea de automóviles que se pasan a través de la cabina de peaje hello en una ventana de 2 segundos?

**Entrada**:

| Asegúrese | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Salida:**

| Recuento | Hora |
| --- | --- |
| 2 |2015-01-01T00:00:02.000Z |
| 1 |2015-01-01T00:00:04.000Z |

**Solución:**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**Explicación:**
**COUNT (DISTINCT hacer)** devuelve Hola número de valores distintos en hello **realizar** columna dentro de un período de tiempo.

## <a name="query-example-determine-if-a-value-has-changed"></a>Ejemplo de consulta: determinar si un valor ha cambiado
**Descripción**: examine un toodetermine valor anterior si es diferente del valor actual de Hola.
¿Por ejemplo, está automóvil anterior hello en Hola Hola de carreteras de peaje que misma marca como car actual Hola?

**Entrada**:

| Asegúrese | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Salida**:

| Asegúrese | Hora |
| --- | --- |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Solución**:

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**Explicación**: Use **LAG** toopeek en hello secuencia un evento nuevo de entrada y obtener hello **realizar** valor. A continuación, compárela toohello **realizar** el valor en hello actual y evento salida Hola si son diferentes.

## <a name="query-example-find-hello-first-event-in-a-window"></a>Ejemplo de consulta: primer evento de Hola de búsqueda en una ventana
**Descripción**: primer coche de Hola de búsqueda en cada intervalo de 10 minutos.

**Entrada**:

| LicensePlate | Asegúrese | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Salida**:

| LicensePlate | Asegúrese | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |

**Solución**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

Ahora vamos a hacer el cambio Hola problema y buscar Hola primer coche de una determinada en cada intervalo de 10 minutos.

| LicensePlate | Asegúrese | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Solución**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>Ejemplo de consulta: último evento de Hola de búsqueda en una ventana
**Descripción**: último automóvil de Hola de búsqueda en cada intervalo de 10 minutos.

**Entrada**:

| LicensePlate | Asegúrese | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Salida**:

| LicensePlate | Asegúrese | Hora |
| --- | --- | --- |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Solución**:

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**Explicación**: hay dos pasos en la consulta de Hola. Hola primera busca una hello más reciente marca de tiempo en las ventanas de 10 minutos. las combinaciones de Hello segundo paso Hola resultados de Hola la primera consulta con hello original flujo toofind Hola eventos que coinciden con marcas de tiempo último hello en cada ventana. 

## <a name="query-example-detect-hello-absence-of-events"></a>Ejemplo de consulta: detectar Hola ausencia de eventos
**Descripción**: compruebe que un flujo no tiene ningún valor que cumpla un criterio determinado.
¿Por ejemplo, han 2 automóviles consecutivas de la misma marca de hello escrito carreteras de peaje hello en hello últimos 90 segundos?

**Entrada**:

| Asegúrese | LicensePlate | Hora |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Honda |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Toyota |DEF-987 |2015-01-01T00:00:03.0000000Z |
| Honda |GHI-345 |2015-01-01T00:00:04.0000000Z |

**Salida**:

| Asegúrese | Hora | CurrentCarLicensePlate | FirstCarLicensePlate | FirstCarTime |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:00:02.0000000Z |AAA-999 |ABC-123 |2015-01-01T00:00:01.0000000Z |

**Solución**:

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**Explicación**: Use **LAG** toopeek en hello secuencia un evento nuevo de entrada y obtener hello **realizar** valor. Comparar toohello **realizar** valor en el evento actual hello y, a continuación, evento de Hola de salida si están Hola igual. También puede usar **LAG** tooget datos acerca de automóvil anterior Hola.

## <a name="query-example-detect-hello-duration-between-events"></a>Ejemplo de consulta: detectar Hola duración del intervalo entre eventos
**Descripción**: buscar duración Hola de un evento determinado. Por ejemplo, dada una secuencia de clics de web, determine tiempo de hello invertido en una característica.

**Entrada**:  

| Usuario | Característica | Evento | Hora |
| --- | --- | --- | --- |
| user@location.com |RightMenu |Iniciar |2015-01-01T00:00:01.0000000Z |
| user@location.com |RightMenu |End |2015-01-01T00:00:08.0000000Z |

**Salida**:  

| Usuario | Característica | Duración |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**Solución**:

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**Explicación**: Hola de uso **última** función hello tooretrieve última **tiempo** valor al tipo de evento de hello era **iniciar**. Hola **última** función utiliza **PARTITION BY [user]** tooindicate que Hola resultado se calcula por usuario único. consulta de Hello tiene un umbral máximo de 1 hora de diferencia de tiempo de hello entre **iniciar** y **detener** eventos, pero se puede configurar según sea necesario **(límite DURATION(hour, 1)**.

## <a name="query-example-detect-hello-duration-of-a-condition"></a>Ejemplo de consulta: detectar una condición de tiempo que dure Hola
**Descripción**: averigüe la duración de una condición.
Por ejemplo, supongamos que, por error, todos los vehículos tienen un peso incorrecto (por encima de 20 000 libras). Queremos que la duración de hello toocompute de los errores de Hola.

**Entrada**:

| Asegúrese | Hora | Peso |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |2000 |
| Toyota |2015-01-01T00:00:02.0000000Z |25000 |
| Honda |2015-01-01T00:00:03.0000000Z |26000 |
| Toyota |2015-01-01T00:00:04.0000000Z |25000 |
| Honda |2015-01-01T00:00:05.0000000Z |26000 |
| Toyota |2015-01-01T00:00:06.0000000Z |25000 |
| Honda |2015-01-01T00:00:07.0000000Z |26000 |
| Toyota |2015-01-01T00:00:08.0000000Z |2000 |

**Salida**:

| StartFault | EndFault |
| --- | --- |
| 2015-01-01T00:00:02.000Z |2015-01-01T00:00:07.000Z |

**Solución**:

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**Explicación**: Use **LAG** instancias de flujo de entrada de hello tooview durante 24 horas y buscar dónde **StartFault** y **StopFault** se extienden por hello peso < 20000.

## <a name="query-example-fill-missing-values"></a>Ejemplo de consulta: rellenar los valores que faltan
**Descripción**: para el flujo de Hola de eventos que tienen valores que faltan, generar un flujo de eventos con intervalos regulares.
Por ejemplo, generar un evento cada 5 segundos que indica el punto de datos de hello visto más recientemente.

**Entrada**:

| t | value |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:01:05" |2 |
| "2014-01-01T06:01:10" |3 |
| "2014-01-01T06:01:15" |4 |
| "2014-01-01T06:01:30" |5 |
| "2014-01-01T06:01:35" |6 |

**Salida (10 primeras filas)**:

| windowend | lastevent.t | lastevent.value |
| --- | --- | --- |
| 2014-01-01T14:01:00.000Z |2014-01-01T14:01:00.000Z |1 |
| 2014-01-01T14:01:05.000Z |2014-01-01T14:01:05.000Z |2 |
| 2014-01-01T14:01:10.000Z |2014-01-01T14:01:10.000Z |3 |
| 2014-01-01T14:01:15.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:20.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:25.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:30.000Z |2014-01-01T14:01:30.000Z |5 |
| 2014-01-01T14:01:35.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:40.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:45.000Z |2014-01-01T14:01:35.000Z |6 |

**Solución**:

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**Explicación**: esta consulta genera eventos de cada 5 segundos y salidas Hola último evento que se recibió anteriormente. Hola [Hopping ventana](https://msdn.microsoft.com/library/dn835041.aspx "Hopping ventana: análisis de transmisiones de Azure") duración determina hasta qué punto Hola atrás consulta presenta un aspecto toofind evento más reciente de hello (300 segundos en este ejemplo).

## <a name="get-help"></a>Obtener ayuda
Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

