---
title: "aaaVisualize y solucionar problemas de trabajos de análisis de transmisiones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toovisualize un trabajo de análisis de transmisiones de canalización para solución de problemas mediante la característica de diagrama de diagnósticos de Hola de autoservicio."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Visualización y solución de problemas de trabajos de Análisis de transmisiones
En el análisis de transmisiones, al igual que con otras tecnologías basadas en la nube, solución de problemas a veces es necesario toolook en ¿por qué un trabajo no genera salida de hello esperada (o ningún resultado para este propósito). Con esto en mente, análisis de transmisiones proporciona capacidad de Hola para visualizar un trabajo de streaming. Esto también resulta útil como herramienta de modelado y tiene la ventaja colateral de Hola para aquellas que requieren que la documentación de su trabajo.

En la visualización de hello son visibles, así como que se va a ejecutar la consulta de hello entradas de Hola de panel y, a continuación, todas las salidas de hello configuran. Problemas de conectividad o la configuración pueden resultan más evidentes y también puede ser útil toosee una representación visual de la configuración.

## <a name="using-hello-diagnosis-diagram-tool"></a>Utilizando la herramienta de diagramas de diagnóstico de Hola
tooaccess este visualizador, simplemente haga clic en hello en el botón de "Diagrama de diagnóstico" Hola hoja de "Configuración" de hello de trabajo de análisis de transmisiones de Hola.

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Cada entrada y salida es tooindicate codificadas mediante colores Hola estado actual de dicho componente, tal y como se muestra a continuación.

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

Cuando el usuario de hello desea toolook en patrones de flujo de datos hello toounderstand de pasos intermedios de la consulta dentro de un trabajo, herramienta de visualización de hello proporciona una vista de desglose de Hola de consulta de hello en sus pasos de componente y la secuencia de flujo de Hola. Al hacer clic en cada paso de consulta mostrará la sección correspondiente de hello en un panel, como se muestra de edición de consultas. 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

