---
title: "aaaAzure modelo de datos de telemetría de aplicación visión - dependencia telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de dependencias"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a>Telemetría de dependencias: modelo de datos de Application Insights

Telemetría de dependencia (en [Application Insights](app-insights-overview.md)) representa una interacción del componente de hello supervisado con un componente remoto como SQL o un extremo HTTP.

## <a name="name"></a>Nombre

Nombre del comando de hello iniciada con esta llamada de dependencia. Valor de cardinalidad bajo. Algunos ejemplos son el nombre del procedimiento almacenado y la plantilla de ruta de acceso de dirección URL.

## <a name="id"></a>ID

Identificador de una instancia de llamada de dependencia. Se utiliza para la correlación con elemento de telemetría de solicitud de hello correspondiente toothis dependencia llamada. Para obtener más información, vea la página de [correlación](application-insights-correlation.md).

## <a name="data"></a>Datos

Comando iniciado por esta llamada de dependencia. Algunos ejemplos son la instrucción SQL y la dirección URL HTTP con todos los parámetros de consulta.

## <a name="type"></a>Tipo

Nombre del tipo de dependencia. Valor de cardinalidad bajo para una agrupación lógica de dependencias y la interpretación de otros campos como commandName y resultCode. Algunos ejemplos son SQL, tabla de Azure y HTTP.

## <a name="target"></a>Destino

Sitio de destino de una llamada de dependencia. Algunos ejemplos son el nombre del servidor y la dirección de host. Para más información, vea la página de [correlación](application-insights-correlation.md).

## <a name="duration"></a>Duración

Duración de la solicitud en formato: `DD.HH:MM:SS.MMMMMM`. Debe ser menor de `1000` días.

## <a name="result-code"></a>Código de resultado

Código de resultado de una llamada de dependencia. Algunos ejemplos son el código de error SQL y el código de estado HTTP.

## <a name="success"></a>Correcto

Indicación de si la llamada es correcta o no.

## <a name="custom-properties"></a>Propiedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Medidas personalizadas

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a>Pasos siguientes

- Configure el seguimiento de dependencias para [.NET](app-insights-asp-net-dependencies.md).
- Configure el seguimiento de dependencias para [Java](app-insights-java-agent.md).
- [Escritura de una telemetría de dependencia personalizada](app-insights-api-custom-events-metrics.md#trackdependency)
- Consulte el [modelo de datos](application-insights-data-model.md) para ver los tipos y el modelo de datos de Application Insights.
- Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.
