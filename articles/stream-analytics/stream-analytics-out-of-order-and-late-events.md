---
title: "aaaHandling orden de eventos y tardanza con análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Aprenda cómo funciona Stream Analytics con eventos desordenados o atrasados en flujos de datos."
keywords: desordenados, atrasados, eventos
documentationcenter: 
services: stream-analytics
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Control del orden de los eventos de Azure Stream Analytics

En un flujo de datos temporales de eventos, se registra cada evento con hora Hola se recibe ese evento Hola. Algunas condiciones podrían producir secuencias de eventos de recepción toooccasionally algunos eventos en un orden diferente a la que se enviaron. Un simple TCP retransmitir, o incluso un sesgo de reloj entre Hola enviar hello recibir centro de eventos y dispositivos puede provocar este toooccur. Eventos de "Puntuación" también se agregan tooreceived secuencias de eventos, tiempo de hello tooadvance en ausencia de Hola de llegadas de eventos. Estos son necesarios en escenarios como "Avisarme cuando no se produzca ningún inicio de sesión durante 3 minutos".

Los flujos de entrada que no están en orden:
* Se ordenan (y, por tanto, se **retrasan**).
* Ajustar sistema hello, según la directiva de tooa especificado por el usuario.


## <a name="lateness-tolerance"></a>Tolerancia a la tardanza
Stream Analytics tolera estos tipos de escenarios. Stream Analytics tiene control de eventos "desordenados" y "atrasados". Controla estos eventos en hello siguientes maneras:

* Los eventos que llegan sin orden pero dentro de hello establecer tolerancia son **ordenar por marca de tiempo**.
* Los eventos que llegan más tarde que la tolerancia se **descartan o ajustan**.
    * **Ajustar**: toohave tooappear ajustada llegó a hello más reciente tiempo aceptable.
    * **Descartados**: los eventos descartados.

![Control de eventos de Stream Analytics](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>Reducir el número de Hola de eventos de fuera de servicio

Como Stream Analytics aplica una transformación temporal cuando procesa los eventos entrantes (por ejemplo, para agregados en ventana o uniones temporales), Stream Analytics ordena los eventos entrantes por orden de marca de tiempo.

Cuando es la palabra clave "timestamp por" hello **no** utiliza, hora de poner en cola de evento de hello centros de eventos de Azure se utiliza de forma predeterminada. Los concentradores de eventos garantiza monotonicity de marca de tiempo de hello en cada partición del concentrador de eventos de Hola. También garantiza que eventos de todas las particiones se combinan en orden de marca de tiempo. Estas dos garantías de Event Hubs aseguran que no hay eventos desordenados.

A veces, es importante para la marca de tiempo se toouse Hola del remitente. En ese caso, se elige una marca de tiempo de carga del evento hello mediante el uso de "marca de tiempo por". En estos escenarios, se podrían introducir uno o más orígenes de desórdenes de eventos:

* Los productores de eventos tienen sesgos de reloj. Esto es común cuando los productores provienen de equipos diferentes, por lo que tienen relojes diferentes.
* Hay un retraso de red de origen Hola de concentrador de eventos de destino de hello eventos toohello.
* Existen sesgos de reloj entre particiones de centro de eventos. Stream Analytics ordena primero los eventos de todas las particiones del centro de eventos por tiempo de puesta en cola del evento. A continuación, examina flujo de datos hello misordered eventos.

En la ficha de configuración de hello, vea Hola después de los valores predeterminados:

![Control de desorden de Stream Analytics](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Si usa 0 segundos como período de tolerancia de fuera de servicio de hello, que está validando que todos los eventos están en orden todo tiempo Hola. Dados los orígenes de hello tres de los eventos misordered, es probable que esto es cierto. 

toocorrect de análisis de transmisiones de tooallow misorder de un evento, puede especificar un período de tolerancia de fuera de servicio distinto de cero. Eventos de búferes de análisis de flujo toothat ventana y, a continuación, pedidos repetidos que ellos mediante Hola marca de tiempo que eligió. A continuación, aplica la transformación temporal de Hola. Puede comenzar con una ventana de 3 segundos y número de Hola Hola valor tooreduce de eventos que se ajusta a la hora de optimizar. 

Un efecto secundario de almacenamiento en búfer de hello es que el resultado de hello es **demoró Hola mismo período de tiempo**. Puede ajustar el número de Hola Hola valor tooreduce de eventos fuera de servicio y mantener baja latencia de trabajo de Hola.

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooStream análisis](stream-analytics-introduction.md)
* [Introducción a Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalado de trabajos de Stream Analytics](stream-analytics-scale-jobs.md)
* [Referencia de lenguaje de consulta de Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)