---
title: aaaOverview de Fundamentos de Bus de servicio de Azure | Documentos de Microsoft
description: "Un tooconnect de Bus de servicio de toousing de introducción software tooother de las aplicaciones de Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Azure Service Bus

Si una aplicación o servicio se ejecuta en la nube de Hola o de forma local, a menudo necesita toointeract con otras aplicaciones o servicios. tooprovide toodo de una manera útil ampliamente, ofertas de Microsoft Azure Service Bus. En este artículo en esta tecnología, que describe qué es y por qué es recomendable toouse lo busca.

## <a name="service-bus-fundamentals"></a>Elementos fundamentales del Bus de servicio

Las distintas situaciones requieren distintos estilos de comunicación. A veces, que permite a las aplicaciones enviar y recibir mensajes a través de una cola simple es mejor solución de Hola. En otras situaciones, una cola ordinaria no es suficiente y es mejor una cola con un mecanismo de publicación y suscripción. En algunos casos, todo lo que hace falta es una conexión entre las aplicaciones y no se requieren colas. Bus de servicio proporciona las tres opciones, lo que permite su toointeract de aplicaciones de varias maneras diferentes.

Bus de servicio es un servicio de nube de varios inquilinos, lo que significa que el servicio de hello es compartido por varios usuarios. Cada usuario, por ejemplo, un desarrollador de aplicaciones crea una *espacio de nombres*, a continuación, define los mecanismos de comunicación de hello requeridos en ese espacio de nombres. La figura 1 muestra el aspecto de esta arquitectura.

![][1]

**Figura 1: Service Bus proporciona un servicio multiempresa para conectar las aplicaciones a través de la nube de Hola.**

Dentro de un espacio de nombres puede usar uno o más ejemplos de los tres mecanismos de comunicación diferentes, que se conectan a las aplicaciones de forma distinta. Hola opciones son:

* *Colas*, que permiten una comunicación unidireccional. Cada cola funciona como un intermediario (al que se le llama a veces *agente*) que almacena los mensajes enviados hasta que se reciben. Cada mensaje lo recibe un único destinatario.
* *Temas*, que proporcionan una comunicación unidireccional mediante *suscripciones* (un solo tema puede tener varias suscripciones). Como una cola, un tema actúa como un agente, pero cada suscripción puede utilizar opcionalmente un filtro tooreceive sólo los mensajes que cumplen determinados criterios.
* *Retransmisiones*, que permiten una comunicación bidireccional. A diferencia de las colas y los temas, las retransmisiones no almacenan mensajes que se encuentran en proceso; no son agentes. En su lugar, simplemente pasa ellos en la aplicación de destino de toohello.

Cuando cree una cola, un tema o una retransmisión, asígneles un nombre. En combinación con la que llama el espacio de nombres, este nombre genera un identificador único para el objeto de Hola. Las aplicaciones pueden proporcionar este tooService nombre Bus, utilice esa cola, tema o retransmisión toocommunicate entre sí. 

toouse cualquiera de estos objetos en el escenario de retransmisión de hello, aplicaciones de Windows pueden usar Windows Communication Foundation (WCF). Este servicio se conoce como [WCF Relay](../service-bus-relay/relay-what-is-it.md). En el caso de las colas y los temas, las aplicaciones de Windows pueden usar las API de mensajería definidas por el bus de servicio. toomake estos objetos toouse más fácil desde aplicaciones que no son de Windows, Microsoft proporciona SDK para Java, Node.js y otros lenguajes. También se puede acceder a las colas y a los temas mediante las [API de REST](/rest/api/servicebus/) sobre HTTP(s). 

Es importante toounderstand que incluso aunque el servicio de Bus de sí mismo se ejecuta en la nube de hello (es decir, en centros de datos de Microsoft Azure), las aplicaciones que lo usan y pueden ejecutar desde cualquier lugar. Puede utilizar aplicaciones de tooconnect de Bus de servicio se ejecuta en Azure, por ejemplo, o aplicaciones que se ejecutan dentro de su propio centro de datos. También puede utilizarlo tooconnect una aplicación que se ejecuta en Azure u otra plataforma en la nube con una aplicación local o con tabletas y teléfonos. Es posible incluso tooconnect electrodomésticos, sensores y otra aplicación de dispositivos tooa central ni ningún tooone otro. Bus de servicio es un mecanismo de comunicación en la nube de Hola que sea accesible desde prácticamente cualquier lugar. Modo en que usa depende de qué las aplicaciones necesitan toodo.

## <a name="queues"></a>Colas

Suponga que decide tooconnect dos aplicaciones mediante una cola de Bus de servicio. La ilustración 2 muestra esa situación.

![][2]

**Figura 2: las colas del Bus de servicio proporcionan una cola asincrónica unidireccional.**

proceso de Hello es simple: un remitente envía una cola de Service Bus de mensajes tooa y un receptor recoge ese mensaje en algún momento posterior. Una cola puede tener solo un único receptor, como muestra la Figura 2, O bien, varias aplicaciones pueden leer de hello misma cola. En este último caso hello, solo receptor lee cada mensaje. Para un servicio de multidifusión, es preciso utilizar un tema.

Cada mensaje tiene dos partes: un conjunto de propiedades, cada una de ellas, un par clave/valor, y una carga de mensaje. carga de Hello puede ser incluso XML, texto o binario. Cómo se utilizan depende de qué una aplicación está intentando toodo. Por ejemplo, una aplicación envía un mensaje acerca de una venta reciente podría incluir propiedades de hello **vendedor = "Ava"** y **cantidad = 10000**. el cuerpo del mensaje de Hola podría contienen una imagen digitalizada de contrato firmado de venta de Hola o, si no hay uno, permanecer vacío.

El receptor puede leer los mensajes de la cola del bus de servicio de dos formas distintas. Hola primera opción, denominada  *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, quita un mensaje de cola de Hola y elimina inmediatamente. Esta opción es sencilla, pero si el receptor de Hola se bloquea antes de finalizar el procesamiento de mensajes de bienvenida, mensaje de saludo se pierde. Dado que se han quitado de cola de hello, ningún otro receptor puede acceder a él. 

Hola segunda opción,  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, está pensado toohelp con este problema. Al igual que **ReceiveAndDelete**, **PeekLock** lectura quita un mensaje de la cola de Hola. No elimina el mensaje de saludo, sin embargo. En su lugar, bloquea el mensaje de saludo, lo que tooother invisible receptores, a continuación, espera a que uno de los tres eventos:

* Si los procesos de receptor de Hola Hola mensaje correctamente, llama a [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete), y cola de Hola elimina el mensaje de bienvenida. 
* Si el receptor de hello decide que no se puede procesar el mensaje de Hola correctamente, llama a [Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon). cola de Hello, a continuación, quita el bloqueo de Hola de mensaje de bienvenida de y hace que los receptores tooother disponible.
* Si el receptor de Hola llama a ninguno de estos métodos dentro de un período de tiempo configurable (de forma predeterminada, 60 segundos), cola Hola se da por supuesto receptor Hola ha fallado. En este caso, se comporta como si se hubiera llamado receptor hello **abandonar**, realizar Hola tooother disponibles los receptores de mensajes.

Tenga en cuenta lo que puede suceder aquí: hello mismo mensaje puede entregarse dos veces, quizás tootwo distintos destinatarios. Las aplicaciones que usan colas de Service Bus deben estar preparadas para este evento. toomake detección de duplicados más fácil, cada mensaje tiene un único [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propiedad que, de forma predeterminada, permanece Hola igual independientemente de cuántas veces mensajes de bienvenida se lee de una cola. 

Las colas son útiles en determinadas situaciones. Le permiten aplicaciones toocommunicate incluso cuando no se ejecutan en hello mismo tiempo, algo que resulta especialmente útil con aplicaciones móviles y por lotes. Una cola con varios receptores también proporciona un equilibrio de carga automático, ya que los mensajes enviados se difunden a través de esos receptores.

## <a name="topics"></a>Temas

Útil tal como están, las colas no están siempre solución correcta Hola. A veces, los temas de bus de servicio son mejores. La ilustración 3 muestra esa perspectiva.

![][3]

**Figura 3: En función de filtro de hello que especifica una aplicación de suscripción, puede recibir algunos o todos los mensajes de Hola envían tooa tema de Bus de servicio.**

A *tema* es similar en la cola de tooa de muchas maneras. Remitentes enviar tema de tooa de mensajes de Hola igual que envían la cola de mensajes tooa y apariencia de los mensajes hello igual que con las colas. Hello diferencia es que temas habilitar cada toocreate aplicación receptora su propio *suscripción* definiendo un *filtro*. Un suscriptor, a continuación, puede ver mensajes de Hola que coincida con dicho filtro. Por ejemplo, la Figura 3 muestra un remitente y un tema con tres suscriptores, cada uno con su propio filtro:

* Suscriptor 1 solo recibe mensajes que contienen propiedades de hello *vendedor = "Ava"*.
* Suscriptor 2 recibe mensajes que contienen propiedades de hello *vendedor = "Ruby"* o contener una *cantidad* propiedad cuyo valor es mayor que 100.000. Quizás Ruby es director de ventas de hello, por lo que desea toosee propias ventas y todas las ventas grandes sin tener en cuenta que hace que sean.
* Suscriptor 3 estableció su filtro demasiado*True*, lo que significa que recibe todos los mensajes. Por ejemplo, esta aplicación puede ser responsable de mantener una pista de auditoría y, por tanto, necesita toosee todos los mensajes de saludo.

Como con las colas, tema tooa de suscriptores puede leer los mensajes mediante [ReceiveAndDelete o PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode). Sin embargo, a diferencia de las colas, un único mensaje envía tooa tema puede ser recibido por varias suscripciones. Este método, normalmente denominado *publicar y suscribirse* (o *pub/sub*), es útil cuando varias aplicaciones están interesadas en hello mismos mensajes. Mediante la definición de filtro derecha hello, cada suscriptor puede aprovechar solo parte de hello del flujo de mensajes de Hola que necesita toosee.

## <a name="relays"></a>Retransmisiones

Tanto las colas como los temas proporcionan una comunicación asincrónica unidireccional a través de un agente. El tráfico fluye en una única dirección y no existe una conexión directa entre los remitentes y los receptores. Sin embargo, ¿qué ocurre si no quiere esa conexión? Suponga que las aplicaciones necesitan tooboth enviar y recibir mensajes, o tal vez desee crear un vínculo directo entre ellos y no es necesario un toostore los mensajes del agente. tooaddress escenarios como éste, Service Bus proporciona *retransmite*, como se muestra en la figura 4.

![][4]

**Figura 4: la retransmisión del Bus de servicio proporciona comunicación sincrónica bidireccional entre aplicaciones.**

Hello pregunta obvia tooask acerca de las retransmisiones es: ¿por qué debo usar? Aunque no necesito colas, ¿por qué realizar aplicaciones comunicarse a través de un servicio de nube en lugar de simplemente interactuar directamente? respuesta de Hello es que hablar directamente puede resultar más difícil de lo que parece.

Suponga que desea tooconnect dos aplicaciones locales, ambos se ejecutan dentro de los centros de datos corporativos. Cada una de esas aplicaciones se encuentran protegidas por un firewall y cada centro de datos usa probablemente la traducción de direcciones de red (NAT). bloques de firewall de Hello los datos entrantes en todos excepto unos puertos y NAT implica que cada aplicación se ejecuta en el equipo hello no tiene una dirección IP fija que puede tener acceso directamente desde el centro de datos fuera de Hola. Sin ayuda adicional, conectan estas aplicaciones a través de hello internet pública es problemático.

Una retransmisión de bus de servicio puede ser de gran ayuda. toocommunicate bidireccional a través de una retransmisión, cada aplicación establece una conexión TCP saliente con Bus de servicio, a continuación, mantiene abierta. Todas las comunicaciones entre dos aplicaciones de hello transmite a través de estas conexiones. Dado que cada conexión se estableció desde dentro de centros de datos de hello, Hola firewall permite entrantes tráfico tooeach aplicación sin tener que abrir puertos nuevos. Este enfoque también obtiene alrededor de problema NAT de hello, puesto que cada aplicación tiene un punto de conexión coherente en nube de hello en toda la comunicación de Hola. Mediante el intercambio de datos a través de retransmisión de hello, aplicaciones de hello pueden evitar problemas de Hola que harían en caso contrario dificultan la comunicación. 

toouse retransmite de Bus de servicio, las aplicaciones que se basan en hello Windows Communication Foundation (WCF). Bus de servicio proporciona enlaces de WCF que hacen que sea sencillo para toointeract de las aplicaciones de Windows a través de retransmisiones. Las aplicaciones que ya usan WCF suelen pueden especificar uno de estos enlaces y luego hablar tooeach otros a través de una retransmisión. Sin embargo, a diferencia de las colas y los temas, el uso, cuando sea posible, de retransmisiones desde aplicaciones que no sean de Windows requiere cierto esfuerzo de programación; no se proporcionan bibliotecas estándar.

A diferencia de lo que ocurre con las colas y los temas, las aplicaciones no crean retransmisiones explícitamente. En su lugar, cuando una aplicación que desea tooreceive mensajes establece una conexión TCP con el Bus de servicio, se crea automáticamente una retransmisión. Cuando se pierde la conexión de hello, se elimina la retransmisión de Hola. tooenable una retransmisión de hello toofind de aplicación creada por un agente de escucha específico, Bus de servicio proporciona un registro que permite a las aplicaciones toolocate una retransmisión específico por nombre.

Las retransmisiones son solución adecuada de hello cuando necesite una comunicación directa entre aplicaciones. Por ejemplo, piense en un sistema de reserva de una aerolínea que se ejecute en un centro de datos local y al que deba poder accederse desde mostradores de facturación, dispositivos móviles y otros equipos. Aplicaciones que se ejecutan en todos estos sistemas podían confiar en retransmisiones de Bus de servicio en hello en la nube toocommunicate, siempre que se podría estar ejecutando.

## <a name="summary"></a>Resumen

Conectar aplicaciones siempre ha sido parte de la creación de soluciones completas e intervalo Hola de escenarios que requieren las aplicaciones y servicios toocommunicate entre sí se ha establecido tooincrease sea más dispositivos y aplicaciones toohello conectado internet. Al proporcionar las tecnologías basadas en la nube para lograr la comunicación a través de colas, temas y retransmisiones, Bus de servicio, tiene como objetivo toomake esta tooimplement más fácil de función esencial y más ampliamente disponibles.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido Fundamentos de hello del Bus de servicio de Azure, siga estas toolearn de vínculos más.

* Cómo toouse [colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)
* Cómo toouse [temas de Bus de servicio](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* Cómo toouse [retransmisión de Bus de servicio](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [Ejemplos del Bus de servicio](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png
