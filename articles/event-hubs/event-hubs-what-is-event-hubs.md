---
title: "aaaWhat centros de eventos de Azure y por qué usarla | Documentos de Microsoft"
description: "Información general e introducción tooAzure centros de eventos - recopilación de telemetría de escala de nube de sitios Web, aplicaciones y dispositivos"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>¿Qué es Event Hubs?

Azure Event Hubs es una plataforma de streaming de datos y servicio de ingesta de eventos de gran escalabilidad que es capaz de recibir y procesar millones de eventos por segundo. Event Hubs puede procesar y almacenar eventos, datos o telemetría generados por dispositivos y software distribuido. Los datos se envían tooan concentrador de eventos se puede transformar y almacenado con cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento y procesamiento por lotes. Con hello capacidad tooprovide [capacidades de publicación / suscripción](https://msdn.microsoft.com/library/aa560414.aspx) con una latencia baja y a escala masiva, los concentradores de eventos actúa como Hola "en rampa" para grandes cantidades de datos.

## <a name="why-use-event-hubs"></a>¿Por qué usar Event Hubs?

Las funcionalidades de control de eventos y telemetría de Event Hubs lo hacen especialmente útil para:

* Instrumentación de aplicaciones
* La experiencia del usuario o el procesamiento de flujos de trabajo
* Escenarios de Internet de las cosas (IoT)

Por ejemplo, Event Hubs permite el seguimiento del comportamiento en aplicaciones móviles, la información sobre el tráfico de granjas de servidores web, la captura de eventos en juegos de consola o la recopilación de telemetría de máquinas industriales, vehículos conectados u otros dispositivos.

## <a name="azure-event-hubs-overview"></a>Información general de los Centros de eventos de Azure

Hello rol común que los concentradores de eventos se reproduce en arquitecturas de soluciones es hello "puerta principal" para una canalización de eventos, se llama a menudo un *introductor de eventos*. Un introductor de eventos es un componente o servicio que se encuentra entre los publicadores de eventos y producción de hello de toodecouple de los consumidores de eventos de una secuencia de eventos del consumo de Hola de esos eventos. Hello en la ilustración siguiente se muestra esta arquitectura:

![Centros de eventos](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Event Hubs proporciona una funcionalidad de control del flujo de mensajes pero tiene características diferentes de la mensajería empresarial tradicional. Las funcionalidades de Event Hubs se basan en un alto rendimiento y en escenarios de procesamiento de eventos. Por lo tanto, es diferente de los centros de eventos [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) de mensajería y no implementa algunas de las capacidades de Hola que están disponibles para [Bus de servicio de mensajería](/azure/service-bus-messaging/) entidades, como temas.

## <a name="event-hubs-features"></a>Características de Event Hubs

Los concentradores de eventos contiene Hola siguientes elementos clave:

- [**Los productores y los publicadores de eventos**](event-hubs-features.md#event-publishers): una entidad que envía el concentrador de eventos de tooan de datos. Se publica un evento mediante AMQP 1.0 o HTTPS.
- [**Capturar**](event-hubs-features.md#capture): permite los centros de eventos de toocapture transmisión de datos y almacenarla en una cuenta de almacenamiento de blobs de Azure.
- [**Las particiones**](event-hubs-features.md#partitions): permite que cada consumidor tooonly lee un subconjunto específico, o partición, de hello secuencia de eventos.
- [**Tokens de SAS**](event-hubs-features.md#sas-tokens): identifica y autentica el publicador de eventos de Hola.
- [**Consumidores de eventos**](event-hubs-features.md#event-consumers): una entidad que lee datos de eventos procedentes de un centro de eventos. Los consumidores de eventos se conectan a través de AMQP 1.0. 
- [**Grupos de consumidores**](event-hubs-features.md#consumer-groups): proporciona cada múltiplo consumir la aplicación con una vista independiente de la secuencia de eventos de hello, habilitando esos tooact consumidores independientemente.
- [**Unidades de procesamiento**](event-hubs-features.md#capacity): unidades de capacidad adquiridas previamente. Una partición individual tiene una escala máxima de una unidad de procesamiento.

Para obtener información técnica acerca de estas y otras características de los centros de eventos, vea hello [Introducción a características de los centros de eventos](event-hubs-features.md). 

## <a name="next-steps"></a>Pasos siguientes

Para información detallada sobre los precios de Event Hubs, consulte [Precios de Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

Para obtener más información acerca de los centros de eventos, visite Hola siguientes vínculos:

* Empiece por un [tutorial de Event Hubs](event-hubs-dotnet-standard-getstarted-send.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)
* [Aplicaciones de ejemplo que usan Event Hubs](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

