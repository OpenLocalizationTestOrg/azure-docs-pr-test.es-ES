---
title: "información general de mensajería de Bus de servicio de aaaAzure | Documentos de Microsoft"
description: "Descripción de la mensajería de Service Bus y Azure Relay"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Bus de servicio de mensajería: entrega flexible de los datos en la nube de Hola
Microsoft Azure Service Bus es un servicio de entrega de información confiable. Hola de este servicio sirve toomake comunicación sea más fácil. Cuando dos o más partes desean información de tooexchange, necesitan un facilitador de comunicación. Service Bus es un mecanismo de comunicación asincrónica o de terceros. Se trata de servicio de postal tooa similar en Hola mundo físico. Servicios postales que sea muy fácil toosend diferentes tipos de paquetes con una variedad de garantías de entrega y letras en cualquier lugar en Hola a todos.

Similar servicio postal de toohello letras, Bus de servicio de entrega es entrega información flexible de hello remitente y destinatario Hola. servicio de mensajería de Hello garantiza que información Hola se entregue incluso si Hola dos partes nunca tanto en línea en hello al mismo tiempo, o si no están disponibles en hello exactamente igual tiempo. De esta manera, mensajería es similar toosending una letra, mientras que comunicación asíncrona no es tooplacing similar una llamada de teléfono (o uso de una llamada de teléfono toobe - antes de identificador de llamada en espera y el autor de la llamada, que son mucho más como mensajería asíncrona).

el remitente del mensaje de Hola puede requerir también una variedad de características de la entrega incluidas transacciones, detección de duplicados, basado en tiempo de expiración y procesamiento por lotes. Estos patrones también tienen analogías postales: repetición de la entrega, requerimiento de firma, cambio de dirección o devolución de llamada.

Service Bus admite dos patrones de mensajería distintos: *Azure Relay* y *Service Bus Messaging*.

## <a name="azure-relay"></a>Azure Relay
Hola [retransmisión de WCF](../service-bus-relay/relay-what-is-it.md) componente de retransmisión de Azure es un servicio centralizado (pero gran equilibrio de carga) que admite diversos protocolos de transporte y estándares de servicios Web. Incluye SOAP, WS-* e incluso REST. Hola [servicio de retransmisión](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) proporciona una variedad de opciones de conectividad de retransmisión y puede ayudar a negociar conexiones directas de punto a punto cuando es posible. Bus de servicio está optimizado para los desarrolladores de .NET que usan Hola Windows Communication Foundation (WCF), ambos con tooperformance de tener en cuenta y la facilidad de uso, y proporciona acceso completo tooits servicio de retransmisión a través de interfaces SOAP y REST. Esto permite que cualquier programación SOAP o REST toointegrate entorno con Bus de servicio.

servicio de retransmisión de Hello admite mensajería unidireccional tradicional, mensajería de solicitud/respuesta y mensajería punto a punto. También admite la distribución de eventos en el ámbito de Internet tooenable la publicación y suscripción escenarios y comunicación de socket bidireccional para conseguir una eficacia mayor punto a punto. En el patrón de mensajería retransmitida de hello, un servicio local conecta toohello servicio de retransmisión a través de un puerto de salida y crea un socket bidireccional para la dirección de comunicación enlazada tooa encuentro concreta. cliente de Hello, a continuación, puede comunicarse con servicio de local de hello mediante el envío de mensajes de servicio de retransmisión toohello Hola rendezvous dirección de destino. servicio de retransmisión de Hello, a continuación, "retransmitirá" servicio de mensajes toohello local a través del socket bidireccional de hello ya están en vigor. Hello cliente no necesita un servicio local de toohello de conexión directa, ni tampoco requiere tooknow donde reside el servicio de Hola y Hola local servicio no necesita ningún puerto de entrada abierto en firewall de Hola.

Iniciar conexión Hola entre el servicio local y servicio de retransmisión de hello, utilizando un conjunto de enlaces de WCF "de retransmisión". Entre bastidores de hello, enlaces de retransmisión de hello asignan tootransport enlace elementos diseñados toocreate WCF componentes de canal que se integran con el Bus de servicio en nube de Hola.

Retransmisión de WCF ofrece numerosas ventajas, pero requiere que el servidor de Hola y estar en línea al mismo tiempo en orden toosend y recibir mensajes de Hola tooboth de cliente. Esto no es óptimo para la comunicación de estilo HTTP, en qué hello las solicitudes no pueden ser normalmente larga duración, ni para los clientes que se conectan ocasionalmente, como los exploradores, aplicaciones móviles y así sucesivamente. La mensajería asíncrona admite la comunicación desacoplada y tiene sus propias ventajas; los clientes y servidores se pueden conectar cuando sea necesario y realizar sus operaciones de forma asincrónica.

## <a name="brokered-messaging"></a>Mensajería asíncrona
En cambio toohello retransmisión esquema, Bus de servicio de mensajería, o [mensajería asíncrona](service-bus-queues-topics-subscriptions.md) puede interpretarse como asincrónica o "temporalmente desacoplada". Los productores (remitentes) y los consumidores (receptores) no tiene toobe en línea en hello mismo tiempo. infraestructura de mensajería de Hello almacena de forma confiable los mensajes en un "agente" (por ejemplo, una cola) hasta que la parte consumidora de hello esté listo tooreceive ellos. Esto permite a los componentes de Hola de toobe de aplicación Hola distribuido desconectados, ya sea voluntariamente; Por ejemplo, para el mantenimiento o debido a un bloqueo del componente tooa, sin que afecte a todo el sistema Hola. Además, aplicación receptora Hola solo puede tener toocome en línea durante determinadas horas del día de hello, como un sistema de administración de inventarios que solo es necesario toorun final Hola de día laborable de Hola.

componentes principales de Hola de infraestructura de mensajería asíncrona de Bus de servicio de hello son colas, temas y suscripciones.  Hola principal diferencia es que los temas admiten capacidades de publicación/suscripción que pueden usarse para contenidos de enrutamiento y entrega una lógica sofisticada, incluido el envío de los destinatarios de toomultiple. Estos componentes permiten nuevos escenarios de mensajería asincrónicos, como desacoplamiento temporal, publicación/suscripción y equilibrio de carga. Para más información sobre estas entidades de mensajería, vea [Colas, temas y suscripciones de Service Bus](service-bus-queues-topics-subscriptions.md).

Como con la infraestructura de retransmisión de WCF de hello, Hola mensajería asíncrona se proporciona funcionalidad para los programadores WCF y .NET Framework y también a través de REST.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la mensajería de Bus de servicio, vea Hola temas siguientes.

* [Elementos fundamentales de Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Colas, temas y suscripciones de Service Bus](service-bus-queues-topics-subscriptions.md)
* [¿Cómo toouse colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [¿Cómo toouse Service Bus temas y suscripciones](service-bus-dotnet-how-to-use-topics-subscriptions.md)

