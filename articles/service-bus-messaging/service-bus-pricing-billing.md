---
title: "precios y facturación de Bus aaaService | Documentos de Microsoft"
description: "Información general de la estructura de precios de Bus de servicio."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>Precios y facturación de Bus de servicio
Service Bus está disponible en los niveles Básico, Estándar y [Premium](service-bus-premium-messaging.md). Puede elegir un nivel de servicio para cada espacio de nombres del servicio Service Bus que cree y esta selección de nivel se aplica a todas las entidades creadas dentro de ese espacio de nombres.

> [!NOTE]
> Para obtener información detallada sobre los precios de Bus de servicio actual, vea hello [página de precios de Azure Service Bus](https://azure.microsoft.com/pricing/details/service-bus/), hello y [P+F de Bus de servicio](service-bus-faq.md#pricing).
>
>

Bus de servicio utiliza Hola siguiendo dos metros para colas y temas/suscripciones:

1. **Operaciones de mensajería**: definidas como llamadas API en los puntos de conexión de servicio de colas o temas y suscripciones. Este contador reemplazará los mensajes enviados o recibidos como unidad principal de Hola de uso facturable para las colas y temas/suscripciones.
2. **Conexiones asíncronas**: define como el número máximo de Hola de conexiones persistentes abiertas contra colas, temas o suscripciones durante un período de muestreo de una hora determinada. Este contador sólo se aplicará en el nivel estándar de hello, en el que puede abrir conexiones adicionales (anteriormente, las conexiones estaban too100 limitado por cola/tema/suscripción) por una cuota nominal por conexión.

Hola **estándar** dispone de nivel de precios escalonados para operaciones realizadas con colas y temas/suscripciones, lo que da lugar a descuentos basados en volumen de too80% en niveles más altos de uso de Hola. También hay un cargo base del nivel estándar de 10 $ al mes, lo que permite tooperform seguridad too12.5 millón de operaciones al mes sin costo adicional alguno.

Hola **Premium** nivel proporciona aislamiento de los recursos en la capa de CPU y memoria de Hola para que cada carga de trabajo de cliente se ejecuta de forma aislada. Este contenedor de recursos se llama *unidad de mensajería*. A cada espacio de nombres premium se le asigna al menos una unidad de mensajería. Puede comprar 1, 2 o 4 unidades de mensajería para cada espacio de nombres Premium del Bus de servicio. Una carga de trabajo único o una entidad puede abarcar varias unidades de mensajes y se puede cambiar el número de Hola de unidades de mensajería como desee, aunque es facturación en unas tasas de 24 horas o diaria. resultado de Hello es rendimiento predecible y repetible para su solución basada en el Bus de servicio. Este rendimiento no es solo más predecible y presenta mayor disponibilidad, sino que también es más rápido.

Tenga en cuenta que cargo base del nivel estándar de Hola se cobra solo una vez al mes por suscripción de Azure. Esto significa que después de crear un espacio de nombres de Bus de servicio de nivel estándar único, será capaz de toocreate tantos estándares espacios de nombres adicionales como desee en esa misma suscripción de Azure, sin incurrir en adicionales base cargos.

Hola [precios de Bus de servicio](https://azure.microsoft.com/pricing/details/service-bus/) tabla resumen las diferencias funcionales de hello entre niveles de Basic, Standard y Premium de Hola.

## <a name="messaging-operations"></a>Operaciones de mensajería
Como parte del programa Hola nuevo modelo de precios, facturación de colas y temas/suscripciones está cambiando. Estas entidades están pasando de una facturación por mensaje toobilling por operación. Una "operación" hace referencia llamada tooany API realizada en un extremo de servicio cola o tema/suscripción. Esto incluye las operaciones de administración, envío/recepción y estado de la sesión.

| Tipo de operación | Description |
| --- | --- |
| Administración |Creación, lectura, actualización, eliminación (CRUD) en colas, temas o suscripciones. |
| Mensajería |Envío y recepción de mensajes con colas, temas o suscripciones. |
| Estado de la sesión |Recuperación o establecimiento del estado de la sesión en una cola, un tema o una suscripción. |

Para obtener detalles de costo, vea los precios de hello indicados en hello [precios de Bus de servicio](https://azure.microsoft.com/pricing/details/service-bus/) página.

## <a name="brokered-connections"></a>Conexiones asincrónicas
Las *conexiones asincrónicas* se adaptan a los patrones de uso de clientes que tienen que ver con una gran cantidad de remitentes/receptores "conectados de forma persistente" a colas, temas o suscripciones. Los remitentes/receptores conectados de forma persistente son aquellos que se conectan mediante AMQP o HTTP con un tiempo de expiración de recepción distinto a cero (por ejemplo, HTTP long polling). Los remitentes y receptores con un tiempo de expiración inmediato no generarán conexiones asíncronas.

Para las cuotas de conexión y otros límites de servicio, vea hello [cuotas de Bus de servicio](service-bus-quotas.md) artículo.

nivel estándar de Hello quita el límite de conexión asíncrona por espacio de nombres de Hola y recuentos de uso de la conexión asíncrona total en hello suscripción de Azure. Para obtener más información, vea hello [conexiones asíncronas](https://azure.microsoft.com/pricing/details/service-bus/) tabla.

> [!NOTE]
> 1000 conexiones asíncronas se incluyen con el nivel de mensajería estándar hello (a través de cargo base de hello) y se pueden compartir entre todas las colas, temas y suscripciones en suscripción de Azure Hola asociado.
>
>

<br />

> [!NOTE]
> La facturación se basa en el número máximo de Hola de conexiones simultáneas y se prorratea según basándose en 744 horas al mes.
>
>

| Nivel Premium |
| --- |
| No se le cobrará conexiones asíncronas en el nivel de hello Premium. |

Para obtener más información sobre las conexiones asíncronas, vea hello [preguntas más frecuentes sobre](#faq) sección más adelante en este tema.

## <a name="faq"></a>P+F

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>¿Qué son las conexiones asíncronas y cómo se cobran?
Una conexión asíncrona se define como uno de hello siguientes:

1. Una conexión AMQP desde una cola de Bus de servicio de cliente tooa o tema/suscripción.
2. Una llamada HTTP, tooreceive un mensaje de un tema de Bus de servicio o una cola que tiene un valor de tiempo de espera de recepción mayor que cero.

Los cargos de Bus de servicio de número máximo de Hola de conexiones asíncronas concurrentes que supere Hola incluyen cantidad (1.000 en el nivel estándar de hello). Valores máximos se mide en cada hora, prorratea dividiendo por 744 horas en un mes y sumándolos Hola período de facturación mensual. cantidad Hola incluido (1000 conexiones asíncronas al mes) se aplica al final de hello del período de facturación de hello en suma de Hola de hello prorrateada máximos de horas.

Por ejemplo:

1. Los 10 000 dispositivos se conectan mediante una conexión AMQP individual y reciben comandos desde un tema de Service Bus. Hola dispositivos la envían eventos de telemetría tooan concentrador de eventos. Si todos los dispositivos se conectan durante 12 horas cada día, se aplica Hola siguientes cargos por conexión (en suma tooany otros cargos de tema de Bus de servicio): 10.000 conexiones * 12 horas * 31 días / 744 = 5,000 conexiones asíncronas. Después de la deducción mensual de Hola de 1000 conexiones asíncronas, se le cobrarían 4000 conexiones asíncronas, con velocidad de Hola de 0,03 $ por cada conexión asíncrona, para un total de 120 $.
2. 10.000 dispositivos reciben mensajes desde una cola de Bus de servicio mediante HTTP, especificando un tiempo de expiración distinto a cero. Si todos los dispositivos se conectan durante 12 horas cada día, verá Hola siguientes cargos por conexión (en suma tooany otros cargos de Bus de servicio): 10.000 conexiones de recepción HTTP * 12 horas al día * 31 días / 744 horas = 5.000 conexiones asíncronas.

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>¿Pueden aplicar cargos por conexión asíncrona tooqueues y temas/suscripciones?
Sí. No hay ningún cargo de conexión para el envío de eventos mediante HTTP, independientemente del número de Hola de envío de sistemas o dispositivos. La recepción de eventos con HTTP con un tiempo de expiración superior a cero, que a menudo se conoce como "long polling", genera cargos por conexión asíncrona. Las conexiones AMQP generan cargos por conexión asíncrona independientemente de si las conexiones de hello están siendo utilizado toosend o de recepción. Tenga en cuenta que se permiten 100 conexiones asíncronas sin cargo en un espacio de nombres Básico. Se trata también de Hola número máximo de conexiones asíncronas permitidas para hello suscripción de Azure. Hello primeras 1000 conexiones asíncronas a través de todos los espacios de nombres estándares en una suscripción de Azure se incluyen sin cargo adicional (más allá del cargo base de hello). Dado que estos números son suficientes toocover muchos escenarios de mensajería de service to service, cargos de conexión asíncrona normalmente solo son relevantes si tiene previsto toouse AMQP o HTTP sondeo largo con un gran número de clientes; Por ejemplo, tooachieve más eficiente eventos de transmisión por secuencias o habilitar la comunicación bidireccional con muchos dispositivos o instancias de la aplicación.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener información detallada sobre los precios de Bus de servicio, vea hello [página de precios de Bus de servicio](https://azure.microsoft.com/pricing/details/service-bus/).
* Vea hello [P+F de Bus de servicio](service-bus-faq.md#pricing) para algunas preguntas más frecuentes sobre comunes acerca de bus de servicio precios y facturación.

[Azure portal]: https://portal.azure.com
