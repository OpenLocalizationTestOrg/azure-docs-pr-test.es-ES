---
title: "toostart aaaHow los trabajos de análisis de transmisiones de streaming | Documentos de Microsoft"
description: "Ejecución de un trabajo de streaming en Análisis de transmisiones de Azure | segmento de ruta de acceso de aprendizaje."
keywords: Trabajos de streaming
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>¿Cómo toorun una transmisión por secuencias de trabajo de análisis de transmisiones de Azure
Cuando un trabajo de entrada, consulta y resultado todas se han especificado que puede iniciar trabajo de análisis de transmisiones de Hola.

toostart el trabajo:

1. En el portal de Azure clásico de hello, en el panel de trabajo de hello, haga clic en **iniciar** final Hola de página Hola.
   
   ![Botón Iniciar trabajo](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   Hola portal de Azure, haga clic en **iniciar** al principio de hello de la página de trabajo.
   
   ![Botón Iniciar trabajo de Azure Portal](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Especifique un **iniciar salida** valor toodetermine al trabajo comenzará a producir un resultado. Hello configuración predeterminada para los trabajos que no se ha iniciado previamente es **hora de inicio del trabajo**, lo que significa que el trabajo de hello inmediatamente comenzará a procesar los datos. También puede especificar un **personalizado** tiempo Hola pasado (para consumir datos históricos) o hello futura (toodelay procesamiento hasta una fecha futura). Para casos en que se ha iniciado y detenido, previamente un trabajo Hola opción **última hora de detención** está disponible en el trabajo de hello tooresume de orden de última hora de salida de hello y evitar la pérdida de datos.  
   
   ![Hora de inicio del trabajo de streaming](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Hora de inicio del trabajo de streaming de Azure Portal](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Confirme la selección. estado del trabajo Hola cambiará demasiado*iniciando* y en breve se moverán demasiado*ejecutando* una vez que ha iniciado el trabajo de Hola. Puede supervisar el progreso de Hola de hello **iniciar** operación Hola **centro de notificaciones**:
   
   ![progreso del trabajo de streaming](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Progreso del trabajo de streaming de Azure Portal](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

