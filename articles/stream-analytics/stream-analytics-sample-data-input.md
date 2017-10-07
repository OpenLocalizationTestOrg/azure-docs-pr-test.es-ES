---
title: "entradas de muestreo AAA en análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Identifique los problemas cuando realice la solución de problemas de trabajos de Stream Analytics."
keywords: "entrada de solución de problemas, muestreo de entrada"
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
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Muestreo de flujo de entrada de Azure Stream Analytics

Mediante el análisis de transmisiones de Azure, puede muestrear eventos de entrada que proceden de un archivo y probar consultas en el portal de hello sin necesidad de toostart o detener un trabajo.

## <a name="testing-your-query"></a>Prueba de la consulta

En el panel de detalles de trabajo de análisis de transmisiones de hello, abra hello **editor de consultas** hoja haciendo clic en el nombre de la consulta de hello en **consulta**. (En nuestro escenario de ejemplo, porque no hay ninguna consulta se ha creado aún, haga clic en hello **< >** marcador de posición.)

![editor de consultas de análisis de transmisiones de Hola](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

hoja de editor enriquecido Hola para crear la consulta se muestra como ocurría en la versión anterior de Hola. Ahora se ha actualizado la hoja de hello con un nuevo panel izquierdo de esa muestra hello entradas y salidas que son utilizados por la consulta de Hola y definidas para este trabajo.

![editor de consultas de análisis de transmisiones de Hello entradas y salidas de listas](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

También se muestra una entrada o salida adicionales, que no se han definido. Provienen de la nueva plantilla de consulta de saludo inicial. Se cambia, o incluso desaparecen por completo, al crear o Editar consulta Hola. Puede ignorar estos errores con seguridad por ahora.

tootest con datos de entrada de ejemplo, haga clic en cualquiera de las entradas y, a continuación, seleccione **cargar datos de ejemplo de archivo**.

![Hola datos de ejemplo de carga en editor de consulta de análisis de transmisiones de archivo (comando)](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Una vez finalizada la carga de hello, haga clic en **prueba** tootest que acabas de proporcionar de datos de ejemplo de esta consulta contra Hola.

![botón de prueba de editor de consulta de análisis de transmisiones de Hola](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

Si desea generar resultados de pruebas de Hola de toosave para su uso posterior, salida de hello de la consulta se muestra en el Explorador de hello con resultados de la descarga de toohello de vínculo. Ahora puede fácilmente y de forma iterativa modifique la consulta y probarlo repetidamente toosee cómo cambia la salida de hello.

![Salida de ejemplo del editor de consultas de Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

Hola delante de la imagen, se ha agregado una segunda salida, denominado **HighAvgTempOutput**.

Cuando se usa varias salidas en una consulta, puede ver resultados de Hola para cada salida por separado y alternar fácilmente entre ellos.

Cuando esté satisfecho con los resultados de hello, puede guardar la consulta, iniciar el trabajo, póngase cómodo y ver magia Hola de análisis de transmisiones.

## <a name="get-help"></a>Obtener ayuda

Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
