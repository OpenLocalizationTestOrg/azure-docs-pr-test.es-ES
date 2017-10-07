---
title: "funciones de la ventana de análisis de aaaIntroduction tooStream | Documentos de Microsoft"
description: "Obtenga información acerca de tres funciones de ventana hello en análisis de transmisiones (saltos de tamaño constante, de salto, deslizante)."
keywords: "ventana de saltos de tamaño constante, ventana deslizante, ventana de salto"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Funciones de la ventana de análisis de introducción tooStream
En escenarios de transmisión por secuencias en tiempo real muchos, es operaciones tooperform necesarios solo en datos de hello incluidos en windows temporal. Compatibilidad nativa con funciones basadas en ventanas es una característica clave de análisis de transmisiones de Azure que mueve aguja hello en la productividad del desarrollador en la creación de trabajos de procesamiento de flujo complejos. Análisis de transmisiones permite a los desarrolladores toouse [ **saltos de tamaño constante**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) y [ **deslizante** ](https://msdn.microsoft.com/library/dn835051.aspx) operaciones de tiempo de tooperform de windows en la transmisión de datos. Merece la pena mencionar que todos los [ventana](https://msdn.microsoft.com/library/dn835019.aspx) resultados de las operaciones en hello **final** de ventana hello. resultado de Hello de ventana hello será evento único basado en función de agregado de hello usada. evento de Hello tendrá marca de tiempo de Hola de final de Hola de ventana hello y todas las funciones de ventana se definen con una longitud fija. Por último resulta importante toonote que todas las funciones de ventana deben usarse en un [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) cláusula.

![Conceptos de las funciones de ventana de Análisis de transmisiones](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>Ventana de saltos de tamaño constante
Funciones de la ventana de saltos de tamaño constante son toosegment usado en un flujo de datos en segmentos de tiempo distintos y realizan una función con ellos, como ejemplo de Hola siguiente. qu Hola de una ventana de saltos de tamaño constante es que repita, no se superponen y un evento no puede pertenecer toomore que una ventana de saltos de tamaño constante.

![Introducción al salto de tamaño constante de las funciones de ventana de Análisis de transmisiones](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>Ventana de salto
Las funciones de ventana de salto saltan hacia adelante en el tiempo un período fijo. Puede ser fácil toothink de ellos como ventanas de saltos de tamaño constante que se pueden superponer, por lo que los eventos pueden pertenecer toomore que un conjunto de resultados de la ventana Hopping. Hola toomake una ventana Hopping mismo como una ventana de saltos de tamaño constante simplemente uno especificaría toobe de tamaño de salto de Hola Hola mismo como el tamaño de la ventana de Hola. 

![Introducción al salto de las funciones de ventana de Análisis de transmisiones](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>Ventana deslizante
Las funciones de ventana deslizante, a diferencia de las ventanas de saltos de tamaño constante o de salto, producen una salida **solo** cuando se produce un evento. Cada ventana tendrá al menos un evento y ventana hello continuamente avanza por una € (epsilon). Al igual que las ventanas de salto, eventos pueden pertenecer toomore que una ventana deslizante.

![Introducción al deslizamiento de las funciones de ventana de Análisis de transmisiones](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Obtener ayuda con las funciones de ventana
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

