---
title: "aaaAzure modelo de datos de telemetría de aplicación visión: excepción de telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de excepciones"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a>Telemetría de excepciones: modelo de datos de Application Insights

En [Application Insights](app-insights-overview.md), una instancia de excepción representa una excepción controlada o no controlada que se produjeron durante la ejecución de la aplicación hello supervisado.

## <a name="problem-id"></a>Identificador del problema

Identificador de donde se produjo la excepción de hello en el código. Se usa para el agrupamiento de las excepciones. Normalmente es una combinación de tipo de excepción y una función de la pila de llamadas de Hola.

Longitud máxima: 1024 caracteres

## <a name="severity-level"></a>Nivel de gravedad

El nivel de gravedad del seguimiento. El valor puede ser `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="exception-details"></a>Detalles de la excepción

(toobe extendido)

## <a name="custom-properties"></a>Propiedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Medidas personalizadas

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Pasos siguientes

- Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.
- Obtenga información acerca de cómo demasiado[diagnosticar las excepciones en las aplicaciones web con Application Insights](app-insights-asp-net-exceptions.md).
- Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.
