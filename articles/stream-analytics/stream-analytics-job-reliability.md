---
title: Evitar interrupciones de servicio con trabajos de Azure Stream Analytics | Microsoft Docs
description: "Guía sobre cómo realizar la actualización resistente de los trabajos de Stream Analytics."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Garantía de la confiabilidad del trabajo de Stream Analytics durante las actualizaciones del servicio

Parte de un servicio completamente administrado es Hola capacidad toointroduce nueva funcionalidad de servicio y las mejoras a un ritmo rápida. Como resultado, Stream Analytics puede tener una actualización de servicio implementada de forma semanal (o más frecuentemente). Independientemente de cuántas pruebas se realizan sigue siendo un riesgo de que un trabajo existente, la ejecución se puede dividir debido toohello introducción de un error. Para los clientes que ejecutan trabajos de procesamiento de transmisión por secuencias críticos estos riesgos deben toobe evitar. Un mecanismo los clientes pueden utilizar tooreduce el riesgo es Azure  **[región emparejada](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modelo. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>¿Cómo solucionan este problema las regiones emparejadas de Azure?

Stream Analytics garantiza que los trabajos de las regiones emparejadas se actualicen en lotes separados. Como resultado, hay un intervalo de tiempo suficiente entre las actualizaciones de hello tooidentify potencial interrupción errores y corregirlas.

_Con excepción de Hola de India Central_ (cuyo región emparejada, sur de India, no tiene presencia de análisis de transmisiones), implementación de Hola de un tooStream de actualización de análisis no se producirían en hello mismo tiempo en un conjunto de regiones emparejadas. Las implementaciones en varias regiones **Hola mismo grupo** puede producirse **en hello vez**.

artículo de Hello en  **[disponibilidad y regiones emparejadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  tiene la información más actualizada de hello en el que están emparejadas de regiones.

Los clientes están toodeploy aconsejable trabajos idénticos tooboth emparejado regiones. Además tooStream análisis internos de las funciones, los clientes de seguimiento también son recomienda trabajos de hello toomonitor como si **ambos** trabajos de producción. Si un salto es toobe identificado un resultado de la actualización de servicio de análisis de transmisiones de hello, escalar de forma adecuada y conmutar por error ninguna salida de trabajo correcto de toohello de los consumidores de nivel inferior. Extensión toosupport impedirá que región emparejada de Hola se vean afectados por la nueva implementación de Hola y mantener la integridad de Hola de trabajos de hello emparejado.
