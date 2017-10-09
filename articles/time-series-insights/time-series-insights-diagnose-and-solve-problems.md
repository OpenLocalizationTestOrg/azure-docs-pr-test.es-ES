---
title: aaaDiagnose y solucionar problemas | Documentos de Microsoft
description: "Este tutorial trata cómo toodiagnose y solucionar problemas en su entorno de visión de la serie de tiempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Diagnóstico y solución de problemas de su entorno Time Series Insights

## <a name="i-dont-see-my-data"></a>No veo mis datos
A continuación, figuran algunas causas ¿por qué no puede ver los datos en su entorno de hello [portal de Azure tiempo serie visión](https://insights.timeseries.azure.com).

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>Su origen de eventos no tiene datos en formato JSON
Azure Time Series Insights solo admite actualmente datos JSON. Para ver ejemplos de JSON, consulte [Formas de JSON admitidas](time-series-insights-send-events.md#supported-json-shapes).

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>Cuando se registra el origen de eventos, no proporcionaba clave Hola que tenga permiso de hello necesario
* Para un centro de IoT, necesita clave hello tooprovide con **servicio conectar** permiso.

   ![Permiso de conexión de servicio de Iot Hub](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Como se muestra en hello anterior imagen, cualquiera de las directivas de hello **iothubowner** y **servicio** funcionaría, porque ambos tienen **servicio conectar** permiso.
* Para un concentrador de eventos, necesita clave hello tooprovide con **escuchar** permiso.

   ![Permiso de escucha de centro de eventos](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Como se muestra en hello anterior imagen, cualquiera de las directivas de hello **leer** y **administrar** funcionaría, porque ambos tienen **escuchar** permiso.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>Hola proporcionado grupo de consumidores no es exclusivo tooTime serie visión
Para un centro de IoT o un concentrador de eventos, durante el registro te requerimos que grupo de consumidores de hello toospecify que debe usarse para leer los datos. Este grupo de consumidores no debe compartirse. Si se comparte, centro de eventos subyacente Hola desconecta automáticamente a uno de los lectores de hello aleatoriamente.

## <a name="i-see-my-data-but-theres-a-lag"></a>Veo mis datos, pero hay un retraso
Éstas son las razones ¿por qué podría ver parte de los datos en su entorno de hello [portal de visión de la serie de tiempo](https://insights.timeseries.azure.com).

### <a name="your-environment-is-getting-throttled"></a>Puede que se esté limitando el entorno
Hola límite se aplica en función de tipo SKU y la capacidad del entorno de Hola. Todos los orígenes de eventos en el entorno de hello compartan esta capacidad. Si el origen de eventos de hello para el concentrador de eventos o centro de IoT es insertar datos más allá de los límites de hello exige, verá la limitación y un retraso.

Hola siguiente diagrama muestra un entorno de visión de la serie de tiempo que tiene un SKU de S1 y una capacidad de 3. Este entorno registra 3 millones de eventos al día.

![Capacidad actual de la SKU del entorno](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Se supone que este entorno es introducir mensajes de un concentrador de eventos con velocidad de entrada de Hola que se muestra en hello siguiente diagrama:

![Velocidad de entrada de ejemplo para una instancia de Event Hubs](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Como se muestra en el diagrama de hello, velocidad de entrada de diario de hello es ~ 67.000 mensajes. Esta velocidad traduce mensajes too46 aproximadamente cada minuto. Si cada mensaje de evento de base de datos central es tooa planas único evento de información de la serie de tiempo, este entorno no ve ninguna limitación. Si cada mensaje de evento de base de datos central es eventos de información de la serie de tiempo de too100 plana, 4 600 eventos deben ser ingestión cada minuto. Un entorno de SKU S1 que tiene una capacidad de 3 solo puede admitir la entrada de 2100 eventos por minuto (1 millón de eventos por día = 700 eventos por minuto por 3 unidades = 2100 eventos por minuto). Por lo tanto, verá un retraso toothrottling due. 

Para comprender de una manera más profunda cómo funciona la lógica de aplanamiento, consulte [Formas JSON admitidas](time-series-insights-send-events.md#supported-json-shapes).

#### <a name="recommended-steps"></a>Pasos recomendados
retardo de hello toofix, Hola de aumento de capacidad SKU de su entorno. Para obtener más información, consulte [cómo tooscale su entorno de visión de la serie de tiempo](time-series-insights-how-to-scale-your-environment.md).

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>Está insertando datos históricos lo cual provoca una entrada lenta
Si va a conectar un origen de eventos existente, es probable que su centro de eventos o instancia de IoT Hub ya contengan datos. Por lo que el entorno de hello inicia extraer datos desde el principio de hello del período de retención de mensajes del origen del evento de Hola. 

Este comportamiento es el comportamiento predeterminado de hello y no se puede invalidar. Se puede ocupar la limitación y puede tardar unos instantes toocatch seguridad sobre la ingesta de datos históricos.

#### <a name="recommended-steps"></a>Pasos recomendados
retardo de hello toofix, Hola toman pasos:
1. Aumentar Hola SKU capacidad toohello valor máximo permitido (10 en este caso). Después de que es aumentar la capacidad de hello, proceso de entrada de hello inicia poniendo mucho más rápido. Puede visualizar ¿con qué rapidez está acercando a través de gráfico de disponibilidad de Hola Hola [portal de visión de la serie de tiempo](https://insights.timeseries.azure.com). Se le cobra por hello mayor capacidad.
2. Después de hello lag se pone al día, disminuir la tasa de entrada normal de hello SKU capacidad back-tooyour.

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>Mi configuración de *nombre de propiedad timestamp* del origen de eventos no funciona
Asegúrese de que el valor y el nombre de hello ajustan toohello siguiendo reglas:
* nombre de propiedad de marca de tiempo de Hello es _entre mayúsculas y minúsculas_.
* valor de propiedad de marca de tiempo de Hola que procede de su origen de eventos, como una cadena JSON, debe tener el formato de hello _aaaa-MM-ddTHH. FFFFFFFK_. Un ejemplo de este tipo de cadena es "2008-04-12T12:53Z".
