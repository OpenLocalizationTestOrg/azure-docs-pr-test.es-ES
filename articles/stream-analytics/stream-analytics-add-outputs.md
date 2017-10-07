---
title: "aaaHow tooconfigure datos salidas para trabajos de análisis de transmisiones | Documentos de Microsoft"
description: "Configuración de salidas de datos para trabajos de Análisis de transmisiones | segmento de ruta de aprendizaje."
keywords: salida de datos, movimiento de datos
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>¿Cómo tooconfigure datos salidas para trabajos de análisis de transmisiones

Trabajos de análisis de transmisiones de Azure pueden ser tooone conectado o más salidas de datos, que definen un receptor de datos de conexión tooan existente. Como el trabajo de análisis de transmisiones procesa y transforma los datos entrantes, una secuencia de eventos de salida de datos se escribe la salida del trabajo tooyour.

Salidas de flujo de datos de análisis pueden ser paneles en tiempo real de toosource usado o alertas, flujos de trabajo de movimiento de datos de desencadenador o simplemente archivar datos de procesamiento por lotes más adelante. El Análisis de transmisiones tiene una integración de primera clase con varios servicios de Azure, que se documentan aquí con detalle.

un trabajo de análisis de transmisiones de salida tooyour tooadd:

1. Hola [portal de Azure](https://portal.azure.com), abra el trabajo y haga clic en **salidas** y, a continuación, haga clic en **agregar** en la hoja de salidas de Hola que aparece.
   
    ![Agregar salidas](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Proporcione un nombre descriptivo para esta salida de hello **Alias de salida** cuadro. Este nombre se puede utilizar en consultas de la tarea más adelante en la salida de toohello de toorefer.  
   
    Rellene el resto de Hola de hello requerido conexión propiedades tooconnect tooyour salida.  Estos campos varían según el tipo de salida y se definen en detalle aquí.  
   
    ![Elección del tipo de movimiento de datos](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. Según el tipo de salida de hello, puede que necesite toospecify cómo Hola se serializa o con formato. configuración de serialización específico de Hola para cada tipo de salida se documenta aquí.
   
    Rellene el resto de Hola Hola conexión necesaria propiedades tooconnect tooyour del origen de datos. Estos campos varían según el tipo de entrada y origen y se definen en detalle en hello [artículo Crear trabajo](stream-analytics-create-a-job.md).  

> [!Note]
>
> Cualquier trabajo toohello agregada del elemento de salida, debe existir antes de inicia el trabajo de Hola y eventos de inicio del flujo. Por ejemplo, si utiliza almacenamiento de blobs como salida, el trabajo de hello no creará una cuenta de almacenamiento automáticamente. Debe toobe creada por el usuario de hello antes de iniciarse el trabajo de hello ASA.
> 
 

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

