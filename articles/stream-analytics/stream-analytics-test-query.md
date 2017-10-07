---
title: "la prueba de consultas de análisis de transmisiones de aaaAzure | Documentos de Microsoft"
description: "¿Cómo tootest las consultas en los trabajos de análisis de transmisiones."
keywords: "probar consulta, consulta de solución de problemas"
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a>Probar las consultas de análisis de transmisiones de Azure en hello portal de Azure

Con el análisis de transmisiones de Azure, puede probar las consultas en hello portal de Azure sin necesidad de toostart o detener un trabajo.

## <a name="test-hello-input"></a>Entrada de Hola de prueba

1. tootest con datos de entrada de ejemplo, haga clic en cualquiera de las entradas y, a continuación, seleccione **cargar datos de ejemplo de archivo**.

    ![consulta de prueba del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. Una vez finalizada la carga de hello, haga clic en **prueba** tootest esta consulta contra Hola muestreo de los datos que ha proporcionado.

    ![datos de prueba de ejemplo del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

salida de Hello de la consulta se muestra en el Explorador de hello, con el vínculo de descarga de resultados si quiere toosave salida de la prueba de Hola para su uso posterior. Ahora puede fácilmente y de forma iterativa modifique la consulta y probarlo repetidamente toosee cómo cambia la salida de hello.

![Salida de ejemplo del editor de consultas de Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

Con varias salidas usadas en una consulta, puede ver los resultados de Hola de ambas salidas por separado y alternar fácilmente entre ellos.

Cuando esté satisfecho con los resultados de Hola se muestra en el Explorador de hello, puede guardar la consulta, iniciar el trabajo y dejar que procesan los eventos sin errores.

## <a name="get-help"></a>Obtener ayuda

Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes

* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
