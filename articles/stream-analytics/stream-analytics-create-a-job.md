---
title: "aaaHow toocreate un trabajo de procesamiento de análisis de datos para análisis de transmisiones | Documentos de Microsoft"
description: "Creación de un trabajo de procesamiento de análisis de datos para Análisis de transmisiones | segmento de ruta de aprendizaje."
keywords: "procesamiento de análisis de datos"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>¿Cómo toocreate trabajo de un procesamiento de análisis de datos para análisis de transmisiones
recurso de nivel superior de Hello en análisis de transmisiones de Azure es un trabajo de análisis de transmisiones.  Consta de uno o más orígenes de datos, una consulta de expresar la transformación de datos de Hola y uno o varios destinos de salida que se escriben los resultados en de la entrada. Conjuntamente estas instrucciones permiten analizar los datos Hola usuarios tooperform escenarios de procesamiento de datos de transmisión por secuencias.

toostart mediante el análisis de transmisiones, empiece por crear un nuevo trabajo de análisis de transmisiones.  Tenga en cuenta que esta acción no tendrá ningún implicaciones de facturación hasta que se inicie el trabajo de Hola.

1. Inicie sesión en hello en línea [portal de Azure clásico](http://manage.windowsazure.com) o hello [portal de Azure](https://portal.azure.com/).
2. En el portal de hello: **haga clic en nuevo**, a continuación, haga clic en **Data Services** o **análisis de datos** según el portal y, a continuación, haga clic en **análisis de transmisiones de Azure** o **transmitir análisis** y, a continuación, **creación rápida**.
   
   ![Asistente para trabajos de procesamiento de análisis de datos](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Creación de un trabajo de procesamiento de análisis de datos](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Especificar configuración deseada de hello para el trabajo de análisis de transmisiones de Hola.
   
   * Hola **nombre del trabajo** cuadro, escriba un trabajo de análisis de transmisiones de nombre tooidentify Hola. Cuando Hola **nombre del trabajo** se valida, aparece una marca de verificación verde en el cuadro Nombre del trabajo de Hola. Hola **nombre del trabajo** solo pueden contener caracteres alfanuméricos y hello '-' caracteres y debe tener entre 3 y 63 caracteres.
   * Use **región** Hola portal de Azure o **ubicación** en hello Azure portal toospecify Hola ubicación geográfica donde desea que el trabajo de hello toorun.
   * Si utiliza hello portal de Azure, seleccione o cree una toouse de cuenta de almacenamiento como hello **cuenta de almacenamiento de supervisión Regional**. Esta cuenta de almacenamiento es toostore usa datos de supervisión de todos los trabajos de análisis de transmisiones que se ejecutan en esta región.
   * Si utiliza hello portal de Azure, especifique un nuevo o existente **grupo de recursos** toohold relacionados con recursos para la aplicación.
4. Después de configuran nuevas opciones de trabajo de análisis de transmisiones hello, haga clic en **crear trabajo de Stream Analytics**. Puede tardar unos minutos para toobe de trabajo de análisis de transmisiones de hello creado. estado de hello toocheck, puede supervisar el progreso de hello en Centro de notificaciones de Hola.
   
   ![Centro de notificaciones del trabajo de procesamiento de análisis de datos](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Trabajo de procesamiento de análisis de datos en Azure Portal: creación del trabajo](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. nuevo trabajo de Hola mostrará el estado de **creado**. Tenga en cuenta que hello **iniciar** botón está deshabilitado. Configurar entrada de trabajo de hello, consulta y salida antes de iniciar el trabajo de Hola.
   
   ![Trabajo de procesamiento de análisis de datos: estado del trabajo](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Trabajo de procesamiento de análisis de datos en Azure Portal: estado del trabajo](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

