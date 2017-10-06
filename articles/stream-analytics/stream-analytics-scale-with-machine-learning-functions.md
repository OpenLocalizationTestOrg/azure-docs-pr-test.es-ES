---
title: "aaaJob escalado con funciones de análisis de transmisiones de Azure y aprendizaje automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooproperly según la escala de trabajos de análisis de transmisiones (creación de particiones, SU cantidad y más) cuando se utilizan funciones de aprendizaje automático de Azure."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Escalado del trabajo de Análisis de transmisiones con funciones de Aprendizaje automático de Azure
A menudo es bastante fácil tooset un trabajo de análisis de transmisiones y ejecutar algunos datos de ejemplo a través de él. ¿Qué se debe hacer cuando necesitemos toorun Hola mismo trabajo con el mayor volumen de datos? Requiere que nos toounderstand cómo tooconfigure Hola análisis de transmisiones de trabajo para que se escalará. En este documento, nos centraremos en aspectos especiales de Hola de análisis de transmisiones de escalado trabajos con funciones de aprendizaje automático. Para obtener información sobre cómo tooscale trabajos de análisis de transmisiones, en general, vea el artículo de hello [escalado de trabajos](stream-analytics-scale-jobs.md).

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>¿Qué es una función de Aprendizaje automático de Azure en Análisis de transmisiones?
Una función de aprendizaje automático en análisis de transmisiones puede utilizarse como una llamada de función normal en lenguaje de consulta de análisis de transmisiones de Hola. Sin embargo, detrás de la escena hello, llamadas a funciones hello son realmente las solicitudes de servicio de Web de aprendizaje de máquina de Azure. Compatibilidad con "el procesamiento por lotes" varias filas, que se llama lote mínima de servicios web de aprendizaje de máquina, Hola mismo web llamada API del servicio, tooimprove el rendimiento global. Vea Hola siguientes artículos para obtener más detalles; [Funciones de aprendizaje automático de azure en análisis de transmisiones](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) y [servicios Web de Azure Machine Learning](../machine-learning/machine-learning-consume-web-services.md).

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Configuración de un trabajo de Análisis de transmisiones con funciones de Aprendizaje automático
Al configurar una función de aprendizaje automático para el trabajo de análisis de transmisiones, hay dos parámetros tooconsider, tamaño de lote de Hola de llamadas de función de aprendizaje automático de Hola y Hola unidades (SUs) aprovisionados para el trabajo de análisis de transmisiones de Hola de streaming. toodetermine Hola los valores adecuados para ello, en primer lugar una decisión debe realizarse entre latencia y rendimiento, es decir, latencia de trabajo de análisis de transmisiones de Hola y el rendimiento de cada SU. SUs siempre se pueden agregar tooa el rendimiento de tooincrease de trabajo de una consulta de análisis de transmisiones bien dividido en particiones, aunque SUs adicionales aumenta el costo de Hola de trabajo en ejecución Hola.

Por lo tanto, es importante toodetermine hello *tolerancia* de latencia en la ejecución de un trabajo de análisis de transmisiones. Naturalmente aumentará la latencia adicional de solicitudes de servicio de aprendizaje automático de Azure en ejecución con el tamaño del lote, que intensificarán latencia Hola de trabajo de análisis de transmisiones de Hola. Hola otra parte, si aumenta el tamaño de lote permite tooprocess de trabajo de análisis de transmisiones de Hola * más eventos con hello *tantos* de aprendizaje automático de solicitudes de servicio web. A menudo el Hola aumento de latencia de aprendizaje automático de servicio web es toohello Sub-lineal aumento del tamaño de lote por lo que es importante tooconsider hello más rentable tamaño de lote para un servicio web de aprendizaje automático en cualquier situación determinada. tamaño de lote de Hello predeterminado para el servicio web de hello solicita es 1000 y puede modificarse mediante el uso de hello [API de REST de análisis de transmisiones](https://msdn.microsoft.com/library/mt653706.aspx "API de REST de análisis de transmisiones") o hello [cliente de PowerShell para el análisis de transmisiones](stream-analytics-monitor-and-manage-jobs-use-powershell.md "cliente de PowerShell para el análisis de transmisiones").

Una vez que se ha determinado un tamaño de lote, Hola cantidad de transmisión por secuencias unidades (SUs) pueden ser determinados, en función de número de Hola de eventos que la función hello necesita tooprocess por segundo. Para más información sobre el ajuste de las unidades de streaming, consulte [Escalación de trabajos de Stream Analytics](stream-analytics-scale-jobs.md).

En general, hay 20 conexiones simultáneas toohello servicio de web de aprendizaje automático para cada 6 SUs, salvo que los trabajos de SU 1 y 3 SU obtendrá 20 conexiones simultáneas también.  Por ejemplo, si es de velocidad de datos de entrada de Hola 200.000 eventos por segundo y se deja el tamaño del lote de hello toohello predeterminado de latencia de servicio web resultante de 1000 de hello con lotes de 1000 eventos mínima es de 200 milisegundos. Esto significa que cada conexión puede realizar servicio web de aprendizaje automático de toohello de 5 solicitudes en un segundo. Con 20 conexiones, trabajo de análisis de transmisiones de hello puede procesar 20.000 eventos en 200ms y, por tanto, de 100.000 eventos en un segundo. ¿Tooprocess 200.000 eventos por segundo, trabajo de análisis de transmisiones de Hola que necesita 40 conexiones simultáneas, que se reciben SUs too12. Hola diagrama siguiente muestra las solicitudes de Hola de extremo de servicio web de hello análisis de transmisiones trabajo toohello aprendizaje automático: cada SUs de 6 tiene servicio de web de aprendizaje de tooMachine de 20 conexiones simultáneas como máximo.

![Ejemplo de escalado de trabajo de Stream Analytics con funciones de Machine Learning 2](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "Ejemplo de escalado de trabajo de Stream Analytics con funciones de Machine Learning 2")

En general, ***B*** para el tamaño de lote, ***L*** de latencia de servicio de web hello en el tamaño del lote B en milisegundos, Hola el rendimiento de un trabajo de análisis de transmisiones con ***N*** SUs es:

![Fórmula de escalado de Stream Analytics con funciones de Machine Learning](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "Fórmula de escalado de Stream Analytics con funciones de Machine Learning")

Una consideración adicional puede ser hello 'máximo de llamadas concurrentes' en hello lado de servicio web de aprendizaje automático, se recomienda tooset este valor máximo de toohello (200 actualmente).

Para obtener más información sobre esta configuración, consulte hello [artículo de ajuste de escala para servicios Web de aprendizaje de máquina](../machine-learning/machine-learning-scaling-webservice.md).

## <a name="example--sentiment-analysis"></a>Ejemplo: Análisis de opiniones
Hello en el ejemplo siguiente se incluye un trabajo de análisis de transmisiones con análisis de opiniones Hola función de aprendizaje automático, como se describe en hello [tutorial de integración de aprendizaje automático de análisis de transmisiones](stream-analytics-machine-learning-integration-tutorial.md).

Hello consulta es una consulta de totalmente con particiones simple seguida de hello **opiniones** funcione, tal y como se muestra a continuación:

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Considere la posibilidad de hello siguiendo escenario; con un rendimiento de 10.000 tweets por segundo un trabajo de análisis de transmisiones debe crearse tooperform análisis de opiniones de tweets de hello (eventos). ¿Con 1 SU, este trabajo de análisis de transmisiones pudo toohandle capaz de tráfico de hello? Usando tamaño predeterminado del lote Hola de trabajo de hello 1000 debe ser tookeep capaz de seguridad con la Ayuda de Hola. Hola más agrega la función de aprendizaje automático debe generar más de un segundo de latencia, que es la latencia de predeterminado general Hola de análisis de opiniones Hola servicio web de aprendizaje automático (con un tamaño de lote de predeterminado de 1000). del trabajo de análisis de transmisiones de Hello **general** o latencia to-end normalmente sería de unos segundos. Eche un vistazo más detallado en este trabajo de análisis de transmisiones, *especialmente* Hola llamadas de función de aprendizaje automático. Con el tamaño del lote de Hola de 1000, un rendimiento de 10.000 eventos tardará unos 10 solicitudes tooweb servicio. Incluso con 1 SU, no hay suficientes conexiones simultáneas tooaccommodate este tráfico de entrada.

Pero ¿qué ocurre si aumenta la velocidad de los eventos de entrada Hola x 100 y ahora el trabajo de análisis de transmisiones de hello necesita tooprocess 1.000.000 tweets por segundo? Hay dos opciones:

1. Aumentar el tamaño del lote de hello, o
2. Tooprocess de flujo de entrada de partición Hola Hola eventos en paralelo

Con la primera opción hello, Hola trabajo **latencia** aumentará.

Con la segunda opción hello, SUs más se necesita toobe aprovisionar y, por tanto, genere simultáneas más solicitudes de servicio web de aprendizaje automático. Esto significa que el trabajo de hello **costo** aumentará.

Suponga latencia Hola de análisis de opiniones Hola servicio web de aprendizaje automático es de 200 milisegundos para lotes de 1000 eventos o por debajo, 250ms en lotes de 5.000-event, 300 ms de lotes de 10.000 eventos o 500 ms para lotes de 25.000-event.

1. Con la primera opción hello, (**no** SUs más de aprovisionamiento), podría aumentar el tamaño del lote de hello demasiado**25.000**. Esto a su vez le permitiría Hola trabajo tooprocess 1.000.000 eventos con 20 conexiones simultáneas toohello servicio web de aprendizaje automático (con una latencia de 500 ms por llamada). Por lo tanto Hola latencia adicional de trabajo de análisis de transmisiones de hello debido a las solicitudes de función de toohello opiniones contra Hola aprendizaje automático de solicitudes de servicio web se aumentará de **200ms** demasiado**500 ms**. Sin embargo, tenga en cuenta que el tamaño por lotes **no** aumentarse infinitamente como servicios web de aprendizaje automático de hello requieren Hola de tamaño de carga de una solicitud de 4 MB o web menor tiempo de espera de las solicitudes de servicio después de 100 segundos de la operación.
2. Con la segunda opción de hello, el tamaño del lote de Hola se deja como 1000, con una latencia de servicio web 200ms, todos los servicios web toohello 20 conexiones simultáneas sería capaz de tooprocess 1000 * 20 * 5 eventos = 100.000 por segundo. Por lo que tooprocess 1.000.000 eventos por segundo, trabajo Hola necesitaría 60 SUs. Primera opción toohello comparados, análisis de flujo de trabajo podría hacer más web las solicitudes de servicio por lotes, a su vez generando un aumento del costo.

A continuación se muestra una tabla para el rendimiento del trabajo de análisis de transmisiones de Hola Hola para SUs diferentes y tamaños de lote (en número de eventos por segundo).

| Tamaño del lote (latencia de Aprendizaje automático) | 500 (200 ms) | 1000 (200 ms) | 5000 (250 ms) | 10 000 (300 ms) | 25 000 (500 ms) |
| --- | --- | --- | --- | --- | --- |
| **1 unidad de búsqueda** |2500 |5.000 |20.000 |30 000 |50.000 |
| **3 unidades de búsqueda** |2500 |5.000 |20.000 |30 000 |50.000 |
| **6 unidades de búsqueda** |2500 |5.000 |20.000 |30 000 |50.000 |
| **12 unidades de búsqueda** |5.000 |10.000 |40.000 |60 000 |100 000 |
| **18 unidades de búsqueda** |7500 |15 000 |60 000 |90 000 |150 000 |
| **24 unidades de búsqueda** |10.000 |20.000 |80 000 |120 000 |200 000 |
| **…** |… |… |… |… |… |
| **60 unidades de búsqueda** |25 000 |50.000 |200 000 |300 000 |500.000 |

En este momento, ya debe saber cómo funcionan las funciones de Aprendizaje automático en Análisis de transmisiones. También es probable que entender que los trabajos de análisis de transmisiones "pull" datos de orígenes de datos y cada "pull" devuelven un lote de eventos de Hola tooprocess de trabajo de análisis de transmisiones. ¿Cómo afecta este modelo de extracción a solicitudes de servicio de web de aprendizaje automático de hello?

Normalmente, tamaño del lote Hola que establecemos para las funciones de aprendizaje automático exactamente no es divisible por número de Hola de eventos devueltos por cada trabajo de análisis de transmisiones "pull". Cuando esto ocurre Hola servicio web de aprendizaje automático se llamará con lotes "parciales". Esto se hace toonot producir una latencia de trabajos adicionales sobrecarga en los eventos de uso combinados de toopull de extracción.

## <a name="new-function-related-monitoring-metrics"></a>Nuevas métricas de supervisión relacionadas con la función
En el área del Monitor de un trabajo de análisis de transmisiones de hello, se han agregado tres métricas adicionales relacionadas con la función. Son las solicitudes de función, eventos de funciones y errores de solicitud de función, como se muestra en el gráfico de hello siguiente.

![Métricas de escalado de Stream Analytics con funciones de Machine Learning](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "Métricas de escalado de Stream Analytics con funciones de Machine Learning")

Hola se definen como sigue:

**Las solicitudes de la función**: Hola número de solicitudes de función.

**EVENTOS de funciones**: número de eventos de Hola Hola función solicitudes.

**ERRORES de solicitud de función**: Hola número de solicitudes de función con errores.

## <a name="key-takeaways"></a>Puntos clave
toosummarize puntos principales de hello, en orden tooscale un trabajo de análisis de transmisiones con funciones de aprendizaje automático, hello siguientes elementos deben tener en cuenta:

1. velocidad de los eventos de entrada Hola
2. Hola tolera latencia para ejecutar el trabajo de análisis de transmisiones de hello (y, por tanto, solicita el tamaño de lote de Hola de servicio web de aprendizaje automático de hello)
3. Hola aprovisionado SUs análisis de secuencia y el número de Hola de solicitudes de servicio web de aprendizaje automático (Hola relacionados con la función costes adicionales)

Como ejemplo se ha utilizado una consulta de Análisis de transmisiones totalmente particionada. Si se necesita una consulta más compleja hello [foro de análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) es un excelente recurso para obtener ayuda adicional en el equipo de análisis de transmisiones de Hola.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información sobre análisis de transmisiones, consulte:

* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
