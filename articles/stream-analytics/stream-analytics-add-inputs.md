---
title: "trabajos de análisis de transmisiones de tooyour de entrada de datos aaaAdd | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toohook seguridad un tooyour de origen de datos análisis de transmisiones de transmisión por secuencias como entrada de datos de los centros de eventos o datos de referencia desde el almacenamiento de blobs de trabajo."
keywords: entrada de datos, datos de streaming
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>Agregar una transmisión por secuencias datos de entrada o referencia datos tooa trabajo de Stream Analytics
Obtenga información acerca de cómo toohook seguridad un tooyour de origen de datos análisis de transmisiones de transmisión por secuencias como entrada de datos de los centros de eventos o datos de referencia desde el almacenamiento de blobs de trabajo.

Trabajos de análisis de transmisiones de Azure pueden ser de entrada de datos de tooone conectados o más, cada uno de los cuales define un origen de datos existente de conexión tooan. Como origen de datos de toothat enviar datos, es utilizado por el trabajo de análisis de transmisiones de Hola y procesan en tiempo real como la transmisión de datos. Análisis de transmisiones tiene la integración de primera clase con [centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/) y [almacenamiento de blobs de Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tanto dentro como fuera de suscripción del trabajo de Hola.

En este artículo es un paso en hello [ruta de acceso de aprendizaje de análisis de transmisiones](/documentation/learning-paths/stream-analytics/).

## <a name="data-input-streaming-data-and-reference-data"></a>Entrada de datos: datos de streaming y datos de referencia
Hay dos tipos distintos de entradas en Análisis de transmisiones: flujos de datos y datos de referencia.

* **Flujos de datos**: trabajos de análisis de transmisiones deben incluir al menos un datos flujo entrada toobe consumirá y transformará trabajo Hola. Almacenamiento de blobs de Azure y Centros de eventos de Azure se admiten como orígenes de entrada de flujos de datos. Centros de eventos de Azure son secuencias de eventos de toocollect usado desde dispositivos conectados, servicios y aplicaciones. El almacenamiento de blobs de Azure puede usarse como origen de entrada para la ingesta de datos en masa como secuencia.  
* **Datos de referencia**: Análisis de transmisiones admite un segundo tipo de entrada auxiliar denominada datos de referencia.  Como toodata opuesto en movimiento, estos datos son estáticos o lenta cambiar.  Se utiliza normalmente para realizar búsquedas y correlaciones con toocreate de flujos de datos un conjunto más completo de datos.  Almacenamiento de blobs de Azure está actualmente Hola solo admitido el origen de entrada de datos de referencia.  

un trabajo de análisis de transmisiones de entrada tooyour tooadd:

1. Hola portal de Azure, haga clic en **entradas** y, a continuación, haga clic en **agregar una entrada** en el trabajo de análisis de transmisiones.
   
    ![Portal de Azure clásico: agregar entrada.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    Hola portal de Azure, haga clic en hello **entradas** disponer en mosaico en el trabajo de análisis de transmisiones.  
   
    ![Portal de Azure: agregar entrada.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. Especificar tipo de Hola de entrada de hello: cualquier **flujo de datos** o **hacen referencia a datos**.
   
    ![Agregar datos correctos de Hola de entrada, modos de transmisión o hacer referencia a](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Agregar datos correctos de Hola de entrada, modos de transmisión o hacer referencia a](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. Si crea una entrada de flujo de datos, especifique el tipo de origen de hello para la entrada de Hola.  Este paso se omite durante la creación de Datos de referencia ya que, en este momento, solo se admite el almacenamiento de blobs.
   
    ![Adición de entrada de datos de flujo de datos](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Adición de entrada de datos de flujo de datos](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. Proporcione un nombre descriptivo para esta entrada en hello cuadro Alias de entrada.  Este nombre se usará en la consulta de la tarea más adelante en la entrada de toohello de toorefer.
   
    Rellene el resto de Hola Hola conexión necesaria propiedades tooconnect tooyour del origen de datos. Estos campos varían según el tipo de entrada y de origen y se definen en detalle [aquí](stream-analytics-create-a-job.md).  
   
    ![Adición de entrada de datos de Centro de eventos](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. Especifique la configuración de serialización de Hola para datos de entrada de hello:
   
   * toomake seguro de las consultas funcionan de forma Hola que espera, especifique hello **formato de serialización del evento** de los datos entrantes.  Los formatos de serialización compatibles son JSON, CSV y Avro.
   * Comprobar hello **codificación** para datos de Hola.  UTF-8 es Hola solo admite el formato de codificación en este momento.
     
     ![Configuración de serialización de datos de entrada de datos de Hola](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Configuración de serialización de datos de entrada de datos de Hola](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. Después de completar la creación de entrada de hello, análisis de transmisiones comprobará que se puede conectar el origen de entrada de toohello.  Puede ver el estado de Hola de hello operación de conexión de prueba en el centro de notificaciones de Hola.
   
    ![Probar conexión de hello transmisión de datos de entrada](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Probar conexión de hello transmisión de datos de entrada](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>Obtener ayuda con las entradas de datos de streaming
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

