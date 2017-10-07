---
title: "aaaAzure modelos de datos de telemetría de aplicación visión, evento de telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de eventos"
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a>Telemetría de eventos: modelo de datos de Application Insights

Puede crear eventos de elementos de telemetría (en [Application Insights](app-insights-overview.md)) toorepresent un evento producido en la aplicación. Normalmente es una interacción del usuario como un clic de botón o la desprotección de un pedido. También puede ser un evento de ciclo de vida de la aplicación como la actualización de la inicialización o la configuración. 

Semánticamente, eventos pueden o no ser toorequests correlacionados. Pero si se usa correctamente, la telemetría de eventos es más importante que las solicitudes o los seguimientos. Eventos representan la telemetría de negocio y debe ser un tooseparate asunto, menos agresiva [muestreo](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Nombre

Nombre del evento. agrupación adecuada tooallow y métricas útiles, restringir la aplicación para que genere un pequeño número de nombres de evento independiente. Por ejemplo, no utilice un nombre diferente para cada instancia generada de un evento.

Longitud máxima: 512 caracteres

## <a name="custom-properties"></a>Propiedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Medidas personalizadas

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Pasos siguientes

- Consulte el [modelo de datos](application-insights-data-model.md) para ver los tipos y el modelo de datos de Application Insights.
- [Escritura de telemetría de eventos personalizada](app-insights-api-custom-events-metrics.md#trackevent)
- Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.
