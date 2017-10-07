---
title: "procesamiento con el procesamiento de eventos de análisis de transmisiones de eventos de tiempo de aaaReal | Documentos de Microsoft"
description: "Aprenda cómo puede interoperar un conjunto de servicios de Azure para habilitar el procesado de eventos en tiempo real y el análisis."
keywords: procesamiento en tiempo real, procesamiento de eventos, arquitectura de referencia
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Arquitectura de referencia: procesado de eventos en tiempo real con Análisis de transmisiones de Microsoft Azure
arquitectura de referencia de Hola para procesamiento con análisis de transmisiones de Azure de eventos en tiempo real está previsto tooprovide un plano genérico para la implementación de una plataforma en tiempo real como una solución de procesamiento de transmisiones de servicio (PaaS) con Microsoft Azure.

## <a name="summary"></a>Resumen
Tradicionalmente, las soluciones de análisis se han basado en funciones como ETL (extracción, transformación, carga) y el almacenamiento de datos, donde los datos están almacenados tooanalysis anterior. Cambios en los requisitos, incluidos los datos más rápidamente que llegan tarde, están realizando la inserción de este límite de toohello modelo existente. datos Hola capacidad tooanalyze móvil toostorage anteriores de secuencias están una solución, y aunque no es una nueva capacidad, el enfoque de hello no se ha adoptado ampliamente en todos los mercados verticales de la industria. 

Microsoft Azure proporciona un catálogo muy amplio de tecnologías de análisis que pueden admitir una matriz de diferentes requisitos y escenarios de solución. Seleccionar qué toodeploy los servicios de Azure para una solución end-to-end puede ser un desafío dado la amplitud de Hola de ofertas. Este documento está diseñado toodescribe Hola capacidades e interoperación de Hola varios servicios de Azure que admiten una solución de transmisión de eventos. También se explican algunos de los escenarios de hello en el que los clientes pueden beneficiarse de este tipo de enfoque.

## <a name="contents"></a>Contenido
* Resumen ejecutivo
* Análisis en tiempo de tooReal Introducción
* Propuesta de valor de datos en tiempo real en Azure
* Escenarios comunes para el análisis en tiempo real
* Arquitectura y componentes
  * Orígenes de datos
  * Capa de integración de datos
  * Capa de análisis en tiempo real
  * Capa de almacenamiento de datos
  * Presentación / capa de consumo
* Conclusión

**Autor:** Charles Feddersen, arquitecto de soluciones, Centro de excelencia de Data Insights, Microsoft Corporation

**Publicado:** enero de 2015

**Revisión:** 1.0

**Descarga:**[Procesado de eventos en tiempo real con Análisis de transmisiones de Microsoft Azure](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

